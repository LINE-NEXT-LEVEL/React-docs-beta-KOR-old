# React에 대해 생각해보기

React는 여러분이 보고 있는 디자인과 여러분이 만든 앱에 대한 사고방식을 바꿀 수 있습니다. 이전에는 숲을 보았다면 React를 사용하고 나서부터는 각각의 나무를 볼 수 있습니다. React는 디자인과 UI를 더 쉽게 생각할 수 있게 만들어줍니다. 이 튜토리얼은 React로 상퓸표 검색대를 만드는 과정을 안내합니다.

## mockup으로 시작하기

여러분이 이미 JSON API를 갖고 있고, 디자이너에게서 시안을  받았다고 가정해 봅시다.

JSON API는 아래와 같은 데이터를 반환합니다.

```javascript
[
  { category: "Fruits", price: "$1", stocked: true, name: "Apple" },
  { category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit" },
  { category: "Fruits", price: "$2", stocked: false, name: "Passionfruit" },
  { category: "Vegetables", price: "$2", stocked: true, name: "Spinach" },
  { category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin" },
  { category: "Vegetables", price: "$1", stocked: true, name: "Peas" }
]
```

시안(mockup)은 아래와 같습니다.

<img width="298" alt="image" src="https://user-images.githubusercontent.com/55529617/183777211-927853e8-a37a-4e13-9d42-ae3ee1541729.png">

React에서 UI를 실행시키기 위해서는 일반적으로 다섯 단계들을 따르면 됩니다.

## 단계1: UI를 컴포넌트 계층 구조로 나눕니다

시안에 모든 컴포넌트와 서브컴포넌트 주위에 박스를 그리고 이름을 지어주는 것으로 시작합니다. 만약 여러분이 디자이너와 함께 일한다면 디자이너가 디자인툴에 이미 컴포넌트들에 이름을 지었을 수도 있습니다. 디자이너들과 함께 확인해보세요!

디자인은 여러분의 배경지식에 따라 다양한 방식으로 컴포넌트로 분리될 수 있습니다.

- Programming - 새로운 함수나 객체를 만드는 경우 사용하는 기술과 같은 것을 사용합니다. 예를 들어, 컴포넌트는 한가지 일만 해야 한다는 단일책임원칙이 있습니다. 이 컴포넌트가 점차 커진다면 더 작은 서브컴포넌트들로 분해되어야 합니다.
- CSS - 클래스 선택자로 무엇을 선택할지 고려해봅니다. (하지만, 컴포넌트는 덜 세분화합니다)
- Design - 디자인 레이어를 어떻게 구성할지 고려해봅니다.

만약 JSON이 잘 구조화되어있다면 여러분은 JSON이 UI 컴포넌트 구조와 자연스럽게 매핑된다는 것을 발견할 수 있습니다. 그 이유는 UI와 데이터 구조는 종종 같은 정보 설계(즉, 같은 형태)를 가지고 있기 때문입니다. 데이터 구조와 하나씩 매칭되는 각각의 컴포넌트는 UI에서 컴포넌트로 분리합니다.

아래 화면에는 다섯개의 컴포넌트들이 있습니다.

<img width="403" alt="image" src="https://user-images.githubusercontent.com/55529617/183777241-fdf7d4f9-524a-416c-a529-7f30bebc1aa1.png">

1. `FilterableProductTable` (회색)은 전체 app을 감싸고 있습니다.
2. `SearchBar` (파란색)은 사용자 입력을 받고 있습니다.
3. `ProductTable` (보라색)은 사용자 입력과 관련된 목록을 보여주고 있습니다.
4. `ProductCategoryRow` (초록색)은 각각의 범주에 대한 제목을 표시하고 있습니다.
5. `ProductRow` (노란색)은 각각의 상품이 적힌 행을 표시하고 있습니다.

`ProductTable`(보라색)을 보면 표 제목("Name"과 "Price"를 포함)이 컴포넌트로 이루어지지 않았다는 것을 볼 수 있습니다. 이것은 선호도의 문제이며 다른 방식이어도 괜찮습니다. 이 예시에서는 그 제목이 `ProductTable`의 목록 안에 있었기 때문에 `ProductTable`의 일부로 지정했습니다. 하지만, 만약 이 제목이 너무 복잡해진다면 `ProductTableHeader` 컴포넌트로 분리하는 것도 좋습니다.

