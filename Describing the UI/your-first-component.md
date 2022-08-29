# 여러분의 첫번째 컴포넌트

컴포넌트는 React의 핵심 개념들 중 하나입니다. 컴포넌트는 사용자 인터페이스(UI)를 구축하는 토대로 React를 공부하는 데 적절한 시작점입니다!

> 이 단원에서 다룰 것들
>
> - 컴포넌트는 무엇인지
> - React 앱에서 컴포넌트의 역할이 무엇인지
> - React 컴포넌트를 만드는 방법

## 컴포넌트 : UI를 만드는 블록들

웹에서 HTML로 `<h1>`과 `<li>`와 같은 내장되어 있는 태그들로 다양한 구조의 document를 만들 수 있습니다.

```HTML
<article>
  <h1>My First Component</h1>
  <ol>
    <li>Components: UI Building Blocks</li>
    <li>Defining a Component</li>
    <li>Using a Component</li>
  </ol>
</article>
```

이 마크업은 `<article>`로 기사를, `<h1>`으로 제목을, `<ol>`로 (축약된) 목차(정렬된 목록)를 표현하고 있습니다. 이와 같은 마크업은 스타일을 위한 CSS와 상호작용을 위한 JavaScript와 함께 섞여서 sidebar, avatar, modal, dropdown과 같은 웹에서 보이는 모든 UI 요소에 사용됩니다.

React는 마크업, CSS, JavaScript 모두를 앱에서 재사용 가능한 UI요소인 custom component 속에서 합칩니다. 위에서 본 목차 코드는 `<TableOfContents />`로 변환되어 모든 페이지에서 render하게 만들 수 있습니다. 숨겨진 내부에서는 `<article>`, `<h1>`과 같은 HTML 태그들이 똑같이 사용되고 있습니다.

HTML 태그와 같이, 여러분은 모든 페이지를 디자인하는 데 컴포넌트들을 합성하고, 정렬하고 중첩할 수 있습니다. 예를 들어, 여러분이 읽고 있는 문서는 React 컴포넌트로 아래와 같이 이루어져 있습니다:

```JSX
<PageLayout>
  <NavigationHeader>
    <SearchBar />
    <Link to="/docs">Docs</Link>
  </NavigationHeader>
  <Sidebar />
  <PageContent>
    <TableOfContents />
    <DocumentationText />
  </PageContent>
</PageLayout>
```

