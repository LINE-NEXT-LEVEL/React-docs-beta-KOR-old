# JSX로 마크업 작성하기

_JSX_ 는 JavaScript 파일 안에서 HTML 같은 마크업을 작성하게 해주는 JavaScript를 위한 구문 확장자입니다. 컴포넌트를 쓰는 다른 방법들이 있지만, 대부분의 React 개발자들은 JSX의 간결함을 선호하고, 대부분의 기존 코드들도 JSX를 사용합니다. 

> **이런 것들을 배웁니다.**
> - React가 렌더링 로직과 마크업을 섞는 이유
> - JSX가 HTML과 다른 점
> - JSX로 정보를 표현하는 방법

## JSX: JavaScript안에 마크업을 넣기
웹은 HTML, CSS, JavaScript로 만들어져왔습니다. 수년간 웹 개발자들은 HTML 안에 내용, CSS안에는 디자인, JavaScript 안에는 로직을 넣었습니다. 종종 분리된 파일로도 작성했습니다. 페이지의 로직이 JavaScript에 분리되어 실행되는 동안 콘텐츠는 HTML에서 마크업 됩니다. 

<img width="769" alt="스크린샷 2022-09-06 오후 11 55 50" src="https://user-images.githubusercontent.com/52595663/188667915-478abf86-0637-48d3-b8ef-78af6c700f30.png">

하지만 웹은 더 인터랙티브해졌고, 로직이 컨텐츠를 결정하는 일이 많아지면서 JavaScript가 HTML을 담당하게 되었습니다. 그래서 **React에서는 렌더링 로직과 마크업이 컴포넌트로 같은 위치에 있게 되었습니다.-이것을 컴포넌트라 합니다.** 

<img width="774" alt="스크린샷 2022-09-06 오후 11 56 19" src="https://user-images.githubusercontent.com/52595663/188668013-856d9808-00d7-45e2-9d42-2cd19fe787b5.png">

버튼의 렌더링 로직과 마크업을 같이 유지하면 서로가 수정될 때 확실하게 동기화되도록 해줍니다. 반대로, 버튼의 마크업이나 사이드바의 마크업 같이 서로 관계 없는 구체적인 부분은 완전히 분리되어서 각각을 수정하는게 더 안전합니다.

각 React 컴포넌트는 브라우저로 렌더링하는 마크업 구문들을 포함할 수 있는 JavaScript 함수입니다. React 컴포넌트는 마크업을 표현하기 위한 JSX라고 불리는 구문 확장자를 사용합니다. JSX는 HTML과 비슷해 보이지만 조금 더 엄격하고 동적인 정보를 표현할 수 있습니다. JSX의 특성을 이해하는 가장 좋은 방법은 몇 가지 HTML을 JSX 마크업으로 변환해보는 것입니다 .

