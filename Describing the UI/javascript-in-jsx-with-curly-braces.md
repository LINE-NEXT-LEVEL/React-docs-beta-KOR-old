# 중괄호(Curly Braces)를 통해 JSX에서 JavaScript 사용하기

JSX는 JavaScript 파일에서 HTML과 유사한 마크업을 작성할 수 있도록 해줍니다. 렌더링 로직과 렌더링할 데이터를 한 곳에서 관리할 수 있습니다. 가끔 마크업 안에 간단한 JavaScript 로직이나 동적인 속성에 대한 참조를 추가하고 싶을 때가 있습니다. 이런 상황에서는 중괄호(curly braces)를 이용해 JSX에 JavaScript 코드를 포함시킬 수 있습니다.

> **여러분이 배울 것들**
>
> - 따옴표(') 혹은 쌍따옴표(')를 이용해 string을 전달하는 방법
> - 중괄호를 이용해 JavaScript 변수의 참조를 JSX 내부에 전달하는 방법
> - 중괄호를 이용해 JSX 내부에서 JavaScript 함수를 호출하는 방법
> - 중괄호를 이용해 JSX 내부에서 JavaScript 객체를 사용하는 방법

## 따옴표(') 혹은 쌍따옴표(')를 이용해 string을 전달하는 방법

만약 string 타입의 속성을 JSX에 전달하려 한다면, 따옴표 혹은 쌍따옴표를 통해 감싸면 됩니다.