프로젝트가 커질수록 디자인의 많은 부분들이 이미 작성한 컴포넌트를 재사용해서 만들 수 있다는 것과 이것이 개발을 빠르게 만든다는 것을 알아차릴 것입니다. 위에서 작성한 목차는 `<TableOfContents />`로 어느 화면에서든 추가될 수 있습니다! 여러분은 [Chakra UI](https://chakra-ui.com/)와 [Material UI](https://mui.com/)와 같은 React open source 커뮤니티에서 공유되는 수천개의 컴포넌트들로 프로젝트를 빠르게 시작할 수 있습니다.

## 컴포넌트를 정의하기

전통적으로 웹페이지를 만들 때, 웹 개발자들은 내용물을 marked up한 뒤 JavaScript를 첨가하여 상호작용을 추가했습니다. 웹에서 상호작용이 보조적인 요소일 때 이런 방식이 잘 작동했습니다. 지금은 많은 사이트와 모든 앱에서 상호작용이 기대되고 있습니다. React는 같은 기술을 여전히 사용하지만 상호작용을 첫번째로 넣습니다: React 컴포넌트는 마크업을 첨가하는 JavaScript 함수입니다. 아래 예시가 어떻게 보이시나요([code sandbox](https://codesandbox.io/s/wn5or1?file=%2FApp.js&from-sandpack=true)에서 아래 예시를 수정할 수 있습니다):

```JavaScript
// App.js

export default function Profile() {
  return (
    <img
      src="https://i.imgur.com/MK3eW3Am.jpg"
      alt="Katherine Johnson"
    />
  )
}
```

![image](https://user-images.githubusercontent.com/55529617/186284397-4d89e0cb-9a66-4ccb-a3c5-9393fbfc713a.png)

여기 컴포넌트를 만드는 방법이 있습니다:

### 단계 1: 컴포넌트를 export하세요

`export default` 접두사는 [표준 Javascript 문법](https://developer.mozilla.org/ko/docs/web/javascript/reference/statements/export)입니다(React에서만 사용되는 특징은 아닙니다). `export default`는 파일 속 핵심 함수를 표시하고 다른 파일에서 그 함수를 import 할 수 있게 만듭니다.( [Importing and Exporting Components](https://beta.reactjs.org/learn/importing-and-exporting-components)에서 더 importing에 대해서 더 배우실 수 있습니다!)

### 단계 2: 함수를 정의하세요

`function Profile() { }`로 여러분은 `Profile`이란 이름의 JavaScript 함수를 정의할 수 있습니다.

> **경고**
> React 컴포넌트는 정규 JavaScript 함수이지만 컴포넌트의 이름은 대문자로 무조건 시작해야 합니다, 그렇지 않으면 컴포넌트가 동작하지 않습니다.

### 단계 3: 마크업을 추가하세요

컴포넌트는 `src`과 `alt` 속성을 가진 `<img />`를 반환합니다. `<img />`는 HTML로 작성된 것처럼 보이지만 실제로 그 내부에서는 JavaScript로 쓰여져 있습니다! 이러한 문법을 [JSX](https://beta.reactjs.org/learn/writing-markup-with-jsx)라 부르며 JavaScript 안에 마크업을 넣는 것을 가능하게 만듭니다.

아래 컴포넌트와 같은 경우 반환 문구는 한 줄에 쓰일 수 있습니다:

```JSX
return <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />;
```

하지만 마크업이 `return` 단어와 같은 라인에 모두 있을 수 없다면, 소괄호로 마크업을 아래와 같이 감싸야 합니다:

```JSX
return (
  <div>
    <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
  </div>
);
```

> **경고**
> 소괄호가 없다면 `return` 이후에 나오는 여러 라인의 코드들은 [무시](https://stackoverflow.com/questions/2846283/what-are-the-rules-for-javascripts-automatic-semicolon-insertion-asi)됩니다!

## 컴포넌트 사용하기

`Profile` 컴포넌트를 정의했으므로 다른 컴포넌트 속에 이 컴포넌트를 넣을 수 있습니다. 예를 들어, 여러 개의 `Profile` 컴포넌트들이 들어간 Gallery 컴포넌트를 export 할 수 있습니다.

```JavaScript
// App.js

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

![image](https://user-images.githubusercontent.com/55529617/186284459-a7470994-9997-4331-aba8-aee35d92ba95.png)

### 브라우저가 바라보는 것

경우에 따라 차이가 있다는 것을 알아야 합니다:

- `<section>`은 소문자이며 React는 여러분이 HTML 태그로 사용하려 한다는 것을 알고 있습니다.
- `<Profile />`은 대문자 `P`로 시작하며 React는 여러분이 `Profile`이라 불리는 컴포넌트를 사용하려 한다는 것을 알고 있습니다.

그리고 `Profile`은 더 많은 HTML을 포함하고 있습니다:`<img />`. 결론적으로, 아래가 브라우저가 바라보는 것입니다:

```HTML
<section>
  <h1>Amazing scientists</h1>
  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
  <img src="https://i.imgur.com/MK3eW3As.jpg" alt="Katherine Johnson" />
</section>
```

### 컴포넌트를 중첩하고 구성하기

컴포넌트는 정규 JavaScript 함수이기 때문에 같은 파일에서 여러 개의 컴포넌트들이 있을 수 있습니다. 컴포넌트들이 서로 강하게 관련있거나 상대적으로 작을 때 편리합니다. 이러한 파일이 번잡해지면 여러분은 분리된 파일로 `Profile`을 옮겨야 합니다. [imports에 관한 문서](https://beta.reactjs.org/learn/importing-and-exporting-components)에서 방법을 짧게 배울 수 있습니다.

`Profile`컴포넌트는 `Gallery` 속에서 렌더링되기 때문에 `Gallery`는 **부모 컴포넌트**이며 각각의 `Profile`은 "자식"이라 부를 수 있습니다. React의 마법과 같은 부분입니다: 여러분은 컴포넌트를 한 번만 정의한 뒤 원하는 만큼 여러 번 여러 장소에서 그 컴포넌트를 사용할 수 있습니다.

> **깊이 파고들기**
>
> ## Components All the Way Down

## 요약

React의 첫 단계를 완수했습니다! 핵심 요소들을 요약해 봅시다!

- React는 **앱의 재사용 가능한 UI 요소들**인 컴포넌트를 만듭니다.
- React 앱에서 UI의 모든 부분은 컴포넌트입니다.
- React 컴포넌트는 아래 내용들만 제외하면 정규 JavaScript 함수와 같습니다;
  - 이름이 대문자로 시작합니다
  - JSX 마크업을 반환합니다

> ## 도전 과제
>
> ### 도전 1: 컴포넌트 export하기
>
> **도전 1: 컴포넌트 export하기**
> root 컴포넌트가 export되지 않았기 때문에 [code sandbox](https://codesandbox.io/s/pb3f9q?file=%2FApp.js&from-sandpack=true)는 작동하지 않습니다:

([code sandbox](https://codesandbox.io/s/pb3f9q?file=%2FApp.js&from-sandpack=true)에서 직접 코드를 작성할 수 있습니다.)

```JavaScript
// App.js

function Profile() {
  return (
    <img
      src="https://i.imgur.com/lICfvbD.jpg"
      alt="Aklilu Lemma"
    />
  );
}
```

![image](https://user-images.githubusercontent.com/55529617/186284515-b495cfb0-14f9-4f11-adc3-1cfbca5fea78.png)

> 해결방안을 보기 전에 스스로 고쳐보세요!

> **정답**
> `export default`를 아래 코드와 같이 함수 정의 앞에 추가합니다:
> `export`만 쓰는 것으로 이 예제가 고쳐지지 않는 이유를 궁금해할 수도 있습니다. `export`와 `export default` 사이에 차이를 [Importing and Exporting Components](https://beta.reactjs.org/learn/importing-and-exporting-components)에서 배울 수 있습니다.

([code sandbox](https://codesandbox.io/s/1q1644?file=%2FApp.js&from-sandpack=true)에서 정답을 확인할 수 있습니다.)

```JavaScript
// App.js

export default function Profile() {
  return (
    <img
      src="https://i.imgur.com/lICfvbD.jpg"
      alt="Aklilu Lemma"
    />
  );
}

```

![image](https://user-images.githubusercontent.com/55529617/186284550-5cc16f17-8b9e-4edc-999c-4fe4cb6faa6a.png)

> ### 도전 2: 반환 문구를 수정하기
>
> ***도전 2: 반환 문구를 수정하기***
> `return` 문구에서 바르지 않은 것이 있습니다. 수정해보세요.

([code sandbox](https://codesandbox.io/s/com4oq?file=%2FApp.js&from-sandpack=true)에서 직접 코드를 작성할 수 있습니다.)

```JavaScript
// App.js
export default function Profile() {
  return
    <img src="https://i.imgur.com/jA8hHMpm.jpg" alt="Katsuko Saruhashi" />;
}

```

![image](https://user-images.githubusercontent.com/55529617/186284588-571505a9-1d73-4cd1-98f4-5167700ff124.png)

> **정답**
> 아래 코드와 같이 return 문구를 한 라인에 있도록 옮기면 컴포넌트가 동작합니다.

([code sandbox](https://codesandbox.io/s/838hye?file=%2FApp.js&from-sandpack=true)에서 정답을 확인할 수 있습니다.)

```JavaScript
// App.js

export default function Profile() {
  return <img src="https://i.imgur.com/jA8hHMpm.jpg" alt="Katsuko Saruhashi" />;
}
```

![image](https://user-images.githubusercontent.com/55529617/186284612-b6fa5e12-2880-48f5-a065-4b588216679f.png)

> 또는 `return` 바로 뒤에 소괄호를 열어서 JSX 마크업을 감싸면 됩니다.

([code sandbox](https://codesandbox.io/s/vq3fi6?file=%2FApp.js&from-sandpack=true)에서 정답을 확인할 수 있습니다.)

```JavaScript
// App.js

export default function Profile() {
  return (
    <img 
      src="https://i.imgur.com/jA8hHMpm.jpg" 
      alt="Katsuko Saruhashi" 
    />
  );
}
```

![image](https://user-images.githubusercontent.com/55529617/186284612-b6fa5e12-2880-48f5-a065-4b588216679f.png)

> ### 도전 3: 실수 찾기
>
> **도전 3: 실수 찾기**
> `Profile` 컴포넌트가 선언되고 사용되는 방식에 문제가 있습니다. 실수를 찾아보세요. (React가 HTML 태그와 컴포넌트를 구분하는 방법을 기억해보세요!)

([code sandbox](https://codesandbox.io/s/dphpgc?file=%2FApp.js&from-sandpack=true)에서 직접 코드를 작성할 수 있습니다.)

```JavaScript
// App.js

function profile() {
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
      <profile />
      <profile />
      <profile />
    </section>
  );
}

```

![image](https://user-images.githubusercontent.com/55529617/186284654-19460117-ce45-436a-90f1-d5cc654ec52c.png)

> **정답**
> React 컴포넌트 이름은 대문자로 시작해야 합니다.
> `function profile()`을 `function Profile()`로 바꾸고 모든 `<profile />`을 `<Profile />`로 바꾸세요:

([code sandbox](https://codesandbox.io/s/zzszdd?file=%2FApp.js&from-sandpack=true)에서 정답을 확인할 수 있습니다.)

```JavaScript
// App.js

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

![image](https://user-images.githubusercontent.com/55529617/186284688-46c310e5-0806-4a1a-9f8c-e572d7a9291f.png)

> ### 도전 4: 여러분만의 컴포넌트
>
> **도전 4: 여러분만의 컴포넌트**
> 컴포넌트를 처음부터 작성해 보세요. 컴포넌트에 적당한 이름을 짓고 마크업을 반환하세요. 만약 생각나는 게 없다면, `<h1>Good job!</h1>`을 보여주는 `Congratulations` 컴포넌트를 작성하세요. 컴포넌트를 export하는 것을 잊지마세요!

([code sandbox](https://codesandbox.io/s/lg4tki?file=/App.js&from-sandpack=true)에서 직접 코드를 작성할 수 있습니다.)

```JavaScript
// App.js
// Write your component below!
```

![image](https://user-images.githubusercontent.com/55529617/186284749-02872c3c-64c0-4b85-90f3-6ca9b555b4bd.png)

> **정답**

([code sandbox](https://codesandbox.io/s/xp5l9t?file=%2FApp.js&from-sandpack=true)에서 정답을 확인할 수 있습니다.)

```JavaScript
// App.js
export default function Congratulations() {
  return (
    <h1>Good job!</h1>
  );
}
```

![image](https://user-images.githubusercontent.com/55529617/186284795-977c33a8-173b-4d97-8d04-e2b1ebafadfe.png)
