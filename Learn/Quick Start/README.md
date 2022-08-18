# Quick start
### React 문서에 오신걸 환영합니다! 여러분은 이 페이지에서 일상적으로 사용하게 될 React 개념들의 80%를 소개받을 것입니다. 

> ### 여러분이 배울 것들
> * component들을 만들고 중첩하는 방법
> * markup과 style을 추가하는 방법
> * 데이터를 보여주는 방법
> * 조건과 리스트들을 렌더링하는 방법
> * 이벤트에 반응하고 화면을 업데이트하는 방법
> * component 간에 데이터를 공유하는 방법

## Component들을 만들고 중첩하는 방법

React 앱들은 컴포넌트들로 만들어집니다. 하나의 컴포넌트는 고유의 논리와 모양을 가지고 있는 UI(user interface) 한 조각입니다.
한 컴포넌트는 버튼만큼 작을 수도 있고, 전체 페이지만큼 클 수도 있습니다.

React component들은 markup을 리턴하는 Javascript 함수들입니다. 

```javascript
function MyButton() {
  return (
    <button>I'm a button</button>
  );
}
```
`MyButton`이라는 컴포넌트를 선언했습니다. 이 컴포넌트를 다른 컴포넌트 안에 중첩할 수 있습니다.
```javascript
export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```
`<MyButton/>`이 대문자로 시작하는 것을 확인해 보세요. 대문자로 시작한다는 것은 <MyButton/>이 React component라는 것을 알려줍니다.
React component들의 이름은 항상 대문자로 시작합니다. 반면에, HTML 태그들은 반드시 소문자로 시작해야 합니다.

