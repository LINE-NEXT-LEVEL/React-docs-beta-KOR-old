# 웹사이트에 React 추가하기
여러분의 웹사이트 전부를 React로 만들 필요는 없습니다. HTML에 React를 추가하는 작업은 별도의 설치가 필요 없고, 1분 정도면 충분합니다. 그럼 즉시 인터랙티브한 컴포넌트를 만들 수 있게 됩니다.

> 여러분이 배울 것들
> - 1분 안에 HTML 문서에 React를 추가할 수 있는 방법
> - JSX 문법이 무엇이고 이를 빠르게 사용해볼 수 있는 방법
> - 프로덕션을 위해 JSX 전처리기를 세팅하는 방법

## 1분 안에 React 추가하기
React는 원래부터 점진적인 적용을 위해 디자인되었습니다. 대부분의 웹사이트들은 전부 React로 만들어지지 않았고, 그럴 필요도 없습니다. 이 가이드는 어떻게 이미 존재하는 HTML 문서에 '인터랙티브함'을 추가할 수 있는지를 다루고 있습니다.
여러분의 웹사이트나 [빈 HTML 파일](https://gist.github.com/gaearon/edf814aeee85062bc9b9830aeaf27b88/archive/3b31c3cdcea7dfcfd38a81905a0052dd8e5f71ec.zip)로부터 시작해도 좋습니다. 인터넷에 연결되어있고, 메모장이나 VSCode같은 텍스트 에디터만 있어도 충분합니다.(조금의 설정을 추가하면 여러분의 [에디터에 문법 하이라이팅 기능을 사용](https://beta.reactjs.org/learn/editor-setup)할 수 있습니다.)

### 1단계 : root가 될 HTML 태그 만들기
우선 여러분이 수정하고 싶은 HTML 문서를 열어주세요. 그리고 빈 `<div>` 태그를 추가해 React가 동작할 위치를 마련해줍니다(root). 방금 만든 `<div>` 태그에 유니크한 `id` 속성을 추가해주세요.

```html
<!-- ... existing HTML ... -->

<div id="like-button-root"></div>

<!-- ... existing HTML ... -->
```
이 `<div>`태그는 'root'라고 부르고, 여기서부터 React 트리가 시작됩니다. Root 태그는 HTML의 `<body>` 태그 내부라면 어디에든 존재할 수 있습니다. 태그 내부는 비워두도록 합니다. 태그 안에 여러분이 작성한 내용이 있더라도 React가 React 컴포넌트로 태그 내부를 바꿀 수 있습니다.

root가 될 태그는 꼭 하나일 필요는 없습니다. 여러분이 원하는 만큼 만들어도 괜찮습니다.

### 2단계 : script 태그 추가하기
HTML 문서의 닫는 `</body>` 태그 직전에 3개의 `<script>` 태그를 추가해야 합니다. 아래 파일들을 다운로드 받기 위함입니다.
- [`react.development.js`](https://unpkg.com/react@18/umd/react.development.js)는 여러분들이 React 컴포넌트를 만들 수 있게끔 합니다.
- [`react-dom.development.js`](https://unpkg.com/react-dom@18/umd/react-dom.development.js)는 React가 HTML element를 [DOM](https://developer.mozilla.org/docs/Web/API/Document_Object_Model)에 렌더 할 수 있도록 합니다.
- `like-button.js`은 다음 단계에서 여러분이 컴포넌트를 작성할 곳입니다.

이제 HTML 파일은 이렇게 생겼을 겁니다.
```html
 <!-- end of the page -->
    <script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>
    <script src="like-button.js"></script>
  </body>
</html>
```

> **주의사항**
> 실제 웹사이트로 배포하기 전에 `development.js`를 `production.min.js`로 바꿨는지 꼭 확인해야 합니다. React의 개발용 빌드는 에러 메시지같은 유용한 기능들을 제공하지만, 이로 인해 웹사이트의 성능이 나빠질 수 있습니다.

### 3단계 : React 컴포넌트 만들기
위에서 계속 작업하던 HTML 파일 옆에 `like-button.js` 파일을 만들어주세요. 그리고 아래 코드 조각을 작성한 후 저장하면 됩니다. 이 코드는 `LikeButton`이라고 하는 React 컴포넌트를 정의하고 있습니다.([Quick Start](https://beta.reactjs.org/learn)에서 컴포넌트 만드는 방법을 더 배워보세요!)

```js
'use strict';

function LikeButton() {
  const [liked, setLiked] = React.useState(false);

  if (liked) {
    return 'You liked this!';
  }

  return React.createElement(
    'button',
    {
      onClick: () => setLiked(true),
    },
    'Like'
  );
}
```

### 4단계 : React 컴포넌트를 페이지에 추가하기
마지막으로 아래 3줄을 `like-button.js` 파일의 맨 밑에 추가해줍니다. 이 코드들은 1단계에서 여러분이 추가한 `<div>` 태그를 HTML 파일에서 찾아 그곳에 React root를 만들고 `LikeButton` 컴포넌트를 그 안에 넣어 보여주도록 합니다.
```js
const rootNode = document.getElementById('like-button-root');
const root = ReactDOM.createRoot(rootNode);
root.render(React.createElement(LikeButton));
```

여러분은 방금 여러분의 첫 React 컴포넌트를 웹사이트에 렌더링 했습니다. 축하합니다!
- [예제의 전체 소스코드 보기](https://gist.github.com/gaearon/0b535239e7f39c524f9c7dc77c44f09e)
- [예제 전문을 다운로드 받기(2KB, 압축된 파일)](https://gist.github.com/gaearon/0b535239e7f39c524f9c7dc77c44f09e/archive/651935b26a48ac68b2de032d874526f2d0896848.zip)

**컴포넌트는 재사용이 가능합니다!**
여러분은 아마 한 HTML 페이지 내부에서도 여러 곳에 같은 React 컴포넌트를 보여주고 싶어할 수도 있습니다. React로 구성된 부분이 다른 부분들과 분리되어 있을때 유용합니다. 여러분은 그냥 HTML 문서 내부에 root 태그를 여러개 만들고, `ReactDOM.createRoot()` 함수를 통해 각각의 root 태그에 React 컴포넌트를 렌더링하면 됩니다. 예를 들어 
1. `index.html`파일 안에 또 다른 root인 `<div id="another-root"></div>`를 만듭니다.
2. `like-button.js`에 아래 3줄을 또 추가해줍니다.
    ```js
    const anotherRootNode = document.getElementById('another-root');
    const anotherRoot = ReactDOM.createRoot(anotherRootNode);
    anotherRoot.render(React.createElement(LikeButton));
    ```
만약 같은 컴포넌트를 여기저기 렌더링시키고 싶다면 `id` 대신 CSS `class`를 각 root에 붙일 수도 있습니다. 이건 [세 개의 'LikeButton'을 만들고 각각에 데이터를 넘겨주는 예제](https://gist.github.com/gaearon/779b12e05ffd5f51ffadd50b7ded5bc8)입니다.

### 5단계 : 프로덕션을 위해 JavaScript를 경량화합니다.
경량화 되지 않은 JavaScript를 사용하면 여러분의 웹사이트를 찾는 유저들이 기다려야 하는 로딩시간이 매우 길어질 수 있습니다. 웹사이트를 배포하기 전에 script들을 경량화하는걸 추천합니다.
- 여러분이 쓰는 스크립트의 '경량화 단계'가 없는 경우, [한 가지 설정 방법](https://gist.github.com/gaearon/42a2ffa41b8319948f9be4076286e1f3)을 제안합니다.
- React는 `production.min.js`로 끝나는 스크립트 파일이 경량화된 버전의 스크립트입니다. 배포된 웹사이트가 이걸 사용하는게 맞다면 프로덕션에 내보내도 좋습니다.

## React를 JSX와 함께 사용해보세요
위에서 했던 내용들은 브라우저가 기본적으로 제공하는 기능만 사용했습니다. 그래서 `like-button.js`가 JavaScript 함수를 통해서 React에게 무엇을 렌더링할지 알려줘야 했습니다.
```js
return React.createElement('button', {onClick: () => setLiked(true)}, 'Like');
```

React는 JSX라는 옵션도 제공합니다. HTML과 비슷하게 생긴 JavaScript 문법입니다.
```jsx
return <button onClick={() => setLiked(true)}>Like</button>;
```
두 코드는 완전히 동일한 내용입니다. JSX는 마크업을 JavaScript로 표현하는 인기있는 문법입니다. 많은 사람들이 이를 UI 코드를 작성하는데 있어 친숙하고 유용하게 느낍니다 - 굳이 React가 아닌 다른 라이브러리에서도 말이죠.

> 이 [online converter](https://babeljs.io/en/repl#?babili=false&browsers=&build=&builtIns=false&spec=false&loose=false&code_lz=DwIwrgLhD2B2AEcDCAbAlgYwNYF4DeAFAJTw4B88EAFmgM4B0tAphAMoQCGETBe86WJgBMAXJQBOYJvAC-RGWQBQ8FfAAyaQYuAB6cFDhkgA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=es2015%2Creact%2Cstage-2&prettier=false&targets=&version=7.17)를 통해 HTML 마크업을 JSX로 바꿀 수도 있습니다.

### JSX를 사용해보세요
JSX를 사용하는 가장 빠른 방법은 Babel 컴파일러를 `<script>` 태그로 추가하는 것입니다. `like-button.js` 이전에 코드를 한 줄 추가합니다. 그리고 `like-button.js`를 추가하는 태그에는 `type="text/babel"` 속성을 붙여주도록 합니다.

```html
<script src="https://unpkg.com/react@18/umd/react.production.min.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js" crossorigin></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script src="like-button.js" type="text/babel"></script>
</body>
```

이제 `like-button.js`를 열어 아래 코드를

```js
return React.createElement(
  'button',
  {
    onClick: () => setLiked(true),
  },
  'Like'
);
```
동일한 내용의 JSX 코드로 교체합니다.

```jsx
return (
  <button onClick={() => setLiked(true)}>
    Like
  </button>
);
```

JS와 마크업을 함께 사용하는게 처음에는 조금 어색할 수 있습니다. 그래도 점점 적응이 될겁니다. [JSX로 마크업 작성하기](https://beta.reactjs.org/learn/writing-markup-with-jsx)도 한번 확인해보세요. 이건 [JSX로 쓰여진 HTML 파일][(](https://raw.githubusercontent.com/reactjs/reactjs.org/main/static/html/single-file-example.html))입니다. 다운로드 받고 갖고 놀기 좋습니다.

> **주의사항**
> Babel 컴파일러를 `<script>`를 통해 사용하는 방법은 학습하거나 간단한 데모를 만드는 단계에서는 좋습니다. 하지만 웹사이트를 느려지게 만들기 때문에 프로덕션에는 적합하지 않습니다. 다음 단계로 나아갈 준비가 되었다면 `type="text/babel"` 속성을 지우고 `<script>` 태그로 Babel compiler를 사용하지 않도록 합시다. 대신 다음 섹션에서는 `<script>` 태그 전체를 JSX에서 JS로 바꿔줄 JSX 전처리기(preprocessor)를 추가할겁니다.


### JSX를 프로젝트에 추가하기
프로젝트에 JSX를 추가하는건 번들러나 개발서버같이 복잡한 도구들을 필요로 하지 않습니다. JSX 전처리기를 추가하는것도 CSS 전처리기를 추가하는 것과 비슷합니다.

프로젝트 폴더로 가서 terminal(명령 프롬프트)을 열어줍시다. 그리고 아래 두개의 명령어를 입력합니다.(Node.js가 설치되어 있어야 합니다.)
1. `npm init -y` (만약 실패할 경우 [이렇게 고칠 수 있습니다.](https://gist.github.com/gaearon/246f6380610e262f8a648e3e51cad40d))
2. `npm install babel-cli@6 babel-preset-react-app@3`

JSX 전처리기를 설치할 때는 npm만 있으면 됩니다. React와 애플리케이션 코드는 여전히 `<script>` 태그로 남아있습니다.

축하합니다! 여러분은 방금 프로덕션에서도 쓸 수 있는 JSX 설정을 완료했습니다.

### JSX 전처리기를 실행하기
JSX 문법이 포함된 파일이 저장될때마다 JSX 전처리기가 다시 실행되도록 하는것도 가능합니다. 전처리기가 다시 실행되면 JSX 문법을 브라우저가 이해할 수 있는 평범한 JavaScript 문법으로 바꿔줄겁니다. 아래는 세팅하는 방법입니다.
1. `src` 폴더를 만듭니다.
2. terminal(명령 프롬프트)에서 다음 명령어를 입력합니다 : `npx babel --watch src --out-dir . --presets react-app/prod` (완료되길 기다리는게 아닙니다! 이 명령어는 `src` 폴더 안에 있는 JSX를 자동으로 감지하는 프로세스를 실행시키는 명령어입니다.)
3. JSX로 작성된 `like-button.js`를 `src` 폴더 안으로 이동시킵니다. ([이렇게요!](https://gist.githubusercontent.com/gaearon/1884acf8834f1ef9a574a953f77ed4d8/raw/dfc664bbd25992c5278c3bf3d8504424c1104ecf/like-button.js))

감시기는 `like-button.js` 파일을 전처리해 브라우저에게 맞는 JavaScript 코드로 변환해줄 겁니다.

> **주의사항**
> 만약 "You have mistakenly installed the `babel` package" 라는 에러 메시지가 나타난다면, [이전 단계](https://beta.reactjs.org/learn/add-react-to-a-website#add-jsx-to-a-project)를 놓친 것 때문일 수 있습니다. 같은 폴더에서 다시 한번 실행해보세요.

방금 여러분이 사용한 도구는 Babel이라고 합니다. Babel에 대한 추가 정보는 Babel의 [문서](https://babeljs.io/docs/en/babel-cli/)에서 확인할 수 있습니다. Babel은 JSX 뿐만 아니라 거의 모든 최신 JavaScript 문법들을 '이전 브라우저에서 돌아가지 않을 걱정 없이' 사용할 수 있도록 합니다.

만약 여러분이 빌드툴의 더 많은 기능을 사용해보고 싶다면 [가장 인기있고 배우기 쉬운 툴체인들을 확인해보세요](https://beta.reactjs.org/learn/start-a-new-react-project)