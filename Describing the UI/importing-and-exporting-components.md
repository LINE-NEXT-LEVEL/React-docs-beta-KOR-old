# 컴포넌트 가져오기(importing), 내보내기(exporting)
컴포넌트의 마법은 재사용성에 있습니다: 다른 컴포넌트로 이루어진 컴포넌트들을 만들 수 있습니다.
하지만 더 많은 컴포넌트 계층을 쌓음에 따라, 별도의 파일로 분리하는 것이 더 합리적인 선택이 될 수 있습니다.
이는 파일들을 더 쉽게 찾고, 많은 곳에 재사용하기 좋게 해줍니다.

> 여러분이 배울 것들
> - 루트 컴포넌트 파일이 무엇인지
> - 컴포넌트를 import, export하는 방법
> - import, export 시 default vs named 구분하기
> - 하나의 파일에서 여러 컴포넌트를 import & export 하는 방법
> - 컴포넌트들을 여러 파일로 분리하는 방법


## 루트 컴포넌트 파일
[CodeSandbox](https://codesandbox.io/s/fpeliw?file=%2FApp.js&from-sandpack=true)
```js
function Profile() {
  return (
    <img
      src="https://i.imgur.com/MK3eW3As.jpg"
      alt="Katherine Johnson"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```
![image](https://user-images.githubusercontent.com/15559593/185513368-e60a55c7-9835-4648-8eb7-c086c9399bec.png)

이는 루트 컴포넌트파일인 App.js에 있습니다. 이 예제의 [Create React App](https://create-react-app.dev/)에서 여러분의 app은 `src/App.js`에 있습니다. 여러분의 설정에 따라 루트 컴포넌트파일은 다른 파일이 될 수도 있습니다. Next.js와 같은 file-based 라우팅을 기반으로한 프레임워크를 사용하신다면, 여러분의 루트 컴포넌트는 각 페이지별로 달라질거에요.

## 컴포넌트를 import, export하는 방법

추후에 랜딩화면을 바꿔 과학 도서들을 놓고싶다? 혹은 모든 프로필을 다른곳에 배치하고 싶다면? `Gallery`와 `Profile`을 루트 컴포넌트에서 옮기는 것이 합리적입니다.
이는 저 요소들을 더 모듈화하고 다른파일에 재사용하기 유리하게합니다.
다음 세가지 단계를 따라 컴포넌트를 옮길 수 있습니다.

1. 컴포넌트들을 넣을 새로운 JS파일을 만든다.
2. 그 파일에서 함수형 컴포넌트를 export([default](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/export#using_the_default_export)나. [named](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/export#using_named_exports)방식을 쓰세요)
3. 그 컴포넌트를 사용할 파일에 import시키세요([default](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/import#importing_defaults)나. [named](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/import#import_a_single_export_from_a_module)방식을 쓰세요)

여기 `Profile`과 `Gallery`가 App.js로부터 분리되어 `Gallery.js`라는 새로운 파일에 옮겨졌습니다. 이제 여러분은 `Gallery.js`에서 `Gallery`를 App.js에 import할 수 있습니다.

[CodeSandbox](https://codesandbox.io/s/wcbt4e?file=%2FGallery.js&from-sandpack=true)
```js
//App.js
import Gallery from './Gallery.js';

export default function App() {
  return (
    <Gallery />
  );
}

```
```js
//Gallery.js
function Profile() {
  return (
    <img
      src="https://i.imgur.com/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```
![image](https://user-images.githubusercontent.com/15559593/185513425-1ddfddd2-90d4-4712-a372-378870d1f199.png)


이 예제가 어떻게 두 컴포넌트 파일로 분리되었는지 살펴봅시다.
1. `Gallery.js`:
   - 같은 파일 내에서만 활용되고 export 되지 않았던 `Profile` 컴포넌트 정의합니다.
   - `Gallery` 컴포넌트를 default export로 export합니다.
2. `App.js`:
   - `Gallery.js`로부터 `Gallery`를 default import 합니다.
   - 루트 `App`컴포넌트를 default export 합니다.

> ## Note
> 파일 확장자인 `.js`를 떼고 다음과 같이 표현된 파일을 보게 될겁니다.
> ```js
> import Gallery from './Gallery';
> ```
> `./Gallery.js`나 `./Gallery` 둘 다 React에서 동작하지면, 전자가 [native ES Modules](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Modules)의 동작방식과 유사합니다.

> ## DEEP DIVE
> Default vs Named Exports
> Javascript로 export하는 두가지 방법이 있습니다.
> default와 named export이죠. 지금까지 우리의 예시들은 default export만 써왔습니다. 하지만 여러분은 두가지 방법을 같은 파일에서 쓸 수 있습니다. default export는 하나만 가질 수 있지만, named export는 여러개 가질 수 있습니다.
![image](https://user-images.githubusercontent.com/15559593/185513474-9afb38c9-99e0-48d3-b349-1a6b702d99e5.png)

> 여러분의 컴포넌트를 export하는 방식은 import를 어떻게 하냐에 따라 달라집니다. named export를 import하듯이 default export를 import하려 시도하면 에러가 발생할 것 입니다. 아래 차트가 형식을 맞추는 데 도움이 될 것입니다.
>
|문법|export 구문|import 구문|
|------|---|---|
|Default| export default function Button(){}|import Button from './button.js;|
|Named|export function Button(){}|import { Button } from './button.js';

> default import를 사용할때는, `import`다음에 아무 네이밍을 사용해도 괜찮습니다. 예를들어 `import Banana from './button.js`라고 작성할 수 있고, 같은 default export 결과를 보게 되실 겁니다. 반대로 named import에서는 네이밍은 양쪽이 서로 맞아야합니다.
이것이 named import라고 불리는 이유입니다.
> 사람들은 주로 file이 하나의 컴포넌트만 export할때  default export를 사용하고, 여러 컴포넌트와 value들을 export할 때 named export를 사용합니다. 여러분이 어떤 코딩스타일을 선호하여도, 여러분의 컴포넌트 함수들과, 이를 담고있는 파일들에 의미있는 네이밍을 해야합니다. `export default () => {}`와 같은 이름없는 컴포넌트들은 디버깅을 더 어렵게 만들기 때문에 지양해야합니다.

## 한 파일에서 여러 컴포넌트를 Importing(가져오기)과 Exporting(내보내기)하는 법

`gallery` 대신 `Profile`을 보여주고 싶다면 어떻게 하면 될까요? `Profile` 컴포넌트도 export할 수 있습니다. 하지만 `Gallery.js`는 이미 default export하고 있기 때문에 두 번의 default export를 할 수는 없습니다.
default export를 하는 새로운 파일을 만들거나, `Profile`에 named export를 추가할 수 있습니다. 하나의 파일은 오직 하나의 default export를 가질 수 있지만, named export는 여러개 가질 수 있습니다.

> default와 named export의 헷갈림을 줄이기 위해서, 어떤 팀은 하나의 스타일을 고수하거나 하나의 파일에서 혼용되는 것을 피합니다. 선호의 차이일 뿐이에요. 여러분에게 맞는 방법으로 하시면 됩니다.

먼저, `Profile`과 `Gallery.js`를 named export합니다(`default` 없이 합니다)

```js
export function Profile() {
  // ...
}
```
다음, `Gallery.js`에서 `App.js`로 `Profile`을 named import로 import합니다(중괄호 활용)

```js
import { Profile } from './Gallery.js';
```

마지막으로 `App` 컴포넌트에서 `<Profile />`를 렌더링합니다.
```js
export default function App() {
  return <Profile />;
}
```
이제 `Gallery.js`는 두 export를 가집니다
1. default `Gallery` export
2. named `Profile` export

`App.js`에 두가지 모두 import시킵니다.
`<Profile/>`을 `<Gallery/>`로 수정해보세요

[CodeSandbox](https://codesandbox.io/s/id6wg8?file=%2FApp.js&from-sandpack=true)

```js
// App.js
import Gallery from './Gallery.js';
import { Profile } from './Gallery.js';

export default function App() {
  return (
    <Profile />
  );
}
```

```js
// Gallery.js
export function Profile() {
  return (
    <img
      src="https://i.imgur.com/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}

```
![image](https://user-images.githubusercontent.com/15559593/185513571-8b8e5ea4-0416-4b93-8837-1003fa4367e5.png)

이제 여러분은 default와 named export를 함께 쓰고있습니다.

- `Gallery.js`:
  - `Profile`이름으로 `Profile` 컴포넌트를 named export 합니다.
  - `Gallery` 컴포넌트를 default export합니다.
- `App.js`:
  - `Gallery.js`에서 `Profile`을 named import합니다.
  - `Gallery`를 `Gallery.js`로부터 default import 합니다.
  - `App` 컴포넌트를 default export합니다.

## 요약

이번 페이지에서 여러분이 배운 것은 다음과 같습니다.
- 루트 컴포넌트 파일이 무엇인지
- 컴포넌트를 import, export하는 방법
- import, export 시 default vs named 구분하기
- 하나의 파일에서 여러 컴포넌트를 export 하는 방법


> ## 도전 과제
> 도전 1: 컴포넌트들을 더 많이 분리하기
> 현재, `Gallery.js`는 `Profile`과 `Gallery`를 함께 export하고 있어서 조금 헷갈리는 부분이 있습니다.

> Profile을 `Profile.js`로 옮기고, `App` 컴포넌트가 `<Profile/>`과 `<Gallery/>`를 동시에 렌더링하도록 바꿔보세요.

> 아마 `Profile`에 대해 default 혹은 named export를 사용하실텐데, `App.js`와 `Gallery.js`에 알맞은 import 문법을 활용하셔야합니다. 위의 deep dive에 있는 테이블을 참조하실 수 있습니다.

|문법|export 구문|import 구문|
|------|---|---|
|Default|` export default function Button(){}`|`import Button from './button.js;`|
|Named|`export function Button(){}`|`import { Button } from './button.js';`

[CodeSandbox](https://codesandbox.io/s/wre7jj?file=%2FGallery.js&from-sandpack=true)
```js
//App.js
import Gallery from './Gallery.js';
import { Profile } from './Gallery.js';

export default function App() {
  return (
    <div>
      <Profile />
    </div>
  );
}
```
```js
//Gallery.js
// Move me to Profile.js!
export function Profile() {
  return (
    <img
      src="https://i.imgur.com/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```
```js
//Profile.js
```
![image](https://user-images.githubusercontent.com/15559593/185513583-a09e38e8-897b-4e45-a3ab-15ce8163be37.png)


한 방식의 export 동작을 확인하고 다른방식도 동작을 확인해보세요.
