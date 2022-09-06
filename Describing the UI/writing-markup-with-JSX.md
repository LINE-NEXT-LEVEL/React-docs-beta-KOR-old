# JSX로 마크업 작성하기

_JSX_ 는 JavaScript 파일 안에서 HTML 같은 마크업을 작성하게 해주는 JavaScript를 위한 구문 확장자입니다. 컴포넌트를 쓰는 다른 방법들이 있지만, 대부분의 React 개발자들은 JSX의 간결함을 선호하고, 대부분의 기존 코드들도 JSX를 사용합니다. 

> **이런 것들을 배웁니다.**
> - React가 렌더링 로직과 마크업을 섞는 이유
> - JSX가 HTML과 다른 점
> - JSX로 정보를 표현하는 방법

## JSX: JavaScript안에 마크업을 넣기
웹은 HTML, CSS, JavaScript로 만들어져왔습니다. 수년간 웹 개발자들은 HTML 안에 내용, CSS안에는 디자인, JavaScript 안에는 로직을 넣었습니다. 종종 분리된 파일로도 작성했습니다. 페이지의 로직이 JavaScript에 분리되어 실행되는 동안 콘텐츠는 HTML에서 마크업 됩니다. 

![참고 이미지](../img/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202022-08-24%20%EC%98%A4%EC%A0%84%208.20.06.png)

하지만 웹은 더 인터랙티브해졌고, 로직이 컨텐츠를 결정하는 일이 많아지면서 JavaScript가 HTML을 담당하게 되었습니다. 그래서 React에서는 렌더링 로직과 마크업이 컴포넌트로 같은 위치에 있게 되었습니다. 

![참고이미지](../img/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202022-08-24%20%EC%98%A4%EC%A0%84%208.25.56.png)

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

![결과 이미지](../img/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202022-08-24%20%EC%98%A4%EC%A0%84%208.38.14.png)
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

만약 추가로 `<div>`를 넣고 싶지 않으면 `<>`와`</>`를 대신 사용하면 됩니다.:

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

### 3. 모든 것에 camelCase를 사용하자

JSX가 JavaScript로 변환되면서 JSX로 쓰여진 속성들은 JavaScript 객체의 키가 됩니다. 