이제 시안에서 컴포넌트를 확립했으므로 계층을 정립합니다. 시안에서 컴포넌트 내부에 있는 컴포넌트들은 계층에서 자식으로 나타납니다.

- `FilterableProductTable`
    - `SearchBar`
    - `ProductTable`
        - `ProductCategoryRow`
        - `ProductRow`

## 단계2: React에서 정적인 버전을 빌드합니다

이제 컴포넌트 계층이 만들어졌으므로 앱을 실행시킬 시간입니다. 가장 직관적인 방식은 어떠한 상호작용 없이 데이터 구조에 맞는 UI를 렌더링하는 버전을 빌드하는 것입니다. 정적인 버전을 우선 빌드하고나서 상호작용을 분리해서 추가하는 것이 보통 쉽습니다. 정적인 버전은 많은 타이핑과 적은 사고를 필요로 하지만 상호작용을 추가하는 것은 많은 사고와 적은 타이핑을 필요로 합니다.

데이터 구조를 렌더링하는 정적인 버전의 앱을 빌드하기 위해서는 다른 컴포넌트들을 재사용하고 [props](https://beta.reactjs.org/learn/passing-props-to-a-component)를 사용해 데이터를 넘기는 [컴포넌트](https://beta.reactjs.org/learn/your-first-component)들을 만들어야 합니다. props는 부모에서 자식으로 데이터를 넘기는 방식입니다. (여러분이 상태 개념에 친숙하다면 이 정적인 버전을 빌드할 때 상태를 사용하지 마세요. 상태는 오직 상호작용에 사용되는데, 즉 데이터가 계속해서 바뀔 때 사용됩니다. 지금은 앱의 정적인 버전을 만들기 때문에 상태가 필요하지 않습니다.)

계층에서 `FilterableProductTable`과 같은 높은 컴포넌트들부터 만들기 시작하여 "top down"방식으로 빌드할 수 있고 `ProductRow`와 같은 낮은 컴포넌트들부터 만들어 'bottom up'방식으로도 빌드할 수 있습니다. 단순한 예제들에서 보통 top-down 방식이 적합하고 큰 프로젝트에서 bottom-up 방식이 더 쉽습니다.

```javascript
function ProductCategoryRow({ category }) {
  return (
    <tr>
      <th colSpan="2">
        {category}
      </th>
    </tr>
  );
}

function ProductRow({ product }) {
  const name = product.stocked ? product.name :
    <span style={{ color: 'red' }}>
      {product.name}
    </span>;

  return (
    <tr>
      <td>{name}</td>
      <td>{product.price}</td>
    </tr>
  );
}

function ProductTable({ products }) {
  const rows = [];
  let lastCategory = null;

  products.forEach((product) => {
    if (product.category !== lastCategory) {
      rows.push(
        <ProductCategoryRow
          category={product.category}
          key={product.category} />
      );
    }
    rows.push(
      <ProductRow
        product={product}
        key={product.name} />
    );
    lastCategory = product.category;
  });

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>{rows}</tbody>
    </table>
  );
}

function SearchBar() {
  return (
    <form>
      <input type="text" placeholder="Search..." />
      <label>
        <input type="checkbox" />
        {' '}
        Only show products in stock
      </label>
    </form>
  );
}

function FilterableProductTable({ products }) {
  return (
    <div>
      <SearchBar />
      <ProductTable products={products} />
    </div>
  );
}

const PRODUCTS = [
  {category: "Fruits", price: "$1", stocked: true, name: "Apple"},
  {category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit"},
  {category: "Fruits", price: "$2", stocked: false, name: "Passionfruit"},
  {category: "Vegetables", price: "$2", stocked: true, name: "Spinach"},
  {category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin"},
  {category: "Vegetables", price: "$1", stocked: true, name: "Peas"}
];

export default function App() {
  return <FilterableProductTable products={PRODUCTS} />;
}

```

<img width="772" alt="image" src="https://user-images.githubusercontent.com/55529617/183777428-4525bf6a-2885-4d34-b654-fb1497fa9292.png">

(만약 이 코드를 보는 게 겁난다면 [Quick Start](https://beta.reactjs.org/learn)를 먼저 보세요!)

컴포넌트들을 만들고 나서 여러분은 데이터 구조를 렌더링하는 재사용 가능한 컴포넌트들을 가지고 있습니다. 정적인 앱이기 때문에 그 컴포넌트들은 JSX만 반환하고 있을 것입니다. 계층에서 가가장 높은 컴포넌트(`FilterableProductTable`)는 데이터 구조를 prop으로 가지고 있습니다. 이것을 "one-way data flow"라고 부르는데 데이터가 상위 컴포넌트에서 하위 컴포넌트들로 내려가기 때문입니다.

> **경고**
> 이 시점에서 어떠한 상태값도 사용해서는 안됩니다. 다음 단계에서 사용되어야 합니다!

## 단계3: UI 상태의 작지만 완벽한 표현을 찾아냅니다

UI 상호작용을 만들기 위해 사용자들이 기본 데이터 구조를 바꿀 수 있게 만들어 주어야 합니다. 바로 여기서 상태를 사용합니다.

앱이 기억해야 하는 변화하는 데이터의 최소단위를 상태로 생각하세요. 상태를 만들 때 가장 중요한 원리는 [DRY(Don't Repeat Yourself)](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)를 지키는 것입니다. 앱이 필요한 상태의 최소단위를 알아내고 그때 그때 필요한 다른 모든 것들을 계산하세요. 예를 들어, 쇼핑 목록을 만든다면 아이템 목록을 상태로 저장할 수 있습니다. 목록의 아이템 수를 표시하고 싶다면 또 다른 상태값으로 아이템 갯수를 저장하지 말고 그 목록의 길이를 읽으면 됩니다.

만들고 있는 앱 속 모든 데이터 조각들을 생각해 보세요.

1. 상품들 목록
2. 사용자가 입력한 검색문구
3. 체크박스의 체크여부
4. 필터링된 상품목록

위의 것들 중 어떤 것이 상태가 될까요? 상태인 것과 아닌 것을 구분해 봅시다:

- 변하지 않나요? 만약 그렇다면, 상태가 아닙니다.
- props로 부모에게서 받아오나요? 만약 그렇다면, 상태가 아닙니다.
- 컴포넌트에서 이미 존재하는 상태 또는 props에서 계산되어지나요? 만약 그렇다면, *절대* 상태가 아닙니다!

위 조건에 맞지 않는 것들이 아마 상태가 될 수 있을 것입니다.

하나하나 보면서 다시 살펴봅시다:

1. 상품 목록은 props로 보내지기 때문에 상태가 아닙니다.
2. 검색문구는 상태로 보입니다. 시간이 지나서 변할 수 있고 어떤 것에서도 계산되어지지 않기 때문입니다.
3. 체크박스 체크여부는 상태로 보입니다. 시간이 지나서 변할 수 있고 어떤 것에서도 계산되어지지 않기 때문입니다.
4. 필터링된 상품목록은 상태가 아닙니다. 그 이유는 기본 상품 목록을 알고 있고 검색 문구와 체크박스 체크여부에 따라 기본 상품 목록을 필터링하면 도출해낼 수 있기 때문입니다.

검색문구와 체크박스의 체크여부만이 상태로 판명났습니다! 잘 따라오셨습니다!

> 더 알아보기
>
> **Props vs State**
>
> React에는 데이터를 담는 두가지 모델이 있습니다: props와 state. 이 둘은 매우 다릅니다:
> Props는 함수에 넘기는 매개변수와 같습니다. Props는 부모 컴포넌트가 자식 컴포넌트로 데이터를 넘기고 부모 컴포넌트의 표시를 커스터마이징 할 수 있도록 합니다. 예를 들어, `Form`은 `Button`에 `color` prop을 넘깁니다.
>
> State는 컴포넌트의 메모리와 같습니다. 컴포넌트가 어떤 정보를 추적하고 상호작용에 맞춰 변화할 수 있도록 해줍니다. 예를 들어, `Button`은 `isHovered` 상태를 계속해서 추적합니다.
>
>Props와 상태는 다르지만 함께 동작합니다. 부모 컴포넌트는 상태(변화가 가능)에 정보를 저장하고 이것을 props로 자식 컴포넌트에 내려보냅니다. 이 글을 읽은 후에 둘의 차이가 여전히 헷갈려도 괜찮습니다. 개념이 정확히 자리잡을 때까지 약간의 연습이 필요합니다.

## 단계4: 상태가 어디에 있어야 하는지 결정합니다

앱의 최소한의 상태들을 확인한 후 어떤 컴포넌트가 이 상태를 변경하거나 소유할 책임이 있는지 알아낼 필요가 있습니다. React는 데이터를 상위 컴포넌트에서 하위 컴포넌트들로 내려보내는 "One-Way Data Flow"를 사용한다는 것을 기억하세요. 어떤 컴포넌트가 무슨 상태를 소유할지 명백하지 않을 수 있습니다. 만약 여러분이 이 개념이 처음이라면 어려울 수 있지만,아래 단계들을 따라하면서 이해할 수 있습니다!

앱 속 각각의 상태에 대해서:

1. 상태를 기반으로 렌더링하는 모든 컴포넌트를 확인합니다.
2. 그 컴포넌트들의 가까운 공통 부모컴포넌트(계층에서 컴포넌트들 모두의 위에 있는 컴포넌트)를 찾습니다.
3. 상태가 어디에 있어야 할지 결정합니다:

  - 공통 부모에 바로 상태를 넣을 수도 있습니다.
  - 공통 부모보다 상위의 컴포넌트에 상태를 넣을 수도 있습니다.
  - 상태를 보유하는 데 적합한 컴포넌트를 찾지 못했다면 상태만을 가지고 있는 새로운 컴포넌트를 만들어서 공통부모 컴포넌트 상위 계층 어딘가에 추가합니다.

이전 단계에서 이 앱의 두가지 상태들(검색 문구와 체크박스의 체크여부)을 찾았습니다. 이 예시에서는 두 가지 상태들이 항상 함께 나타난다면 하나의 상태로 생각하는 게 더 쉬울 수 있습니다.

두 상태들(검색 문구와 체크박스의 체크여부)에 대한 전략을 살펴봅시다:

1. 상태를 사용하는 컴포넌트들을 확인합니다:

  - `ProductTable`은 상태에 따라서 상품 목록을 필터링할 필요가 있습니다. (검색 문구와 체크박스의 체크여부)
  - `SearchBar`는 해당 상태값을 표시할 필요가 있습니다. (검색 문구와 체크박스의 체크여부)

2. 공통 부모를 찾습니다: 두 컴포넌트들의 가까운 공통 부모컴포넌트는 `FilterableProductTable`입니다.
3. 상태가 어디에 있을지 결정합니다: 검색 문구와 체크박스의 체크여부를 `FilterableProductTable`에 둡니다.

결론적으로 `FilterableProductTable`에 상태들을 두게 되었습니다.

[useState() hook](https://beta.reactjs.org/apis/usestate)으로 컴포넌트에 상태를 추가합니다. hook은 컴포넌트의 [렌더링주기](https://beta.reactjs.org/learn/render-and-commit)에 끼어들 수 있게 해줍니다. `FilterableProductTable`의 상단에 두 상태변수들을 추가하고 앱의 초기 상태값을 정합니다:

```javascript
function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);
```

그 다음, `ProductTable`과 `SearchBar`에 prop으로 `filterText`와 `inStockOnly`를 넘깁니다.

```JSX
<div>
  <SearchBar 
    filterText={filterText} 
    inStockOnly={inStockOnly} />
  <ProductTable 
    products={products}
    filterText={filterText}
    inStockOnly={inStockOnly} />
</div>
```

어떻게 앱이 작동하는지 볼 수 있습니다. `filterText`의 초기값을 `useState('')` 에서 `useState('fruit')`으로 [Code Sandbox](https://codesandbox.io/s/m6znel?file=/App.js&from-sandpack=true)에서 바꾸어 보세요. 검색 문구와 표가 모두 업데이트되는 것을 볼 수 있습니다.

```javascript
import { useState } from 'react';

function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState(''); // useState('fruit')으로 바꾸어보기
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar 
        filterText={filterText} 
        inStockOnly={inStockOnly} />
      <ProductTable 
        products={products}
        filterText={filterText}
        inStockOnly={inStockOnly} />
    </div>
  );
}

function ProductCategoryRow({ category }) {
  return (
    <tr>
      <th colSpan="2">
        {category}
      </th>
    </tr>
  );
}

function ProductRow({ product }) {
  const name = product.stocked ? product.name :
    <span style={{ color: 'red' }}>
      {product.name}
    </span>;

  return (
    <tr>
      <td>{name}</td>
      <td>{product.price}</td>
    </tr>
  );
}

function ProductTable({ products, filterText, inStockOnly }) {
  const rows = [];
  let lastCategory = null;

  products.forEach((product) => {
    if (
      product.name.toLowerCase().indexOf(
        filterText.toLowerCase()
      ) === -1
    ) {
      return;
    }
    if (inStockOnly && !product.stocked) {
      return;
    }
    if (product.category !== lastCategory) {
      rows.push(
        <ProductCategoryRow
          category={product.category}
          key={product.category} />
      );
    }
    rows.push(
      <ProductRow
        product={product}
        key={product.name} />
    );
    lastCategory = product.category;
  });

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>{rows}</tbody>
    </table>
  );
}

function SearchBar({ filterText, inStockOnly }) {
  return (
    <form>
      <input 
        type="text" 
        value={filterText} 
        placeholder="Search..."/>
      <label>
        <input 
          type="checkbox" 
          checked={inStockOnly} />
        {' '}
        Only show products in stock
      </label>
    </form>
  );
}

const PRODUCTS = [
  {category: "Fruits", price: "$1", stocked: true, name: "Apple"},
  {category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit"},
  {category: "Fruits", price: "$2", stocked: false, name: "Passionfruit"},
  {category: "Vegetables", price: "$2", stocked: true, name: "Spinach"},
  {category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin"},
  {category: "Vegetables", price: "$1", stocked: true, name: "Peas"}
];

export default function App() {
  return <FilterableProductTable products={PRODUCTS} />;
}
```

useState('')|useState('fruit')
------|---
|<img width="774" alt="image" src="https://user-images.githubusercontent.com/55529617/183777661-757a4f74-a049-4c27-82bf-9c35f0e2b0ac.png">|<img width="772" alt="image" src="https://user-images.githubusercontent.com/55529617/183777725-b4899d19-bc7e-4f11-b18e-aaa1c3a5be24.png">|

Sandbox에서 `ProductTable`과 `SearchBar`는 표, 입력, 체크박스를 렌더링하가ㅣ 위해 `filterText`와 `inStockOnly` props를 사용합니다. 예를 들어, 아래 코드는 어떻게 `SearchBar`가 입력값을 만들어내는지 보여줍니다:

```javascript
function SearchBar({ filterText, inStockOnly }) {
  return (
    <form>
      <input 
        type="text" 
        value={filterText} // filterText를 기본 입력값으로 받고 있습니다
        placeholder="Search..."/>
```

React가 어떻게 상태를 사용하고 React로 앱을 구성하는 방식에 대해 더 알고 싶다면 [상태 관리 글](https://beta.reactjs.org/learn/managing-state)을 참고하세요.

## 단계5: 반대되는 데이터 흐름을 추가합니다

현재까지 앱은 props와 상태를 정확히 계층 아래로 보내면서 렌더링하고 있습니다. 사용자 입력에 따라 상태를 변화시키기 위해서는 다른 방식으로 데이터 흐름을 지원할 필요가 있습니다: 계층 깊숙이 있는 form 컴포넌트는 `FilterableProductTable`에 있는 상태를 업데이트할 필요가 있습니다.

React는 props와 상태를 계층 아래로 보내는 데이터흐름을 가지고 있지만 약간의 타이핑으로 양방향 데이터 바인딩을 만들 수 있습니다. 위 Sandbox에서 무언가 입력하거나 체크박스를 체크했을 때, React가 무시하는 걸 볼 수 있습니다. 의도적인 부분입니다. `<input value={filterText} />`를 쓰면서 `input`의 prop인 `value`가 `FilterableProductTable`에서 보내지는 `filterText` 상태와 항상 동일하도록 설정했습니다. `filterText`가 새롭게 업데이트되지 않기 때문에 입력값이 절대 변하지 않습니다.

사용자가 입력을 변경시킬 때마다 해당 변화들을 반영시키기 위해 상태를 업데이트하고 싶습니다. 상태는 `FilterableProductTable`에서 가지고 있으므로 `FilterableProductTable`에서 `setFilterText`와 `setInStockOnly`를 불러올 수 있습니다. `SearchBar`에서 `FilterableProductTable`의 상태를 업데이트하기 위해서는 `SearchBar`에 set 함수들을 넘길 필요가 있습니다.

```javascript
function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar 
        filterText={filterText} 
        inStockOnly={inStockOnly}
        onFilterTextChange={setFilterText}
        onInStockOnlyChange={setInStockOnly} />
```

`SearchBar` 속에서 부모상태를 재설정하는 `onChange` 이벤트 핸들러를 추가합니다.

```JSX
<input 
  type="text" 
  value={filterText} 
  placeholder="Search..." 
  onChange={(e) => onFilterTextChange(e.target.value)} />
```

이제 앱이 완벽히 동작합니다! (참고: [Sandbox](https://codesandbox.io/s/qd3rix?file=%2FApp.js&from-sandpack=true))

```javascript
import { useState } from 'react';

function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar 
        filterText={filterText} 
        inStockOnly={inStockOnly} 
        onFilterTextChange={setFilterText} 
        onInStockOnlyChange={setInStockOnly} />
      <ProductTable 
        products={products} 
        filterText={filterText}
        inStockOnly={inStockOnly} />
    </div>
  );
}

function ProductCategoryRow({ category }) {
  return (
    <tr>
      <th colSpan="2">
        {category}
      </th>
    </tr>
  );
}

function ProductRow({ product }) {
  const name = product.stocked ? product.name :
    <span style={{ color: 'red' }}>
      {product.name}
    </span>;

  return (
    <tr>
      <td>{name}</td>
      <td>{product.price}</td>
    </tr>
  );
}

function ProductTable({ products, filterText, inStockOnly }) {
  const rows = [];
  let lastCategory = null;

  products.forEach((product) => {
    if (
      product.name.toLowerCase().indexOf(
        filterText.toLowerCase()
      ) === -1
    ) {
      return;
    }
    if (inStockOnly && !product.stocked) {
      return;
    }
    if (product.category !== lastCategory) {
      rows.push(
        <ProductCategoryRow
          category={product.category}
          key={product.category} />
      );
    }
    rows.push(
      <ProductRow
        product={product}
        key={product.name} />
    );
    lastCategory = product.category;
  });

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>{rows}</tbody>
    </table>
  );
}

function SearchBar({
  filterText,
  inStockOnly,
  onFilterTextChange,
  onInStockOnlyChange
}) {
  return (
    <form>
      <input 
        type="text" 
        value={filterText} placeholder="Search..." 
        onChange={(e) => onFilterTextChange(e.target.value)} />
      <label>
        <input 
          type="checkbox" 
          checked={inStockOnly} 
          onChange={(e) => onInStockOnlyChange(e.target.checked)} />
        {' '}
        Only show products in stock
      </label>
    </form>
  );
}

const PRODUCTS = [
  {category: "Fruits", price: "$1", stocked: true, name: "Apple"},
  {category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit"},
  {category: "Fruits", price: "$2", stocked: false, name: "Passionfruit"},
  {category: "Vegetables", price: "$2", stocked: true, name: "Spinach"},
  {category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin"},
  {category: "Vegetables", price: "$1", stocked: true, name: "Peas"}
];

export default function App() {
  return <FilterableProductTable products={PRODUCTS} />;
}
```

<img width="769" alt="image" src="https://user-images.githubusercontent.com/55529617/183777809-c7709e2c-16c9-4362-a424-025cbdf9de21.png">

이벤트 핸들링과 상태 업데이트에 대해서는 [상호작용 추가하기](https://beta.reactjs.org/learn/adding-interactivity) 부분에서 더 배울 수 있습니다.

## 다음에 배울 것

React로 컴포넌트와 앱을 만드는 사고방식에 대한 간단한 소개였습니다. 지금 [React 프로젝트 시작하기](https://beta.reactjs.org/learn/installation)를 하거나 이 튜토리얼에 사용된 [모든 구문 더 알아보기](https://beta.reactjs.org/learn/describing-the-ui)를 할 수 있습니다.
