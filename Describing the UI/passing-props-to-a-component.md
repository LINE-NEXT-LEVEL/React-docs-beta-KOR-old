# 컴포넌트에 Props 넘겨주기

React 컴포넌트는 서로 소통하는데에 _props_를 사용합니다.
각 부모 컴포넌트는 props를 넘겨주는 방식으로 자식 컴포넌트에게 정보를 줄 수 있습니다. props라는 표현은 여러분이 HTML속성을 떠올리게 하겠지만, 사실 객체, 배열, 함수를 포함한 어떤 JavasScript 값들도 넘길 수 있습니다.

> **여러분이 배울 것들**
> - 컴포넌트에 props를 넘겨주는 법
> - 컴포넌트에서 props를 읽는 방법
> - props의 기본값을 설정하는 방법
> - JSX를 컴포넌트에 넘겨주는 방법
> - props가 시간 흐름에 따라 변하는 방식


## 익숙한 props
Props는 여러분이 JSX 태그로 넘길 수 있는 정보입니다. 예를들어
`className`, `src`, `alt`, `width`, `height`는 여러분이 `<img>`에 넘겨줄 수 있는 props입니다.

[CodeSandbox](https://codesandbox.io/s/5gwdmf?file=%2FApp.js&from-sandpack=true)
```js
function Avatar() {
  return (
    <img
      className="avatar"
      src="https://i.imgur.com/1bX5QH6.jpg"
      alt="Lin Lanying"
      width={100}
      height={100}
    />
  );
}

export default function Profile() {
  return (
    <Avatar />
  );
}

```
`<img>`에 전달할 수 있는 props는 미리 정해져 있습니다.(ReactDOM이 [HTML 표준](https://html.spec.whatwg.org/multipage/embedded-content.html#the-img-element)를 따릅니다.) 하지만 여러분은  `<Avatar>`와 같은 _여러분의_ 컴포넌트를 커스텀하기 위해 어떤 props라도 넘겨줄 수 있습니다. 어떻게 하는지 볼까요?

## 컴포넌트에 props 넘기기

아래 코드에서 `Profile`은 자식 컴포넌트 `Avatar`에 아무 props도 넘겨주고 있지 않습니다.
```js
export default function Profile() {
  return (
    <Avatar />
  );
}
```
여러분은 `Avatar`에 두 단계를 거쳐 props를 전달할 수 있습니다.

### Step1: 자식 컴포넌트에 props 넘기기

먼저, `Avatar`에 props를 넘겨주세요. 예를 들어 두 props `person`(객체)
과 `size`(숫자)를 넘겨봅시다.

```js
export default function Profile() {
  return (
    <Avatar
      person={{ name: 'Lin Lanying', imageId: '1bX5QH6' }}
      size={100}
    />
  );
}
```
> `person=` 다음에 있는 두개의 중괄호가 여러분을 헷갈리게 한다면,
>  JSX 중괄호 내부의 [객체일뿐](https://beta.reactjs.org/learn/javascript-in-jsx-with-curly-braces#using-double-curlies-css-and-other-objects-in-jsx)을 생각해보세요.

이제, 여러분은 `Avatar` 컴포넌트 내부에서 이 props들을 읽을 수 있습니다.

### step2: 자식 컴포넌트 내부에서 props 읽기

여러분은 `function Avatar` 바로 다음에 있는 `({`과 `})` 내부에 콤마로 구별되어 있는 `person, size` 처럼 나열하여서 props를 읽을 수 있습니다.
이로써 `Avatar` 코드 내부에서 이들을 변수처럼 활용할 수 있게됩니다.
```js
function Avatar({ person, size }) {
  // person and size are available here
}
```
`Avatar`에 `person`과 `size` props를 활용하여 렌더링될 로직을 추가하면, 다 된 것 입니다.
이제 여러분은 `Avatar`를 다른 props들로 많은 방법들로 렌더링되게 할 수 있습니다. 변수 값들을 수정해보세요!
[CodeSanbox](https://codesandbox.io/s/5x2t1l?file=/App.js&from-sandpack=true)

```js
//App.js
import { getImageUrl } from './utils.js';

function Avatar({ person, size }) {
  return (
    <img
      className="avatar"
      src={getImageUrl(person)}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}

export default function Profile() {
  return (
    <div>
      <Avatar
        size={100}
        person={{
          name: 'Katsuko Saruhashi',
          imageId: 'YfeOqp2'
        }}
      />
      <Avatar
        size={80}
        person={{
          name: 'Aklilu Lemma',
          imageId: 'OKS67lh'
        }}
      />
      <Avatar
        size={50}
        person={{
          name: 'Lin Lanying',
          imageId: '1bX5QH6'
        }}
      />
    </div>
  );
}
```
```js
//utils.js
export function getImageUrl(person, size = 's') {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    size +
    '.jpg'
  );
}
```
Props는 여러분이 부모 컴포넌트와 자식 컴포넌트를 별개로 생각할 수 있도록 해줍니다. 예를들어 여러분은 `Avatar`가 어떻게 활용하는지에 관계없이 `person` 또는 `size`를 `Profile` 내부에서 변경할 수 있습니다. 유사하게 `Profile`을 살펴보지 않고 `Avatar`가 props를 활용하는 방식을 변경할 수 있습니다.

여러분은 props를 여러분이 조정할 수 있는 "손잡이"로 생각할 수 있습니다.
function(함수)에서 arguments(인자)가 하는 역할과 같은 역할을 수행합니다.
사실, props는 여러분의 컴포넌트의 유일한 인자입니다! React 컴포넌트 함수들은 하나의 인자로 `props` 객체를 받습니다
```js
function Avatar(props) {
  let person = props.person;
  let size = props.size;
  // ...
}
```

대체로 여러분은 `props`객체 자체를 전부 필요로 하지는 않고, 분리된 props로 분해해서 활용하게 될 것입니다.

> ## 주의
> props를 선언할 때 `()`쌍 내부에 `{}`쌍을 넣는 것을 잊지마세요.
> ```js
> function Avatar({ person, size }) {
>  // ...
>}
> ```
> 이 문법은 [구조 분해 할당](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Unpacking_fields_from_objects_passed_as_a_function_parameter)이라고 불리며, 함수 파라미터에서 값들을 읽는 것과 같습니다
> ```js
>function Avatar(props) {
>  let person = props.person;
>  let size = props.size;
>  // ...
>}
> ```

## prop을 위한 기본값 설정

만약 여러분이 prop의 값이 정해지지 않았을때 기본값을 지정하고 싶다면,
구조분해할당(destructuring)을 하면서 `=`와 기본값을 파라미터 다음에 넣어주면 됩니다
```js
function Avatar({ person, size = 100 }) {
  // ...
}
```
이제 만약 `<Avatar person={...} />`이 `size` prop 없이 렌더링 된다면, `size`는 `100`으로 지정될 것 입니다.

기본 값은 `size` prop이 지정되지 않거나, 여러분이 `size={undefined}`를 넘겨줄 때만 활용됩니다. 하지만 여러분이 `size={null}`이나 `size={0}`을 넘겨준다면, 기본 값은 활용되지 않습니다

## JSX spread 구문으로 props 전달하기

가끔, props를 넘기는 것은 반복적일 수 있습니다.
```js
function Profile({ person, size, isSepia, thickBorder }) {
  return (
    <div className="card">
      <Avatar
        person={person}
        size={size}
        isSepia={isSepia}
        thickBorder={thickBorder}
      />
    </div>
  );
}
```
반복되는 코드에 잘못된 것은 없고, 오히려 더 읽기 쉬울 수 있습니다. 하지만 여러분은 간결함을 중요시 여길 수 있습니다. 몇 컴포넌트들은 `Profile`이 `Avatar`에 주는 것 처럼 자식 컴포넌트에 모든 props를 넘겨주기도 합니다.
왜냐하면 props를 직접적으로 쓰진 않더라도 spread 구문으로 간결하게 쓰는 것도 합리적일 수 있습니다
```js
function Profile(props) {
  return (
    <div className="card">
      <Avatar {...props} />
    </div>
  );
}
```
이처럼 `Profile`의 모든 props를 `Avatar`에게 각 이름들을 나열할 필요없이 넘겨줄 수 있습니다

**spread 구문을 제한적으로 활용하세요.** 모든 다른 컴포넌트에서 활용한다면 어떤 문제가 있는 것 입니다.
이는 여러분의 컴포넌트를 분리하고, JSX로 children을 넘겨줘야한다는 의미일 수 있습니다.

## JSX를 children으로 넘겨주기

브라우저 내장 태그들을 감싸는 것은 흔한일 입니다
```html
<div>
  <img />
</div>
```

가끔 여러분은 컴포넌트를 같은방식으로 감싸고 싶을 수 있습니다
```js
<Card>
  <Avatar />
</Card>
```
JSX 태그 내부에 여러분의 컨텐츠를 감싸면, 부모 컴포넌트는 그 컨텐츠를 `children`이라 불리는
prop으로 받게 됩니다. 예를들어 아래 `Card`는 `<Avatar />`를 `children` prop으로 받고, div로 감싸져 렌더링 될 것입니다.

[CodeSandbox](https://codesandbox.io/s/tx9gtr?file=/App.js&from-sandpack=true)
```js
//App.js
import Avatar from './Avatar.js';

function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

export default function Profile() {
  return (
    <Card>
      <Avatar
        size={100}
        person={{
          name: 'Katsuko Saruhashi',
          imageId: 'YfeOqp2'
        }}
      />
    </Card>
  );
}
```
```js
//Avatar.js
import { getImageUrl } from './utils.js';

export default function Avatar({ person, size }) {
  return (
    <img
      className="avatar"
      src={getImageUrl(person)}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}
```
```js
//utils.js
export function getImageUrl(person, size = 's') {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    size +
    '.jpg'
  );
}
```
`Card`컴포넌트가 아무 컨텐츠나 감쌀 수 있는지 확인하기 위해,  `<Card>` 내부의 `<Avatar>`를 아무 문자로 바꿔보세요.
내부에서 무엇이 렌더링되는지 알 필요가 없습니다. 여러분은 많은 곳에서 이 유연한 패턴을 보게 될 것입니다.

여러분은 임의의 JSX와 부모 컴포는트로 "채워지는" "빈 곳"인 `children`을 가지는 컴포넌트를 생각해볼 수 있습니다.
`children` prop을 패널, 그리드 등과 같은 시각적 포장에 활용할 수 있고, [레이아웃 컴포넌트 추출하기](https://beta.reactjs.org/learn/extracting-layout-components)에서 더 자세히 탐구할 수 있습니다.

## props가 시간 흐름에 따라 변하는 방식
아래 `Clock`컴포넌트는 부모 컴포넌트로부터 `color`와 `time` 두 props를 받습니다.(부모 컴포넌트의 코드는 아직 배우지 않은 [상태](https://beta.reactjs.org/learn/state-a-components-memory)를 활용하기 때문에 생략되었습니다.)

아래 코드에서 color를 변경해 보세요

[CodeSandbox](https://codesandbox.io/s/dk5wm7?file=/Clock.js&from-sandpack=true)
```js
//Clock.js
export default function Clock({ color, time }) {
  return (
    <h1 style={{ color: color }}>
      {time}
    </h1>
  );
}
```

이 예제는 **컴포넌트가 시간에 지남에 따라 다른 props를 받을 수 있음을 시사합니다.** Props는 고정되어 있지 않습니다.
여기에서 `time` prop는 매 초 변화하고, `color` prop은 여러분이 다른 color를 선택했을 때 변화합니다.
Props는 시작하는 순간뿐 아니라, 매 순간 컴포넌트의 데이터를 반영합니다

하지만, props는 [불변성](https://en.wikipedia.org/wiki/Immutable_object)을 가집니다.
이는 "변화할 수 없다"는 의미의 컴퓨터과학 용어입니다. 컴포넌트가 props를 변경할 필요가 있을 때(예를 들어, 유저 인터렉션이나 새 데이터에 응답할 때),
부모 컴포넌트에게 _다른 props(새 객체)_ 를 달라고 "요청"해야할 것입니다. 기존 props는 사라지고, JavaScript 엔진은 해당 props의 메모리도 회수합니다.

**"props 변경"을 시도하지 마세요** 유저 입력(color 선택 변경과 같이)에 응답해야할 때
여러분은 [상태: 컴포넌트의 메모리](https://beta.reactjs.org/learn/state-a-components-memory)에서 배울 수 있는"set state"가 필요합니다.

## 요약
- props를 전달하기 위해서는, HTML 속성처럼 JSX에 추가하세요.
- props를 읽기 위해서는 `function Avatar({person, size})` 구조 분해 할당(destructuring) 구문을 활용하세요.
- 지정되지 않거나, undefined인 props에 활용되는 기본 값을 `size = 100`과 같이 지정할 수 있습니다.
- `<Avatar {...pops}>`와 같은 JSX spread 구문으로 모든 props를 넘길 수 있지만, 너무 많이 쓰지는 마세요.
- `<Card><Avatar /></Card>`와 같은 중첩 JSX는 `Card`컴포넌트의 `children` prop으로 표현될 수 있습니다.
- props는 순간의 읽기전용 스냅샷입니다. 매 렌더링마다 새 props를 받아오게 됩니다.
- 여러분은 props를 변경할 수 없습니다. 상호작용이 필요할때는 set state가 필요합니다.

## 도전과제

1. 컴포넌트 추출하기

  이 `Gallery`컴포넌트는 거의 유사한 두 프로필을 담고있습니다.
  `Profile` 컴포넌트를 추출하고 반복을 줄여보세요. 여러분은 어떤 props를 넘길지 결정해야 합니다.

  [CodeSandbox](https://codesandbox.io/s/dh3v4z?file=%2FApp.js&from-sandpack=true)

  ```js
  //App.js
  import { getImageUrl } from './utils.js';

export default function Gallery() {
  return (
    <div>
      <h1>Notable Scientists</h1>
      <section className="profile">
        <h2>Maria Skłodowska-Curie</h2>
        <img
          className="avatar"
          src={getImageUrl('szV5sdG')}
          alt="Maria Skłodowska-Curie"
          width={70}
          height={70}
        />
        <ul>
          <li>
            <b>Profession: </b>
            physicist and chemist
          </li>
          <li>
            <b>Awards: 4 </b>
            (Nobel Prize in Physics, Nobel Prize in Chemistry, Davy Medal, Matteucci Medal)
          </li>
          <li>
            <b>Discovered: </b>
            polonium (element)
          </li>
        </ul>
      </section>
      <section className="profile">
        <h2>Katsuko Saruhashi</h2>
        <img
          className="avatar"
          src={getImageUrl('YfeOqp2')}
          alt="Katsuko Saruhashi"
          width={70}
          height={70}
        />
        <ul>
          <li>
            <b>Profession: </b>
            geochemist
          </li>
          <li>
            <b>Awards: 2 </b>
            (Miyake Prize for geochemistry, Tanaka Prize)
          </li>
          <li>
            <b>Discovered: </b>
            a method for measuring carbon dioxide in seawater
          </li>
        </ul>
      </section>
    </div>
  );
}
  ```
  ```js
  //utils.js
  export function getImageUrl(imageId, size = 's') {
  return (
    'https://i.imgur.com/' +
    imageId +
    size +
    '.jpg'
  );
}

  ```

2. props로 이미지 사이즈 관리하기

  이 예제에서, `Avatar`는 `<img>`의 가로와 높이를 결정하는 `size` prop을 받습니다. `size` prop은 예제에서 `40`으로 설정되어 있습니다.
  하지만 새로운 탭에서 이미지를 열어보면 이미지가 더 큰 것을 알 수 있습니다(`160`픽셀). 이미지의 진짜 크기는 여러분이 요청하는 썸네일 크기로 결정됩니다.
  `Avatar` 컴포넌트에서, `size` prop에 기반하여 가장 가까운 이미지 크기를 요청하도록 변경해보세요. `size`가 `90`보다 작으면 `getImageURL` 함수에 `b`(big)보다 `s`(small)을 요청하는 것처럼 하시면 됩니다. `size` prop을 변경하고 새 탭에서 이미지를 열어보면서 여러분의 변경 사항이 잘 동작하는지 확인해보세요.

  [CodeSandbox](https://codesandbox.io/s/spzgh1?file=/App.js&from-sandpack=true)
  ```js
  //App.js
  import { getImageUrl } from './utils.js';

function Avatar({ person, size }) {
  return (
    <img
      className="avatar"
      src={getImageUrl(person, 'b')}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}

export default function Profile() {
  return (
    <Avatar
      size={40}
      person={{
        name: 'Gregorio Y. Zara',
        imageId: '7vQD0fP'
      }}
    />
  );
}
```
```js
//utils.js
export function getImageUrl(person, size) {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    size +
    '.jpg'
  );
}
```

3. children prop의 JSX 넘기기

아래 마크업에서 `Card` 컴포넌트를 추출하고, `children` prop이 다른 JSX를 넘기도록 활용해보세요

[CodeSandbox](https://codesandbox.io/s/xtn0d0?file=/App.js&from-sandpack=true)
```js
//App.js
export default function Profile() {
  return (
    <div>
      <div className="card">
        <div className="card-content">
          <h1>Photo</h1>
          <img
            className="avatar"
            src="https://i.imgur.com/OKS67lhm.jpg"
            alt="Aklilu Lemma"
            width={70}
            height={70}
          />
        </div>
      </div>
      <div className="card">
        <div className="card-content">
          <h1>About</h1>
          <p>Aklilu Lemma was a distinguished Ethiopian scientist who discovered a natural treatment to schistosomiasis.</p>
        </div>
      </div>
    </div>
  );
}
```