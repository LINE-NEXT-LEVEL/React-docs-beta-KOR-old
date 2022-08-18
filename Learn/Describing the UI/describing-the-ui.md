# UI 표현하기
React는 유저 인터페이스(UI)를 렌더링하기 위한 JavaScript 라이브러리입니다. UI는 버튼, 텍스트, 이미지같은 작은 단위들로부터 만들어집니다. React는 이들을 재사용 가능하고, 중첩 가능한 컴포넌트로 조합해줍니다. 웹 사이트부터 스마트폰의 앱까지, 스크린에 있는 모든 것들은 컴포넌트로 쪼개질 수 있습니다. 이번 시간에는 React 컴포넌트를 생성하고, 커스텀하고, 조건에 따라 화면에 그리는 방법에 대해 배우게 됩니다.

> 이 단원에서 다룰 것들
> - [첫 React 컴포넌트를 어떻게 작성할 수 있는지](https://beta.reactjs.org/learn/your-first-component)
> - [언제 그리고 어떻게 다중 컴포넌트 파일을 만드는지](https://beta.reactjs.org/learn/importing-and-exporting-components)
> - [JSX를 이용해 마크업을 JavaScript로 표현하는 방법](https://beta.reactjs.org/learn/writing-markup-with-jsx)
> - [컴포넌트에서 중괄호({})와 JSX를 이용해 JavaScript 기능들에 접근하는 방법](https://beta.reactjs.org/learn/javascript-in-jsx-with-curly-braces)
> - [props를 이용해 컴포넌트를 구성하는 방법](https://beta.reactjs.org/learn/passing-props-to-a-component)
> - [컴포넌트를 조건에 따라 렌더링하는 방법](https://beta.reactjs.org/learn/conditional-rendering)
> - [한번에 여러 컴포넌트를 렌더링하는 방법](https://beta.reactjs.org/learn/rendering-lists)
> - [컴포넌트를 순수하게 유지함으로써 버그를 방지하는 방법](https://beta.reactjs.org/learn/keeping-components-pure)


## 첫 번째 컴포넌트
React 애플리케이션은 컴포넌트라고 부르는 격리된 UI 조각들로부터 만들어집니다. React 컴포넌트는 JavaScript 함수이고, 마크업을 조합해 작성합니다. 컴포넌트는 하나의 버튼처럼 작을수도 있고, 페이지 전체만큼 클 수도 있습니다. 아래 예시는 `Profile` 컴포넌트 세 개를 렌더링하는 `Gallery` 컴포넌트입니다.

```jsx
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

> **이 주제에 대해 배울 준비가 되셨나요?**
> [첫 컴포넌트](https://beta.reactjs.org/learn/your-first-component에 대해 읽으며 어떻게 React 컴포넌트를 선언하고 사용하는지 배워봅시다. 
> [더 읽어보기](https://beta.reactjs.org/learn/your-first-component)


## 컴포넌트 내보내고 불러오기
여러 컴포넌트를 하나의 파일에서 선언할 수도 있습니다. 하지만 큰 파일은 둘러보기가 불편할 수 있습니다. 이 문제를 해결하려면 컴포넌트를 적절한 파일로 _내보내기(export)_ 해야 합니다. 그리고 _불러오기(import)_를 통해 내보내진 컴포넌트를 다른 파일에서 사용할 수 있습니다.

```jsx
import Profile from './Profile.js';

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

> **이 주제에 대해 배울 준비가 되셨나요?**
> [컴포넌트 내보내고 불러오기](https://beta.reactjs.org/learn/importing-and-exporting-components)에 대해 읽으며 어떻게 컴포넌트를 적절한 파일로 분리시킬지 배워보세요.
> [더 읽어보기](https://beta.reactjs.org/learn/importing-and-exporting-components)


## JSX로 마크업 작성하기
각각의 React 컴포넌트는 JavaScript 함수입니다. 컴포넌트는 React가 브라우저를 통해 렌더링할 수 있는 마크업을 포함하고 있을 수도 있습니다. React 컴포넌트는 마크업을 JSX라고 부르는 확장 문법을 통해 표현합니다. JSX는 HTML과 비슷하게 생겼지만, 조금 더 엄격하고, 대신 정보들을 더 동적으로 표현할 수 있습니다.

HTML 마크업을 그대로 React 컴포넌트에 복사한다면, 제대로 동작하지 않을 가능성이 있습니다.

```jsx
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
      <li>Improve spectrum technology
    </ul>
  );
}
// Error : /App.js: Adjacent JSX elements must be wrapped in an enclosing tag. Did you want a JSX fragment <>...</>? (5:4)
```

HTML 코드가 위처럼 생겼다면, [converter](https://transform.tools/html-to-jsx)를 통해 고쳐볼 수 있습니다.

```jsx
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
        <li>Improve spectrum technology</li>
      </ul>
    </>
  );
}
```

> **이 주제애 대해 배울 준비가 되셨나요?**
> [JSX로 마크업 작성하기](https://beta.reactjs.org/learn/writing-markup-with-jsx)에 대해 읽고 어떻게 유효한 JSX를 작성하는지 배워보세요.
> [더 읽어보기](https://beta.reactjs.org/learn/writing-markup-with-jsx)


## 중괄호({})를 통해 JSX에 JavaScript 주입하기
JSX는 HTML처럼 생긴 마크업 문법입니다. JavaScript 파일 내부에 쓸 수 있기 때문에 렌더링 로직과 내용을 한 곳에서 관리할 수 있다는 장점이 있습니다. 가끔 여러분은 마크업 안에 약간의 JavaScript 로직이나 동적인 프로퍼티에 대한 참조를 집어넣고 싶을 수 있습니다. 이런 상황에서는 중괄호({})를 JSX 안에 씀으로써 JavaScript에게 일종의 '창문'을 열어줄 수 있습니다.

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

> **이 주제에 대해 배울 준비가 되셨나요?**
> [중괄호({})를 이용해 JSX안에 JavaScript 작성하기](https://beta.reactjs.org/learn/javascript-in-jsx-with-curly-braces)를 읽고 어떻게 JSX 내부에서 JavaScript 데이터에 접근할 수 있는지를 배워보세요.
> [더 읽어보기](https://beta.reactjs.org/learn/javascript-in-jsx-with-curly-braces)


## 컴포넌트에 props 넘겨주기
React 컴포넌트는 컴포넌트끼리 소통하기 위해 _props_를 사용합니다. 모든 부모 컴포넌트는 props를 자식 컴포넌트에게 넘겨줌으로써 정보를 전달해줄 수 있습니다. Props는 HTML 속성(attribute)와 비슷하게 생겼습니다. 그치만 props를 통해서라면 어떤 JavaScript 값이라도 넘겨줄 수 있습니다. 객체, 배열, 함수, 심지어 JSX까지 말이죠!

```jsx
import { getImageUrl } from './utils.js'

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

function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}
```

> **이 주제에 대해 배울 준비가 되셨나요?**
> [Props를 컴포넌트에 넘겨주기](https://beta.reactjs.org/learn/passing-props-to-a-component)를 읽고 어떻게 props를 전달하는지 배워보세요.
> [더 읽어보기](https://beta.reactjs.org/learn/passing-props-to-a-component)


## 조건부 렌더링
종종 컴포넌트는 어떤 조건에 따라 다른 내용을 보여줘야 할 때가 있습니다. React에서는 JavsScript 문법을 통해 조건부로 JSX를 렌더링하는 것이 가능합니다. `if`문이나 `&&`, `? :` 연산자를 이용하면 됩니다.

예를 들어, JavaScript의 `&&` 연산자는 조건부로 체크 마크를 렌더링할 때 사용합니다.

```jsx
function Item({ name, isPacked }) {
  return (
    <li className="item">
      {name} {isPacked && '✔'}
    </li>
  );
}

export default function PackingList() {
  return (
    <section>
      <h1>Sally Ride's Packing List</h1>
      <ul>
        <Item
          isPacked={true}
          name="Space suit"
        />
        <Item
          isPacked={true}
          name="Helmet with a golden leaf"
        />
        <Item
          isPacked={false}
          name="Photo of Tam"
        />
      </ul>
    </section>
  );
}
```

> **이 주제에 대해 배울 준비가 되셨나요?**
> [조건부 렌더링](https://beta.reactjs.org/learn/conditional-rendering)을 읽고 조건부로 화면을 그리는 방법에 대해 배워보세요.
> [더 읽어보기](https://beta.reactjs.org/learn/conditional-rendering)


## 배열 렌더링
가끔 여러분은 데이터 모음(collection)으로부터 여러개의 유사한 컴포넌트를 그리고 싶을 수 있습니다. React와 함께 JavaScript의 `filter()`와 `map()`을 이용하면 데이터 배열을 필터링하거나 변형시켜 컴포넌트의 배열을 만들 수 있습니다.

```jsx
import { people } from './data.js';
import { getImageUrl } from './utils.js';

export default function List() {
  const listItems = people.map(person =>
    <li key={person.id}>
      <img
        src={getImageUrl(person)}
        alt={person.name}
      />
      <p>
        <b>{person.name}:</b>
        {' ' + person.profession + ' '}
        known for {person.accomplishment}
      </p>
    </li>
  );
  return (
    <article>
      <h1>Scientists</h1>
      <ul>{listItems}</ul>
    </article>
  );
}
```

> **이 주제에 대해 배울 준비가 되셨나요?**
> [배열 렌더링](https://beta.reactjs.org/learn/rendering-lists)을 읽고 어떻게 컴포넌트 배열을 렌더링하는지, 어떻게 key를 고르는지에 대해 배워보세요.
> [더 읽어보기](https://beta.reactjs.org/learn/rendering-lists)


## 컴포넌트를 순수하게 유지하기
몇몇 JavaScript 함수들은 순수합니다. 순수 함수란
- **외부 상황에 관심이 없습니다.** 순수 함수는 자기가 호출되기 이전의 어떤 객체나 변수도 변경하지 않습니다.
- **같은 입력은 언제나 같은 출력을 보장합니다.** 순수 함수는 같은 인자를 주었을 때 언제나 같은 결과(return)를 돌려줍니다.

컴포넌트를 순수 함수처럼 엄격하게 작성한다면, 코드가 커지더라도 여러분을 당황스럽게 하는 버그들과 예측 불가능한 동작들을 피할 수 있습니다. 아래 예시는 순수하지 않은 컴포넌트입니다.

```jsx
let guest = 0;

function Cup() {
  // Bad: changing a preexisting variable!
  guest = guest + 1;
  return <h2>Tea cup for guest #{guest}</h2>;
}

export default function TeaSet() {
  return (
    <>
      <Cup />
      <Cup />
      <Cup />
    </>
  )
}
```

기존 변수를 수정하는 대신 prop을 넘겨주는 것으로 컴포넌트를 순수하게 만들 수 있습니다.

```jsx
function Cup({ guest }) {
  return <h2>Tea cup for guest #{guest}</h2>;
}

export default function TeaSet() {
  return (
    <>
      <Cup guest={1} />
      <Cup guest={2} />
      <Cup guest={3} />
    </>
  );
}
```

> **이 주제에 대해 배울 준비가 되셨나요?**
> [컴포넌트를 순수하게 유지하기](https://beta.reactjs.org/learn/keeping-components-pure)를 읽고 어떻게 컴포넌트를 순수하고 예측 가능한 함수처럼 작성할 수 있는지 배워보세요.
> [더 읽어보기](https://beta.reactjs.org/learn/keeping-components-pure)


## 다음 내용은?
[첫 컴포넌트](https://beta.reactjs.org/learn/your-first-component)부터 시작해 이번 단원을 읽어보세요.
이미 이 주제에 대해 잘 알고 있다면, [상호작용 추가하기](https://beta.reactjs.org/learn/adding-interactivity)는 어떠신가요?