결과물:
```javascript 
//App.js

function MyButton() {
  return (
    <button>
      I'm a button
    </button>
  );
}

export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```
`export default` 키워드는 해당 파일의 메인 component를 명시합니다. 
Javascript 문법에 익숙하지 않다면, [MDN](https://developer.mozilla.org/en-US/docs/web/javascript/reference/statements/export)이나 [javascript.info](https://javascript.info/import-export) 가 좋은 참고자료가 됩니다. 

## JSX로 markup 쓰기

위에서 본 markup문은 JSX라고 부릅니다. 선택사항이지만, 대부분의 React 프로젝트들은 편의를 위해 JSX를 사용합니다.
[local에서의 개발을 위해 추천하는 도구들](https://beta.reactjs.org/learn/installation) 모두 위 박스의 JSX를 지원합니다.

JSX는 HTML보다 더 엄격합니다. `<br/>`처럼 태그를 닫아줘야합니다. 또, component는 여러개의 JSX태그를 return 할 수 없습니다.
여러개의 JSX태그를 return 하기 위해서는 하나의 부모 태그로 감싸야합니다. `<div>...</div>` 나 `<>...</>` 처럼 빈 태그를 이용해서 감싸주어야 합니다.
```javascript
function AboutPage() {
  return (
    <>
      <h1>About</h1>
      <p>Hello there.<br />How do you do?</p>
    </>
  );
}
```
JSX로 변경해야 하는 HTML이 많다면, [온라인 변환기](https://transform.tools/html-to-jsx)를 사용할 수 있습니다.

## 스타일 추가하기
react에서는 `css class`를 명시하기 위해 className을 사용합니다. 동작하는 방식은 HTML의 `class` 속성과 같습니다.
```javascript
<img className="avatar" />
```
그리고 나서 분리된 CSS파일에 CSS규칙들을 적습니다.
```css
/* In your CSS */
.avatar {
  border-radius: 50%;
}
```
React는 CSS파일을 추가하는 방식을 미리 정해놓지 않았습니다. 가장 간단한 방법으로는 HTML에 `<link>`태그를 추가하는 것입니다.
만약 빌드 도구나 프레임워크를 사용한다면, 문서를 확인해서 CSS파일을 프로젝트에 추가하는 방법을 배우세요.

## 데이터 보여주기
JSX는 JavaScript에 markup를 넣도록 해줍니다. 중괄호 `{}` 를 사용하면 JavaScript로 "탈출"할 수 있기 때문에 코드의 몇몇 변수를 심어놓고 그 데이터를 사용자에게 보여줄 수 있습니다.
예를 들어, 다음 코드는 `user.name`을 보여줍니다.
```javascript
return (
  <h1>
    {user.name}
  </h1>
);
```
JSX속성에서 "JavaScript로 탈출"하는 것도 가능합니다. 하지만 따옴표 _대신에_ 중괄호를 사용해야 합니다. 
예를 들어, `className=""avatar"`는 `"avatar"` 문자열을 CSS class로 전달합니다.
하지만 `src={user.imageUrl}` 은 Javascript의 `user.imageUrl` 의 변수 값을 읽고, 그 값을 `src` 속성으로 전달합니다.
```javascript
return (
  <img
    className="avatar"
    src={user.imageUrl}
  />
);
```
JSX 중괄호 안에 더 복잡한 표현들을 넣을 수도 있습니다. 여기 [문자열 연결 ](https://javascript.info/operators#string-concatenation-with-binary)예시가 있습니다.
```javascript
//App.js
const user = {
  name: 'Hedy Lamarr',
  imageUrl: 'https://i.imgur.com/yXOvdOSs.jpg',
  imageSize: 90,
};

export default function Profile() {
  return (
    <>
      <h1>{user.name}</h1>
      <img
        className="avatar"
        src={user.imageUrl}
        alt={'Photo of ' + user.name}
        style={{
          width: user.imageSize,
          height: user.imageSize
        }}
      />
    </>
  );
}
```
위의 예시에서, `style={{}}`은 특별한 구문이 아니고, 일반적인 `{}` 객체를 JSX 중괄호 `style={ }` 안에 넣은 것입니다. 
JavaScript 변수들에 의존하는 style을 사용할 때 `style` 속성을 사용할 수 있습니다.

## 조건적으로 렌더링하기
React 에서, 조건을 사용하기 위한 특별한 구문이 따로 있는 것은 아닙니다. 일반적인 JavaScript 코드에서 써왔던 같은 기술을 사용하면 됩니다.
예를 들면, JSX를 조건적으로 포함하기 위해서 if 를 사용하면 됩니다.
```javascript
let content;
if (isLoggedIn) {
  content = <AdminPanel />;
} else {
  content = <LoginForm />;
}
return (
  <div>
    {content}
  </div>
);
```
좀더 작은 코드를 선호한다면, [조건자 `?`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) 를 사용할 수 있습니다. `if` 와 달리 `?` 는 JSX 안에서 동작합니다.
```javascript
<div>
  {isLoggedIn ? (
    <AdminPanel />
  ) : (
    <LoginForm />
  )}
</div>
```
`else` 구문이 따로 필요 없다면, [논리 연산자 `&&`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND#short-circuit_evaluation) 를 사용해서 더 짧게 만들 수 있습니다.
```javascript
<div>
  {isLoggedIn && <AdminPanel />}
</div>
```
위 셋 모두 조건부로 상태를 표시해줍니다. 이런 JavaScript 구문에 익숙하지 않으 항상 `if...else`를 사용하는 것으로 시작할 수 있습니다.

## List 렌더링하기 
컴포넌트 리스트를 렌더링하기 위해서 `for` 반복문이나 [배열의 `map()`함수](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)와 같은 JavaScript 기능들을 사용하게 될 겁니다.
상품이 담긴 배열로 예를 들어보겠습니다.

```javascript
const products = [
  { title: 'Cabbage', id: 1 },
  { title: 'Garlic', id: 2 },
  { title: 'Apple', id: 3 },
];
```
`map()` 함수를 사용해서 상품 배열을 `<li>` 아이템 배열로 변환하고, component 안에 넣습니다.
```javascript
const listItems = products.map(product =>
  <li key={product.id}>
    {product.title}
  </li>
);

return (
  <ul>{listItems}</ul>
);
```
`<li>`가 `key` 속성을 가진다는 것을 확인하세요. 동일한 레벨에 있는 아이템들을 식별하기 위해서는 리스트에 있는 각 아이템마다 문자열이나 숫자를 넘겨줘야합니다. 보통, key는 데이터베이스 ID와 같이 데이터에서 와야합니다. 나중에 아이템들을 새로 삽입하거나, 삭제하거나 재배치할 때 React가 그 과정을 이해하기 위해서는 key가 필요합니다.
```javascript
//App.js
const products = [
  { title: 'Cabbage', isFruit: false, id: 1 },
  { title: 'Garlic', isFruit: false, id: 2 },
  { title: 'Apple', isFruit: true, id: 3 },
];

export default function ShoppingList() {
  const listItems = products.map(product =>
    <li
      key={product.id}
      style={{
        color: product.isFruit ? 'magenta' : 'darkgreen'
      }}
    >
      {product.title}
    </li>
  );

  return (
    <ul>{listItems}</ul>
  );
}
```

## 이벤트에 반응하기
component안에 _이벤트 핸들러_ 함수를 선언해서 이벤트에 반응하게 할 수 있습니다.
```javascript
function MyButton() {
  function handleClick() {
    alert('You clicked me!');
  }

  return (
    <button onClick={handleClick}>
      Click me
    </button>
  );
}
```
`onClick={handleClick}`은 끝에 괄호가 없습니다! 이벤트 핸들러 함수를 _부르지_ 마세요. 이벤트 핸들러 함수를 아래로 전달해주기만 하면 됩니다.
사용자가 버튼을 클릭할 때 React가 이벤트 함수를 부를거에요. 

## 화면 업데이트하기
당신은 component가 몇몇 정보를 "기억"하고 그 정보를 보여주기를 원할 겁니다. 예를 들면, 버튼이 클릭된 횟수를 세길 원할 수도 있습니다.
이렇게 하기 위해서는 component에 _상태_를 추가하면 됩니다.

먼저, React에서 `useState`를 가져와 봅시다.
```javascript
import { useState } from 'react';
```
이제 component 안에 _상태 변수_ 를 선언할 수 있습니다.
```javascript
function MyButton() {
  const [count, setCount] = useState(0);
```
`useState`에서 두가지 정보를 가져올 수  있습니다. 현재 상태(`count`)와 그 상태를 업데이트할 수 있는 (`setCount`)입니다.
아무 이름이나 줄 수 있지만, `[something, setSomething]` 처럼 부르는 관습이 있습니다.

`useState()`에 `0`을 넘겨주었기 때문에 처음 버튼이 보여질 때는 `count`가 `0`이 될 것입니다.
상태를 변경하고 싶으면 `setCount()`를 부르고 새로운 값을 함수에 넘겨주면 됩니다. 그러면 버튼을 클릭할 때마다 클릭횟수가 늘어납니다.
```javascript
function MyButton() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <button onClick={handleClick}>
      Clicked {count} times
    </button>
  );
}
```
React는 다시 component 함수를 부릅니다. 이번에는` count`가 `1`이 되고, 그 다음에 부르면 클릭 횟수가 `2`로 변할 것입니다.
같은 component를 여러번 렌더링하고 싶다면, 각 컴포넌트들이 각자만의 상태를 갖고 있으면 됩니다. 
```javascript
//App.js
import { useState } from 'react';

function MyButton() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <button onClick={handleClick}>
      Clicked {count} times
    </button>
  );
}
```

