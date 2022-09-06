# 조건부 렌더링

보통 컴포넌트는 다양한 조건에 따라서 다른 것들을 보여줄 필요가 있습니다. 리엑트에서 `if` 구문, `&&`, 그리고 `? :` 연산자와 같은 자바스크립트 문법을 사용해 JSX를 조건에 맞추어 렌더링할 수 있습니다.

> **여러분이 배울 것들**
>
> - 조건에 따라 다른 JSX를 반환하는 방법
> - 조건에 따라 JSX 조각을 포함하거나 제외하는 방법
> - 리엑트 코드에서 흔히 사용하는 조건 문법의 줄임

## JSX를 조건에 맞게 반환하기

짐으로 싸거나 싸지 않는 것을 표시할 수 있는 몇 개의 `Item`을 렌더링하는 `PackingList` 컴포넌트가 있습니다.

([CodeSandbox](https://codesandbox.io/s/g29jwx?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.)

```JavaScript
// App.js
function Item({ name, isPacked }) {
  return <li className="item">{name}</li>;
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

이미지

`Item` 컴포넌트들 중 몇 개는 `isPacked` prop을 `false` 대신에 `true`로 설정했습니다. `isPacked={true}`일 경우에 물건들을 싸는 것이므로 체크표시(✔)를 추가해야 합니다.

아래와 같이 [`if`/`else` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else) 로 작성할 수 있습니다:

```JavaScript
if (isPacked) {
  return <li className="item">{name} ✔</li>;
}
return <li className="item">{name}</li>;
```

`isPacked` prop이 `true`라면, 이 코드는 다른 JSX tree를 반환합니다. 이 코드를 적용하면, 아이템 중 몇 개가 끝에 체크표시를 가지게 됩니다:

([CodeSandbox](https://codesandbox.io/s/os3sy7?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.)

```JavaScript
//App.js
function Item({ name, isPacked }) {
  if (isPacked) {
    return <li className="item">{name} ✔</li>;
  }
  return <li className="item">{name}</li>;
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

이미지

다른 경우에 무엇이 반환되는지 [CodeSandbox]를 수정해보고 결과가 어떻게 변화하는지 보세요!

자바스크립트의 `if`와 `return` 구문을 이용해 가지치기 로직을 생성하는 방법을 기억하세요. 리엑트에서 (조건과 같은) 흐름 제어는 JavaScript에 의해 조종됩니다.

## 조건에 맞추어 `null`을 이용해 아무것도 반환하지 않기

어떤 상황들에서는 어떤 것도 렌더링하고 싶지 않을 떄가 있습니다. 예를 들어, 여러분이 짐을 싸야 하는 아이템들을 전혀 보여주고 싶지 않을 수 있습니다. 컴포넌트는 무조건 어떤 것을 반환해야 합니다. 이런 경우, `null`을 반환할 수 있습니다:

```JavaScript
if (isPacked) {
  return null;
}
return <li className="item">{name}</li>;
```

`isPacked`가 true라면 컴포넌트(`Item`)는 null을 반환하는데, 즉 어떤 것도 반환하지 않습니다. `isPacked`가 false라면 JSX를 반환하고 렌더링할 것입니다:

([CodeSandbox](https://codesandbox.io/s/v9zmhr?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.)

```JavaScript
function Item({ name, isPacked }) {
  if (isPacked) {
    return null;
  }
  return <li className="item">{name}</li>;
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

이미지

실전에서 컴포넌트에서 `null`을 반환하는 것은 흔한 일이 아닌데 왜냐하면 렌더링을 시도하는 개발자가 놀랄 수 있기 때문입니다. 일반적으로 여러분은 부모 컴포넌트의 JSX에서 그 컴포넌트를 조건에 맞추어 포함하거나 제외합니다. 아래 글에서 어떻게 하는지 적혀있습니다!

## JSX를 조건에 맞게 포함하기

이전 예시에서, 어떤(무엇이든!) JSX tree가 컴포넌트에서 반환될지를 조절했습니다. 여러분은 이미 렌더링 출력 결과에서 중복을 알아차렸을 수도 있습니다.

```JSX
<li className="item">{name} ✔</li>
```

위 JSX는 아래 JSX와 매우 비슷합니다.

```JSX
<li className="item">{name}</li>
```

두 조건부 브랜치들은 모두 `<li className="item">...</li>`를 반환합니다:

```JavaScript
if (isPacked) {
  return <li className="item">{name} ✔</li>;
}
return <li className="item">{name}</li>;
```

중복이 치명적이지는 않지만 이 중복은 코드를 유지하는 걸 더 어렵게 만들 수 있습니다. `className` 변경을 원한다면 어떻게 될까요? 코드에서 두 곳 모두 `className`을 변경해야만 합니다. 그런 상황에서는 코드를 더 [간단](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)하게 만들기 위해서 최소한의 JSX를 조건에 맞게 포함해야 합니다.

## 조건부(삼항) 연산자(`? :`)

JavaScript는 조건식을 작성하는데 간편한 구문을 사용합니다 -- [조건부 연산자](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) 또는 "삼항 연산자."

이 코드 대신에:

```js
if (isPacked) {
  return <li className="item">{name} ✔</li>;
}
return <li className="item">{name}</li>;
```

아래처럼 작성할 수 있습니다:

```js
return (
  <li className="item">
    {isPacked ? name + ' ✔' : name}
  </li>
);
```

"`isPacked`가 true일 경우, 그러면(`?`) `name + ' ✔'`을 렌더링하고, 그렇지 않으면(`:`) `name`을 렌더링하세요."와 같이 해석할 수 있습니다.

> **깊이 파고들기**
>
> ## 두 예시들이 완전히 똑같습니까?
>
> 객체지향 프로그래밍을 알고 계신다면 위의 두 예시들은 미묘하게 다르다고 생각했을 수도 있습니다 왜냐하면 첫 번째 예시가 `<li>`라는 두 개의 다른 "인스턴스"를 만들기 때문입니다.
> 하지만 JSX 요소는 "인스턴스"가 아닙니다 왜냐하면 그 요소들은 어떠한 내부 상태를 가지고 있지 않고 실제 DOM 노드도 아니기 때문입니다. JSX 요소는 청사진과 같은 가벼운 설명입니다. 따라서 위 두 예시들은 사실 완벽히 같습니다. 이에 대한 작동원리는 [상태 보존 및 새롭게 세팅하기](https://beta.reactjs.org/learn/preserving-and-resetting-state)에서 상세하게 보실 수 있습니다.

이제 취소선을 긋기 위해 `<del>`과 같은 다른 HTML 태그로 아이템의 이름 전체를 감싸 봅시다. 더 많은 새 라인들과 소괄호들을 추가함으로서 각각의 경우들에 대해서 많은 JSX를 중첩하는 것이 더 쉬워졌습니다.

([CodeSandbox](https://codesandbox.io/s/kwrlob?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.)

```js
function Item({ name, isPacked }) {
  return (
    <li className="item">
      {isPacked ? (
        <del>
          {name + ' ✔'}
        </del>
      ) : (
        name
      )}
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

이미지

## 논리적인 AND 연산자(`&&`)

흔하게 마주칠 수 있는 또다른 축약표현은 [논리적인 AND 연산자(`&&`)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND)입니다. 조건이 true인 경우에만 렌더링하거나 즉 **조건에 맞지 않은 경우 어떤 것도 렌더링하지 않을** 때 리엑트 컴포넌트들에 종종 사용됩니다. `&&`로 여러분은 `isPacked`가 `true`일 때만 체크표시를 렌더링할 수 있습니다.  

```js
return (
  <li className="item">
    {name} {isPacked && '✔'}
  </li>
);
```

"`isPacked`인 경우, 그러면(`&&`) 체크표시를 렌더링하고, 그렇지 않으면, 아무것도 렌더링하지 마세요"라고 해석할 수 있습니다.

아래 결과를 보실 수 있습니다:

([CodeSandbox](https://codesandbox.io/s/cd4erk?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.)

```js
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

> **경고**
>
> `&&`의 왼쪽에 숫자를 넣지 마세요.
>
> 조건을 검사하기 위해 JavaScript는 자동적으로 왼쪽 부분을 boolean으로 바꿉니다. 하지만, 만약 왼쪽 부분에 0이 있다면, 모든 표현이 그 값(0)이 되어 리엑트는 아무것도 렌더링하지 않는 것이 아니라 `0`을 렌더링할 것입니다.
> 예를 들어, `messageCount && <p>New messages</p>`와 같은 코드를 작성하는 것은 흔한 실수입니다. `messageCount`가 `0`일 때 아무것도 렌더링하지 않을 거라 생각하는 것이 쉽지만 실제로는 `0`을 렌더링합니다!
>
> 이것을 고치기 위해서 boolean을 왼쪽 부분에 두세요: `messageCount > 0 && <p>New messages</p>`

## 조건에 맞추어 JSX를 변수에 할당하기

단축표현이 코드를 작성하는 데 방해가 된다면 `if` 구문과 변수를 사용하세요. [`let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)으로 선언된 변수들에 재할당할 수 있습니다, 따라서 이름과 같은 여러분이 표시하고 싶은 기본 내용을 제공하고 시작하세요:

```js
let itemContent = name;
```

`if` 구문을 사용해 `isPacked`가 `true`일 경우 `itemContent`에 JSX 표현을 재할당합니다:

```js
if (isPacked) {
  itemContent = name + " ✔";
}
```

[중괄호는 "JavaScript로 가는 창"을 엽니다.](https://beta.reactjs.org/learn/javascript-in-jsx-with-curly-braces#using-curly-braces-a-window-into-the-javascript-world) 반환되는 JSX 트리 안의 중괄호 속에 변수를 넣고 이전에 계산된 값(`itemContent`)을 JSX 안에 넣으세요.  

```jsx
<li className="item">
  {itemContent}
</li>
```

이 스타일은 매우 장황하지만 매우 유연합니다. 아래 결과가 있습니다:

([CodeSandbox](https://codesandbox.io/s/0vrsow?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.)

```js
function Item({ name, isPacked }) {
  let itemContent = name;
  if (isPacked) {
    itemContent = name + " ✔";
  }
  return (
    <li className="item">
      {itemContent}
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

이미지

이전처럼, 이 코드는 글자뿐만 아니라 추상화된 JSX에서도 동작합니다.

([CodeSandbox](https://codesandbox.io/s/s3p7lh?file=%2FApp.js&from-sandpack=true)에서 확인 할 수 있습니다.)

```js
function Item({ name, isPacked }) {
  let itemContent = name;
  if (isPacked) {
    itemContent = (
      <del>
        {name + " ✔"}
      </del>
    );
  }
  return (
    <li className="item">
      {itemContent}
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

이미지

JavaScript에 익숙하지 않다면, 다양한 스타일은 처음에 버겁게 느껴질지도 모릅니다. 하지만, 이 스타일들을 배우는 것은 리엑트 컴포넌트뿐만 아니라 어떤 JavaScript 코드라도 읽고 쓰는 데 도움이 됩니다! 처음 시작하기에 더 좋은 스타일을 고르고나서 다른 것이 어떻게 동작하는지 잊었을 때 이 글을 다시 읽어보세요.

## 요약

- 리엑트에서는 JavaScript로 분기처리를 제어합니다.
- `if` 구문을 통해 JSX 표현을 조건적으로 반환할 수 있습니다.
- 조건에 맞게 JSX를 변수에 저장하고 나서 중괄호를 이용해 다른 JSX 속에 해당 변수를 넣을 수 있습니다.
- JSX에서 `{cond ? <A /> : <B />}`는 "`cond`하면 `<A />`를 렌더링하고, 그렇지 않으면 `<B />`를 렌더링한다"를 의미합니다.
- JSX에서 `{cond && <A />}`는 "`cond`하면 `<A />`를 렌더링하고, 그렇지 않으면 `<B />`를 렌더링한다"를 의미합니다.
- 단축 표현은 흔하지만 `if`를 선호한다면 단축표현을 사용할 필요는 없습니다.

> ## 도전 과제
>
> ### 도전 1: `? :`를 이용해 불완전한 아이템들 아이콘을 보여주기
>
> **도전 1: `? :`를 이용해 불완전한 아이템들 아이콘을 보여주기**
>
> `isPacked`가 `true`가 아닌 경우 조건연산자(`cond ? a : b`)를 사용해 ❌를 렌더링하세요.

([CodeSandbox](https://codesandbox.io/s/cd4erk?file=%2FApp.js&from-sandpack=true)에서 직접 코드를 작성할 수 있습니다.)

```js
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

이미지

> **정답**

```js
function Item({ name, isPacked }) {
  return (
    <li className="item">
      {name} {isPacked ? '✔' : '❌'}
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

이미지

([CodeSandbox](https://codesandbox.io/s/8zscn7?file=%2FApp.js&from-sandpack=true)에서 정답을 확인할 수 있습니다.)

> ### 도전 2: `&&`를 이용해 아이템 중요도 보여주기
>
> **도전 2: `&&`를 이용해 아이템 중요도 보여주기**
>
> 이 예시에서, 각각의 `Item`은 숫자형의 `importance` prop을 받습니다. 0이 아닌 중요도를 가진 아이템에만 이탤릭체로 "(중요도:X)"로 렌더링하기 위해서 `&&` 연산자를 사용하세요. 아이템 목록은 아래와 같이 끝나야 합니다:
> - Space suit (Importance: 9)
> - Helmet with a golden leaf
> - Photo of Tam (Importance: 6)
> 두 라벨 사이에 공간을 추가하는 것을 잊지 마세요!

([CodeSandbox](https://codesandbox.io/s/wvs5jk?file=%2FApp.js&from-sandpack=true)에서 직접 코드를 작성할 수 있습니다.)

```js
function Item({ name, importance }) {
  return (
    <li className="item">
      {name}
    </li>
  );
}

export default function PackingList() {
  return (
    <section>
      <h1>Sally Ride's Packing List</h1>
      <ul>
        <Item 
          importance={9} 
          name="Space suit" 
        />
        <Item 
          importance={0} 
          name="Helmet with a golden leaf" 
        />
        <Item 
          importance={6} 
          name="Photo of Tam" 
        />
      </ul>
    </section>
  );
}
```

이미지

> **정답**
>
> 아래와 같이 하면 효과가 있습니다:

([CodeSandbox](https://codesandbox.io/s/fnswhh?file=%2FApp.js&from-sandpack=true)에서 정답을 확인할 수 있습니다.)

```js
function Item({ name, importance }) {
  return (
    <li className="item">
      {name}
      {importance > 0 && ' '}
      {importance > 0 &&
        <i>(Importance: {importance})</i>
      }
    </li>
  );
}

export default function PackingList() {
  return (
    <section>
      <h1>Sally Ride's Packing List</h1>
      <ul>
        <Item 
          importance={9} 
          name="Space suit" 
        />
        <Item 
          importance={0} 
          name="Helmet with a golden leaf" 
        />
        <Item 
          importance={6} 
          name="Photo of Tam" 
        />
      </ul>
    </section>
  );
}
```

이미지

> `0`이 렌더링되지 않아야 한다면 `importance`가 `0`이 있는 경우 `importance && ...`처럼 작성하지 않고 `importance > 0 && ...`처럼 작성해야 한다는 것을 기억하세요.
>
> 이 해결방안에서는 두 분리된 조건들이 이름과 중요도 라벨 사이에 공간을 넣는 데 사용됩니다. 대안으로 `importance > 0 && <> <i>...</i></>`같이 fragment를 사용해 공간을 넣거나 `importance > 0 && <i> ...</i>` 같이 `<i>` 속에 직접 공간을 넣을 수 있습니다.

> ### 도전 3: 일련의 `? :` 코드를 `if`와 변수들로 리팩토링하기
>
> **도전 3: 일련의 `? :` 코드를 `if`와 변수들로 리팩토링하기**
>
> 이 `Drink` 컴포넌트는 `name` prop이 `"tea"` 또는 `"coffee"`인지에 따라서 다른 정보를 보여주기 위해 일련의 `? :` 조건을 사용합니다. 문제는 각각의 음료에 대한 정보가 다양한 조건들에 걸쳐 있습니다. 삼항 `? :` 조건 대신에 하나의 `if` 문구만을 사용하는 코드로 리팩토링하세요.

([CodeSandbox](https://codesandbox.io/s/vnyc4c?file=%2FApp.js&from-sandpack=true)에서 직접 코드를 작성할 수 있습니다.)

```js
function Drink({ name }) {
  return (
    <section>
      <h1>{name}</h1>
      <dl>
        <dt>Part of plant</dt>
        <dd>{name === 'tea' ? 'leaf' : 'bean'}</dd>
        <dt>Caffeine content</dt>
        <dd>{name === 'tea' ? '15–70 mg/cup' : '80–185 mg/cup'}</dd>
        <dt>Age</dt>
        <dd>{name === 'tea' ? '4,000+ years' : '1,000+ years'}</dd>
      </dl>
    </section>
  );
}

export default function DrinkList() {
  return (
    <div>
      <Drink name="tea" />
      <Drink name="coffee" />
    </div>
  );
}

```

이미지

> `if`를 사용해 코드를 리팩토링하면서 코드를 단순화하는 방법들에 대해 더 많은 생각을 할 수 있었나요?

> **정답**
>
> 이 문제를 해결할 여러 방식들이 있지만 아래는 그 중 하나의 답입니다:

([CodeSandbox](https://codesandbox.io/s/eyqfti?file=%2FApp.js&from-sandpack=true)에서 정답을 확인할 수 있습니다.)

```js
function Drink({ name }) {
  let part, caffeine, age;
  if (name === 'tea') {
    part = 'leaf';
    caffeine = '15–70 mg/cup';
    age = '4,000+ years';
  } else if (name === 'coffee') {
    part = 'bean';
    caffeine = '80–185 mg/cup';
    age = '1,000+ years';
  }
  return (
    <section>
      <h1>{name}</h1>
      <dl>
        <dt>Part of plant</dt>
        <dd>{part}</dd>
        <dt>Caffeine content</dt>
        <dd>{caffeine}</dd>
        <dt>Age</dt>
        <dd>{age}</dd>
      </dl>
    </section>
  );
}

export default function DrinkList() {
  return (
    <div>
      <Drink name="tea" />
      <Drink name="coffee" />
    </div>
  );
}
```

> 각각의 음료에 대한 정보는 다양한 조건들에 걸쳐 뿌려져 있는 것 대신에 함께 묶여 있습니다. 이것은 향후 더 많은 음료들을 추가하는 것을 쉽게 만듭니다.
>
> 또다른 해결방안은 정보를 객체에 옮김으로서 조건들을 모두 없애는 것입니다:

```js
const drinks = {
  tea: {
    part: 'leaf',
    caffeine: '15–70 mg/cup',
    age: '4,000+ years'
  },
  coffee: {
    part: 'bean',
    caffeine: '80–185 mg/cup',
    age: '1,000+ years'
  }
};

function Drink({ name }) {
  const info = drinks[name];
  return (
    <section>
      <h1>{name}</h1>
      <dl>
        <dt>Part of plant</dt>
        <dd>{info.part}</dd>
        <dt>Caffeine content</dt>
        <dd>{info.caffeine}</dd>
        <dt>Age</dt>
        <dd>{info.age}</dd>
      </dl>
    </section>
  );
}

export default function DrinkList() {
  return (
    <div>
      <Drink name="tea" />
      <Drink name="coffee" />
    </div>
  );
}
```