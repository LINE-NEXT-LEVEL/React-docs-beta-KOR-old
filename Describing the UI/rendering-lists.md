# 리스트 렌더링하기

종종 수집된 데이터를 바탕으로 다양한 비슷한 컴포넌트들을 보여주고 싶을 때가 있습니다. 배열 형태의 데이터를 조작하고 싶으면 [JavaScript array methods](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array#)를 사용하면 됩니다. 이 페이지에서는 배열 형태의 데이터를 컴포넌트 배열로 필터링하고 변형시키기 위해 `filter()`과`map()`를 사용해 볼 것입니다.

 > **여러분이 배울 것들**
 > - JavaScript의 `map()`을 사용하여 배열을 컴포넌트로 렌더링하는 방법
 > - JavaScript의 `filter()`을 사용하여 특정한 컴포넌트만 렌더링하는 방법
 > - React key를 언제 사용하고 왜 사용해야 하는지

## 배열로 데이터 렌더링하기

 여기 목록 형태의 내용이 있습니다.

```HTML
<ul>
  <li>Creola Katherine Johnson: mathematician</li>
  <li>Mario José Molina-Pasquel Henríquez: chemist</li>
  <li>Mohammad Abdus Salam: physicist</li>
  <li>Percy Lavon Julian: chemist</li>
  <li>Subrahmanyan Chandrasekhar: astrophysicist</li>
</ul>
```

이 리스트 아이템 간의 유일한 차이는 내용입니다. 인터페이스를 구축할 때, 한 컴포넌트를 여러 인스턴스로 사용하면서 다른 데이터들을 사용하곤 합니다: 댓글 목록부터 프로필 이미지 갤러리까지 다양한 예시가 있습니다. 이런 상황에서는 JavaScript객체와 배열 안의 데이터를 저장하고 `map()`이나`filter()`같은 메소드를 사용해서 데이터를 가진 컴포넌트 목록을 렌더링할 수 있습니다.

배열로 아이템 목록을 생성하는 방법의 짧은 예시입니다: 

1. 배열로 데이터 **옮기기**:

```JavaScript
const people = [
  'Creola Katherine Johnson: mathematician',
  'Mario José Molina-Pasquel Henríquez: chemist',
  'Mohammad Abdus Salam: physicist',
  'Percy Lavon Julian: chemist',
  'Subrahmanyan Chandrasekhar: astrophysicist'
];
```

2. `people`의 멤버들을 새로운 JSX node 배열인 `listItems`로 **매핑**하기:  

```JSX
const listItems = people.map(person => <li>{person}</li>);
```

3. `<ul>`로 `listItems`를 감싸서 컴포넌트에서 `리턴`시켜주기:

```JSX
return <ul>{listItems}</ul>;
```

결과물은 이렇습니다:

```JSX
const people = [
  'Creola Katherine Johnson: mathematician',
  'Mario José Molina-Pasquel Henríquez: chemist',
  'Mohammad Abdus Salam: physicist',
  'Percy Lavon Julian: chemist',
  'Subrahmanyan Chandrasekhar: astrophysicist'
];

export default function List() {
  const listItems = people.map(person =>
    <li>{person}</li>
  );
  return <ul>{listItems}</ul>;
}
```

[CodeSandbox](https://codesandbox.io/s/0zipqx?file=/App.js&from-sandpack=true)에서 직접 코드를 작성할 수 있습니다.

## 아이템 배열 필터링하기

이 데이터들을 좀 더 구조화될 수 있습니다.

```JavaScript
const people = [{
  id: 0,
  name: 'Creola Katherine Johnson',
  profession: 'mathematician',
}, {
  id: 1,
  name: 'Mario José Molina-Pasquel Henríquez',
  profession: 'chemist',
}, {
  id: 2,
  name: 'Mohammad Abdus Salam',
  profession: 'physicist',
}, {
  name: 'Percy Lavon Julian',
  profession: 'chemist',  
}, {
  name: 'Subrahmanyan Chandrasekhar',
  profession: 'astrophysicist',
}];
```

직업이 `chemist`인 사람들만 보여주고 싶다고 가정해 봅시다. 그 사람들만 리턴해주기 위해서 JavaScript의 `filter()`메소드를 사용할 수 있습니다. 이 메소드는 아이템 배열들을 받아들이고, 테스트(`true`또는`false`값을 리턴해주는 함수)로 전달합니다. 그리고 나서, 테스트를 통과(`true`를 리턴)한 아이템들로만 새로운 배열을 만들어서 다시 리턴해줍니다. 

여러분은 `직업(profession)`이 `화학자(chemist)`인 아이템만 원합니다. 이를 검증하기 위한 "테스트" 함수는 `(person) => person.profession === 'chemist'`이렇게 생겼습니다. 같이 합쳐봅시다:

1. `person.profession === 'chemist'`로 걸러져야 할 `사람들`에 `filter()`를 불러서 "화확자"인 사람들만 있는 새 배열인 `chemists`을 **생성**합니다.

```JavaScript
const chemists = people.filter(person =>
  person.profession === 'chemist'
);
```

2.이제 `화학자`로 **매핑**합니다.

```JSX
const listItems = chemists.map(person =>
  <li>
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
```

3.마지막으로 컴포넌트에서 `listItems`를 리턴해줍니다.

```JSX
return <ul>{listItems}</ul>;
```

```JSX
//App.js
import { people } from './data.js';
import { getImageUrl } from './utils.js';

export default function List() {
  const chemists = people.filter(person =>
    person.profession === 'chemist'
  );
  const listItems = chemists.map(person =>
    <li>
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
  return <ul>{listItems}</ul>;
}
```

```JavaScript
//data.js
export const people = [{
  id: 0,
  name: 'Creola Katherine Johnson',
  profession: 'mathematician',
  accomplishment: 'spaceflight calculations',
  imageId: 'MK3eW3A'
}, {
  id: 1,
  name: 'Mario José Molina-Pasquel Henríquez',
  profession: 'chemist',
  accomplishment: 'discovery of Arctic ozone hole',
  imageId: 'mynHUSa'
}, {
  id: 2,
  name: 'Mohammad Abdus Salam',
  profession: 'physicist',
  accomplishment: 'electromagnetism theory',
  imageId: 'bE7W1ji'
}, {
  id: 3,
  name: 'Percy Lavon Julian',
  profession: 'chemist',
  accomplishment: 'pioneering cortisone drugs, steroids and birth control pills',
  imageId: 'IOjWm71'
}, {
  id: 4,
  name: 'Subrahmanyan Chandrasekhar',
  profession: 'astrophysicist',
  accomplishment: 'white dwarf star mass calculations',
  imageId: 'lrWQx8l'
}];
```

```JavaScript
export function getImageUrl(person) {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    's.jpg'
  );
}
```

[CodeSandbox](https://codesandbox.io/s/6ki8d9?file=/utils.js&from-sandpack=true)에서 직접 코드를 작성할 수 있습니다.

## 주의할 점

화살표 함수는 `=>` 바로 다음의 표현을 내부적으로 리턴해줍니다. 그래서 따로 `return`을 명시해줄 필요가 없습니다:

```JSX
const listItems = chemists.map(person =>
  <li>...</li> // Implicit return!
);
```

하지만 **`=>`뒤에 중괄호({})가 따라오면 명시적으로 `return`을 써줘야 합니다!**

```JSX
const listItems = chemists.map(person => { // Curly brace
  return <li>...</li>;
});
```

`=> {`을 갖고 있는 화살표 함수는 ["block body"](https://beta.reactjs.org/learn/rendering-lists#:~:text=to%20have%20a-,%E2%80%9Cblock%20body%E2%80%9D,-.%20They%20let%20you)를 갖고 있다고 합니다. block body는 한 줄 이상의 코드를 쓰게 해 주지만, `return`을 직접 써줘야 합니다. 잊어버리면 아무것도 리턴되지 않습니다!

## `key`로 순서대로 있는 아이템 목록을 유지하기

새 탭에서 위에 있는 샌드박스 아무거나 열어본다면, 콘솔창에 에러를 볼 수 있을 것입니다.

아이템 배열에는 `key`를 주어야 합니다 — 그 배열에 있는 다른 아이템들과 구별해줄 수 있는 string이나 숫자입니다.

```HTML
<li key={person.id}>...</li>
```

## 노트

> `map()` 바로 안에 있는 JSX element들은 항상 key가 필요합니다!

key들은 나중에 짝을 지을 수 있도록 아이템 배열의 어떤 아이템이 React의 컴포넌트에 상응하는지 알려줍니다. key는 배열 아이템들이 움직이거나(분류 등), 삽입이 되거나, 제거될 때 중요해집니다. 잘 선택된 `key`는 React에게 정확히 무엇이 일어났는지 알려주고 DOM 트리를 적절하게 업데이트하게 해줍니다.

즉석으로 키를 생성하는 것보다, 데이터 안에 키를 포함시켜야 합니다:

```JSX
//App.js
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
        <b>{person.name}</b>
          {' ' + person.profession + ' '}
          known for {person.accomplishment}
      </p>
    </li>
  );
  return <ul>{listItems}</ul>;
}
```

```JavaScript
//data.js
export const people = [{
  id: 0, // Used in JSX as a key
  name: 'Creola Katherine Johnson',
  profession: 'mathematician',
  accomplishment: 'spaceflight calculations',
  imageId: 'MK3eW3A'
}, {
  id: 1, // Used in JSX as a key
  name: 'Mario José Molina-Pasquel Henríquez',
  profession: 'chemist',
  accomplishment: 'discovery of Arctic ozone hole',
  imageId: 'mynHUSa'
}, {
  id: 2, // Used in JSX as a key
  name: 'Mohammad Abdus Salam',
  profession: 'physicist',
  accomplishment: 'electromagnetism theory',
  imageId: 'bE7W1ji'
}, {
  id: 3, // Used in JSX as a key
  name: 'Percy Lavon Julian',
  profession: 'chemist',
  accomplishment: 'pioneering cortisone drugs, steroids and birth control pills',
  imageId: 'IOjWm71'
}, {
  id: 4, // Used in JSX as a key
  name: 'Subrahmanyan Chandrasekhar',
  profession: 'astrophysicist',
  accomplishment: 'white dwarf star mass calculations',
  imageId: 'lrWQx8l'
}];
```

```JavaScript
//util.js
export function getImageUrl(person) {
  return (
    'https://i.imgur.com/' +
    person.imageId +
    's.jpg'
  );
}
```

[CodeSandbox](https://codesandbox.io/s/etqusf?file=/utils.js&from-sandpack=true)에서 직접 코드를 작성할 수 있습니다.

## Deep Dive

### 각 리스트 아이템에 여러 DOM 노드들을 보여주기

각 아이템이 보여주어야 할 게 하나가 아니라 여러개의 DOM 노드일때는 어떻게 해야할까요?

짧은 `<>``</>` 구문으로는 키를 전달할 수 없기 때문에 `<div>`로 그룹화하거나 약간 더 길고 더 명시적인 `<Fragment>`구문을 사용해줄 수 있습니다.

```JSX
import { Fragment } from 'react';

// ...

const listItems = people.map(person =>
  <Fragment key={person.id}>
    <h1>{person.name}</h1>
    <p>{person.bio}</p>
  </Fragment>
);
```

Fragment는 DOM에서 사라지고 납작한 `<h1>`,`<p>`,`<h1>`,`<p>` 만 말들어줄 것 입니다.

## `key`를 어디서 얻을 것인가

데이터 소스에 따라 key값이 달라집니다:

- 데이터베이스에서 가져온 데이터: 데이터가 데이터베이스에서 온 것이라면,원래 유일한 값인 데이터베이스의 key/ID를 사용하면 됩니다. 
- 현재 환경에서 만들어진 데이터: 데이터가 현재 환경에서 생성되고 유지되는 경우(예시. 노트 필기앱의 노트), 아이템을 만들 때 `crypto`나`uuid`같은 패키지를 이용해서 증가하는 숫자를 사용하세요.

## Key 규칙들

- key는 형재/자매들 간에 특별한 값이어야 합니다. 다른 배열 상의 JSX노드에서 같은 값을 사용하는 것은 괜찮습니다.
- key는 불변성을 갖고 있어야 합니다. 변하면 key의 목적이 훼손됩니다. 렌더링하는 동안 key를 생성하지 마세요.

## React는 key가 왜 필요할까?

데스크탑의 파일들이 이름이 없다고 상상해보세요. 대신, 파일을 확인하려면 순서대로 확인해야 합니다. — 첫 번째 파일, 두 번째 파일 같은 식이 될 것입니다. 익숙해질 수야 있지만, 한 번 파일을 삭제하면 혼란스러울 것입니다. 두 번째가 첫 파일이 되고, 세 번째 파일이 두번째 파일이 되기 때문입니다.