> **노트**
> [JSX와 React](https://beta.reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform#whats-a-jsx-transform)는 분리해서 사용할 수 있는 두 가지 분리된 개념입니다.

## HTML을 JSX로 변환하기

(완벽한 문법의)HTML이 있다고 가정해 봅시다:

```HTML
<h1>Hedy Lamarr's Todos</h1>
<img 
  src="https://i.imgur.com/yXOvdOSs.jpg" 
  alt="Hedy Lamarr" 
  class="photo"
>
<ul>
    <li>Invent new traffic lights
    <li>Rehearse a movie scene
    <li>Improve the spectrum technology
</ul>
```

그리고 이 HTML을 컴포넌트에 넣어보려고 합니다:

```javascript
export default function TodoList() {
  return (
    // ???
  )
}
```

그래도 복사해서 컴포넌트에 붙여넣기하면, 제대로 동작하지 않습니다:

```javascript

//App.js
export default function TodoList() {
  return (
    // This doesn't quite work!
    <h1>Hedy Lamarr's Todos</h1>
    <img 
      src="https://i.imgur.com/yXOvdOSs.jpg" 
      alt="Hedy Lamarr" 
      class="photo"
    >
    <ul>
      <li>Invent new traffic lights
      <li>Rehearse a movie scene
      <li>Improve the spectrum technology
    </ul>
  );
}
```
<img width="524" alt="스크린샷 2022-09-06 오후 11 56 46" src="https://user-images.githubusercontent.com/52595663/188668134-ddfe697d-7a0c-4001-918a-ccc2eed7c6f2.png">

[CodeSandbox](https://codesandbox.io/s/o7zoc2?file=%2FApp.js&from-sandpack=true)
제대로 실행이 안되는 이유는 JSX가 HTML보다 더 엄격하고 몇 가지 규칙이 더 있기 때문입니다. 위에 에러 메세지를 읽어보면, 마크업을 고칠 수 있는 방법이 나와있습니다. 또는 아래에 가이드를 따라가면서 수정해볼 수 있습니다.

> **노트**
> 대부분 React는 문제가 어디인지 알려주는 에러 메세지를 띄울 것입니다. 하다가 막히면 에러메세지를 읽어보세요!

## JSX 규칙들

### 1. 하나의 root element를 리턴해주자

컴포넌트에서 여러개의 element를 돌려주려면 하나의 부모 태그로 감싸줘야합니다. 
예를 들어, `<div>`를 감싸주는 태그로 사용해볼 수 있습니다:

```javascript
<div>
  <h1>Hedy Lamarr's Todos</h1>
  <img 
    src="https://i.imgur.com/yXOvdOSs.jpg" 
    alt="Hedy Lamarr" 
    class="photo"
  >
  <ul>
    ...
  </ul>
</div>
```

만약 추가로 `<div>`를 넣고 싶지 않으면 `<>`와`</>`를 대신 사용하면 됩니다:

```javascript
<>
  <h1>Hedy Lamarr's Todos</h1>
  <img 
    src="https://i.imgur.com/yXOvdOSs.jpg" 
    alt="Hedy Lamarr" 
    class="photo"
  >
  <ul>
    ...
  </ul>
</>
```

빈 태그는 [React fragment](https://beta.reactjs.org/learn/TODO)라고 부릅니다. React fragment는 브라우저의 HTML 트리에서 어떤 흔적을 남기지 않고 태그들을 그룹화하게 도와줍니다.

> DEEP DIVE
> **여러 개의 JSX태그는 왜 감싸져야 하나요?**
> 
> JSX는 HTML처럼 생겼습니다. 하지만 실제로는 일반적인 JavaScript객체로 변환됩니다. JavaScript함수에서는 리턴값을 배열로 감싸지 않으면 두 개를 리턴할 수 없습니다. 이렇게 실제로 어떻게 동작하는지를 보면 왜 다른 태그나 fragment로 감싸지 않고는 두 개의 JSX 태그를 리턴할 수 없는지 알 수 있습니다.

### 2. 모든 태그를 닫자

JSX는 완전히 닫힌 태그를 요구합니다. 스스로 닫는 기능이 있는 `<img>`도 `<img />`가 되어야 합니다. 그리고 `<li>oranges`처럼 감싸주는 태그들은 `<li>oranges</li>`로 적어야 합니다.

아래는 Hedy Lamarr의 사진과 리스트 아이템이 닫힌 태그로 구성된 모습입니다. 

```JSX
<>
  <img 
    src="https://i.imgur.com/yXOvdOSs.jpg" 
    alt="Hedy Lamarr" 
    class="photo"
   />
  <ul>
    <li>Invent new traffic lights</li>
    <li>Rehearse a movie scene</li>
    <li>Improve the spectrum technology</li>
  </ul>
</>
```

### 3. 모든 것에 camelCase를 사용하자!

JSX가 JavaScript로 변환되면서 JSX로 쓰여진 속성들은 JavaScript 객체의 키가 됩니다. 컴포넌트를 사용하면서, 종종 속성들을 변수로 읽고 싶을 것입니다. 하지만 JavaScript는 변수명에 제약이 있습니다. 예를 들면, 변수명은 대시(—)를 포함할 수 없고, `class`와 같은 예약된 단어를 사용할 수 없습니다. 

이러한 이유로 React에서는 camelCase로 많은 HTML과 SVG 속성들을 적습니다. 예를 들어, `stroke-width` 대신에 `strokeWidth`를 사용합니다. `class`가 예약어이기 때문에 React에서는 [해당하는 Dom 요소](https://developer.mozilla.org/en-US/docs/Web/API/Element/className)를 이름 짓는데 `className`을 사용합니다. 

```JSX
<img 
  src="https://i.imgur.com/yXOvdOSs.jpg" 
  alt="Hedy Lamarr" 
  className="photo"
/>
```

여러분은 모든 [React Dom element](https://beta.reactjs.org/TODO)들의 속성을 찾아볼 수 있습니다. 잘못할까봐 걱정하지 마세요 - React가 브라우저 콘솔에 수정 예시 메세지를 프린트해줄 겁니다. 

## 조심할 사항

> 과거의 흔적으로, `area-*`와`data-*`는 HTML에서 대시(-)와 같이 쓰입니다.

## 꿀팁: JSX 변환기를 사용하자

이미 있는 마크업의 속성들을 모두 바꾸는 것은 지루한 작업일 수 있습니다! 이미 있는 HTML과 SVG를 JSX로 바꾸는데 [변환기](https://transform.tools/html-to-jsx)를 사용하기를 권합니다. 변환기는 매우 실용적이지만, 여전히 스스로 JSX를 편안하게 작성할 수 있도록 어떻게 돌아가는지는 이해할 필요가 있습니다. 

여기 최종 결과물입니다: 

```JSX
//App.js
export default function TodoList() {
  return (
    <>
      <h1>Hedy Lamarr's Todos</h1>
      <img 
        src="https://i.imgur.com/yXOvdOSs.jpg" 
        alt="Hedy Lamarr" 
        className="photo" 
      />
      <ul>
        <li>Invent new traffic lights</li>
        <li>Rehearse a movie scene</li>
        <li>Improve the spectrum technology</li>
      </ul>
    </>
  );
```
<img width="519" alt="스크린샷 2022-09-06 오후 11 57 21" src="https://user-images.githubusercontent.com/52595663/188668271-cfdf2097-10ef-4997-87ad-3f7d01ee569e.png">

[CodeSandBox](https://codesandbox.io/s/q2blb9?file=/App.js&from-sandpack=true)에서 직접 코드를 작성할 수 있습니다.

## 복습하기

이제 왜 JSX가 있고 JSX를 어떻게 컴포넌트로 사용하는지 배웠습니다.

- React component는 렌더링 로직과 마크업이 연관되어 있기 때문에 하나로 묶어줍니다.
- JSX는 몇 가지 차이를 제외하곤 HTML과 비슷합니다. 필요하면 [변환기](https://transform.tools/html-to-jsx)를 사용할 수 있습니다. 
- 종종 에러 메세지가 마크업을 옳은 방향으로 수정하도록 짚어줄 수 있습니다.

## 도전 과제

### 도전 과제1 : HTML을 JSX로 바꾸기

컴포넌트에 HTML이 전달되었는데 적절한 JSX가 아집니다. 고쳐보세요:

```JSX
//App.js
export default function Bio() {
  return (
    <div class="intro">
      <h1>Welcome to my website!</h1>
    </div>
    <p class="summary">
      You can find my thoughts here.
      <br><br>
      <b>And <i>pictures</b></i> of scientists!
    </p>
  );
}
```
[CodeSandBox](https://codesandbox.io/s/o3j6fk?file=%2FApp.js&from-sandpack=true)에서 정답을 확인할 수 있습니다.

손으로 해볼 지 변환기를 사용할 지는 자유입니다!