[CodeSandbox](https://codesandbox.io/s/lkd0no?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.

```jsx
export default function Avatar() {
  return (
    <img
      className="avatar"
      src="https://i.imgur.com/7vQD0fPs.jpg"
      alt="Gregorio Y. Zara"
    />
  );
}
```

<img width="593" alt="스크린샷 2022-08-31 오전 1 09 42" src="https://user-images.githubusercontent.com/53335940/187486972-e36f790b-523d-4695-949b-4fe34b0997f2.png">

여기서 `"https://i.imgur.com/7vQD0fPs.jpg"`와 `"Gregorio Y. Zara"`가 string으로서 전달되었습니다.
만약 여러분이 `src`나 `alt` 텍스트를 동적으로 지정해주고 싶다면 어떻게 해야 할까요? **`{`와 `}`로 감싸진 JavaScript 변수를 사용하면 됩니다.**

[CodeSandbox](https://codesandbox.io/s/j25087?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.

```jsx
export default function Avatar() {
  const avatar = 'https://i.imgur.com/7vQD0fPs.jpg';
  const description = 'Gregorio Y. Zara';
  return (
    <img
      className="avatar"
      src={avatar}
      alt={description}
    />
  );
}
```

<img width="581" alt="스크린샷 2022-08-31 오전 1 13 44" src="https://user-images.githubusercontent.com/53335940/187487749-8db3915e-a540-4f07-af3e-194146c6f000.png">

`className="avatar"`와 `src={avatar}`의 차이점이 보이시나요? `className="avatar"`는 이미지를 둥글게 해주는 CSS 클래스를 지정해주고, `src={avatar}`는 JavaScript 변수 `avatar`의 값을 참조합니다. 중괄호가 마크업 안에서 JavaScript 코드를 쓸 수 있도록 도와주었기 때문에 가능합니다.

## 중괄호 사용하기: JavaScript 세상으로 통하는 창문

JSX는 JavaScript를 작성하는 한 가지 특별한 방법입니다. 중괄호(`{ }`)와 함께라면 JavaScript 코드를 내부에 적는게 가능하다는 말입니다. 아래의 예제를 봅시다. 우선 과학자의 이름을 `name`이란 변수에 선언합니다. 그리고 중괄호를 `<h1>`안에 `name` 변수를 심고 있습니다.

[CodeSandbox](https://codesandbox.io/s/kmv2h8?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.

```jsx
export default function TodoList() {
  const name = 'Gregorio Y. Zara';
  return (
    <h1>{name}'s To Do List</h1>
  );
}

```

<img width="578" alt="스크린샷 2022-08-31 오전 1 19 52" src="https://user-images.githubusercontent.com/53335940/187488887-d40bc4c5-3828-466d-ba02-e71294d2f476.png">

`name` 변수를 'Gregorio Y. Zara'에서 'Hedy Lamarr'로 바꿔보세요. 바뀐 점을 눈치 채셨나요?
`formatDate()`와 같은 함수를 포함한 어떤 JavaScript 표현식도 중괄호 내부에서는 동작합니다.

[CodeSandbox](https://codesandbox.io/s/iuf3k6?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.

```jsx
const today = new Date();

function formatDate(date) {
  return new Intl.DateTimeFormat(
    'en-US',
    { weekday: 'long' }
  ).format(date);
}

export default function TodoList() {
  return (
    <h1>To Do List for {formatDate(today)}</h1>
  );
}
```

<img width="581" alt="스크린샷 2022-08-31 오전 1 21 56" src="https://user-images.githubusercontent.com/53335940/187489238-0d984bc5-7423-4682-8f7f-e37903f970f2.png">

### 중괄호를 어디서 사용해야 하나요?

오직 두 가지 방법으로만 중괄호를 JSX와 함께 사용할 수 있습니다.

1. **텍스트로서** JSX 태그 안에 바로 넣기 : `<h1>{name}'s To Do List</h1>`는 동작 합니다. 하지만 `{tag}>Gregorio Y. Zara's To Do List</{tag}>`는 동작하지 않습니다.
2. **속성으로서** `=`기호 바로 다음에 사용하기 : `src={avatar}`는 `avatar`의 값을 읽습니다. 하지만 `src="{avatar}"`는 `{avatar}`라는 string 값을 전달할 것입니다.

## "이중 중괄호" 사용하기: CSS와 다른 객체

string, number, 그리고 다른 JavaScript 표현식들 뿐만 아니라, 객체를 JSX에 전달하는 것도 가능합니다. 객체들은 `{ name: "Hedy Lamarr", inventions: 5 }`와 같이 원래부터 중괄호를 이용해 표현됩니다. 그래서 JS 객체를 JSX에 전달하기 위해서는 또 다른 중괄호 쌍으로 객체를 감싸주어야 합니다. `person={{ name: "Hedy Lamarr", inventions: 5 }}` 이렇게요.

JSX 안에 CSS 스타일을 추가하는 경우에 이런 식으로 표기하곤 합니다. React가 이런 스타일을 요구하는건 아닙니다(CSS 클래스는 대부분의 경우에 훌륭한 방법입니다). 그래도 이렇게 inline 스타일을 추가하는 것이 필요한 경우 `style` 속성에 객체를 넘겨주면 됩니다.

[CodeSandbox](https://codesandbox.io/s/u02y7v?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.

```jsx
export default function TodoList() {
  return (
    <ul style={{
      backgroundColor: 'black',
      color: 'pink'
    }}>
      <li>Improve the videophone</li>
      <li>Prepare aeronautics lectures</li>
      <li>Work on the alcohol-fuelled engine</li>
    </ul>
  );
}
```

<img width="583" alt="스크린샷 2022-08-31 오전 1 28 10" src="https://user-images.githubusercontent.com/53335940/187490370-bddb8a77-aade-4455-b2b2-11ecac29bc86.png">

`backgroundColor`와 `color` 값을 바꿔보세요.
아래와 같이 작성하면 중괄호 내부의 JavaScript 객체를 제대로 볼 수 있습니다.

```jsx
<ul style={
  {
    backgroundColor: 'black',
    color: 'pink'
  }
}>
```

이제부터 여러분이 JSX 내부에서 `{{`와 `}}`를 본다면, 그냥 JSX 중괄호 안에 있는 단순한 객체라는걸 알아차릴 수 있게 될겁니다.

> **주의 사항**
>
> 인라인 `style` 속성은 카멜케이스(camelCase)로 작성됩니다. 예를 들어 HTML 코드인 `<ul style="background-color: black">`는 컴포넌트에서 `<ul style={{ backgroundColor: 'black' }}>` 이렇게 작성되어야 합니다.

## JavaScript 객체와 중괄호에 대한 더 재밌는 사실들

한 객체 안에 여러개의 표현식들을 담고, JSX의 중괄호에서 한꺼번에 참조할 수도 있습니다.

[CodeSandbox](https://codesandbox.io/s/osbftg?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.

```jsx
const person = {
  name: 'Gregorio Y. Zara',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src="https://i.imgur.com/7vQD0fPs.jpg"
        alt="Gregorio Y. Zara"
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

<img width="582" alt="스크린샷 2022-08-31 오전 1 37 45" src="https://user-images.githubusercontent.com/53335940/187492175-90e588b8-f21e-4aea-ae81-814350c2f90a.png">

이 예제에서 JavaScript 객체 `person`은 string 타입인 `name`과 객체인 `theme`을 가지고 있습니다.

```js
const person = {
  name: 'Gregorio Y. Zara',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};
```

컴포넌트는 이 값들을 `person`에 접근해 사용합니다.

```jsx
<div style={person.theme}>
  <h1>{person.name}'s Todos</h1>
```

## 돌아보기

이제 여러분은 JSX에 대해 거의 모든걸 배웠습니다.

- JSX 속성으로서 따옴표로 둘러싸인 텍스트는 string으로 전달됩니다.
- 중괄호는 JavaScript 로직을 마크업과 함께 작성할 수 있도록 해줍니다.
- 중괄호는 JSX 태그 내부나 `=` 기호 바로 뒤에 속성으로서 이용됩니다.
- `{{`와 `}}`는 특별한 문법이 아닙니다. JavaScript 객체를 JSX 중괄호 내부에서 표현하기 위한 방법일 뿐입니다.

## 도전 과제

### 도전 1: 실수 수정하기

아래 코드는 `Objects are not valid as a React child`라는 에러 문구와 함께 동작하지 않습니다.

[Code Sandbox](https://codesandbox.io/s/l1vt8l?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.

```jsx
const person = {
  name: 'Gregorio Y. Zara',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person}'s Todos</h1>
      <img
        className="avatar"
        src="https://i.imgur.com/7vQD0fPs.jpg"
        alt="Gregorio Y. Zara"
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

<img width="539" alt="스크린샷 2022-08-31 오전 1 56 02" src="https://user-images.githubusercontent.com/53335940/187495603-7de65090-56ee-4820-bb0b-2ef2a5c0d087.png">

**힌트**
중괄호 안을 잘 살펴보세요. 올바른 값을 넣고 있나요?

**정답**
string이 아닌 _객체 자체를_ 마크업에 넘겨주었기 때문에 예시에서 문제가 발생했습니다. `<h1>{person}'s Todos</h1>`은 `person` 객체 전부를 렌더링 하려고 하고 있어요! 객체를 통째로 텍스트처럼 취급하려 하는 것은 에러를 발생시킵니다. React는 여러분이 이를 어떻게 표현하고 싶어 하는지 모르기 때문입니다.

이 문제를 해결하려면 `<h1>{person}'s Todos</h1>`를 `h1>{person.name}'s Todos</h1>`로 수정해야 합니다.

[Code Sandbox](https://codesandbox.io/s/osbftg?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.

```jsx
const person = {
  name: 'Gregorio Y. Zara',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src="https://i.imgur.com/7vQD0fPs.jpg"
        alt="Gregorio Y. Zara"
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

<img width="548" alt="스크린샷 2022-08-31 오전 2 08 26" src="https://user-images.githubusercontent.com/53335940/187498046-f32b5b18-ba12-4ac9-945f-bbeb1fbf1455.png">

### 도전 2: 객체에서 정보 추출하기

`person` 객체에서 이미지 URL을 추출해보세요.

[Code Sandbox](https://codesandbox.io/s/osbftg?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.

```jsx
const person = {
  name: 'Gregorio Y. Zara',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src="https://i.imgur.com/7vQD0fPs.jpg"
        alt="Gregorio Y. Zara"
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

<img width="549" alt="스크린샷 2022-08-31 오전 1 57 38" src="https://user-images.githubusercontent.com/53335940/187495895-232a4a68-5269-472f-8541-587d3a72cd59.png">

**정답**
이미지 URL을 `person.imageUrl` 프로퍼티로 바꾸고 `<img>` 태그에서 중괄호를 이용해 읽도록 합니다.

[Code Sandbox](https://codesandbox.io/s/xwp20z?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.

```jsx
const person = {
  name: 'Gregorio Y. Zara',
  imageUrl: "https://i.imgur.com/7vQD0fPs.jpg",
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src={person.imageUrl}
        alt="Gregorio Y. Zara"
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

<img width="549" alt="스크린샷 2022-08-31 오전 1 57 38" src="https://user-images.githubusercontent.com/53335940/187495895-232a4a68-5269-472f-8541-587d3a72cd59.png">

### 도전 3: JSX 중괄호 안에 표현식 작성하기

아래 객체에서 완전한 이미지 URL은 base URL, `imageId`, `imageSize`, 파일 확장자 총 4개의 조각으로 나뉘어져 있습니다 : base URL(항상 `'https://i.imgur.com/'`), `imageId`(`'7vQD0fP'`), `imageSize`(`'s'`), 그리고 파일 확장자(항상 `'.jpg'`).
이 조각들을 조합해 하나의 이미지 URL을 만들고 싶습니다. 그런데 `<img>` 태그에서 `src`를 잘못 지정한것 같아 보입니다.
고칠 수 있나요?

[Code Sandbox](https://codesandbox.io/s/5l3sdj?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.

```jsx
const baseUrl = 'https://i.imgur.com/';
const person = {
  name: 'Gregorio Y. Zara',
  imageId: '7vQD0fP',
  imageSize: 's',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src="{baseUrl}{person.imageId}{person.imageSize}.jpg"
        alt={person.name}
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}
```

<img width="548" alt="스크린샷 2022-08-31 오전 2 03 22" src="https://user-images.githubusercontent.com/53335940/187496979-a887ba51-bc2f-4956-87ef-d27b60369d06.png">

알맞게 고쳤는지 확인하기 위해서는 `imageSize`의 값을 `'b'`로 바꿔보세요. 그럼 수정 후에 이미지의 사이즈가 재조정 될 것입니다.

**정답**
`src={baseUrl + person.imageId + person.imageSize + '.jpg'}` 는 정답이 될 수 있습니다.

1. `{`를 통해 중괄호를 열고 JavaScript 표현식 작성하기.
3. 알맞은 URL string 조합하기 (`baseUrl + person.imageId + person.imageSize + '.jpg'`)
4. `}`를 통해 중괄호를 닫아 JavaScript 표현식 끝맺기.

[Code Sandbox](https://codesandbox.io/s/1zerz2?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.

```jsx
const baseUrl = 'https://i.imgur.com/';
const person = {
  name: 'Gregorio Y. Zara',
  imageId: '7vQD0fP',
  imageSize: 's',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src={baseUrl + person.imageId + person.imageSize + '.jpg'}
        alt={person.name}
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}

```

<img width="549" alt="스크린샷 2022-08-31 오전 1 57 38" src="https://user-images.githubusercontent.com/53335940/187495895-232a4a68-5269-472f-8541-587d3a72cd59.png">

이 식을 아래의 `getImageUrl`처럼 별도의 함수로 분리할 수도 있습니다.

[Code Sandbox](https://codesandbox.io/s/l8qtdp?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.

```jsx
// App.js
import { getImageUrl } from './utils.js'

const person = {
  name: 'Gregorio Y. Zara',
  imageId: '7vQD0fP',
  imageSize: 's',
  theme: {
    backgroundColor: 'black',
    color: 'pink'
  }
};

export default function TodoList() {
  return (
    <div style={person.theme}>
      <h1>{person.name}'s Todos</h1>
      <img
        className="avatar"
        src={getImageUrl(person)}
        alt={person.name}
      />
      <ul>
        <li>Improve the videophone</li>
        <li>Prepare aeronautics lectures</li>
        <li>Work on the alcohol-fuelled engine</li>
      </ul>
    </div>
  );
}

// utils.js
export function getImageUrl(person) {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    person.imageSize +
    '.jpg'
  );
}
```

<img width="549" alt="스크린샷 2022-08-31 오전 1 57 38" src="https://user-images.githubusercontent.com/53335940/187495895-232a4a68-5269-472f-8541-587d3a72cd59.png">

변수와 함수는 마크업이 단순함을 유지할 수 있도록 도와줍니다!
