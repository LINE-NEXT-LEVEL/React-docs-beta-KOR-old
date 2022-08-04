# 새 프로젝트 시작하기

만약 여러분이 새로운 프로젝트를 시작하려 한다면, 우리는 툴체인 혹은 프레임워크를 사용하는걸 추천합니다. 이 툴은 로컬 환경에 Node.js만 설치되어있어야 하지만, 편안한 개발 환경을 제공해줍니다.

> #### 여러분이 배울 것들
>
> * 툴체인과 프레임워크의 차이점
> * 최소한의 툴체인으로 프로젝트를 시작하는 방법
> * 완전한 프레임워크로 프로젝트를 시작하는 방법
> * 대중적인 툴체인과 프레임워크에 어떤 것들이 들어있는지

## 여러분의 모험을 선택하세요

React는 UI 코드를 '컴포넌트'라고 부르는 작은 조각들로 쪼개 정리할 수 있도록 합니다. ***라이브러리라는 말이 있었으면 좋겠습니다.*** React는 라우팅이나 데이터 관리같은 일은 관여하지 않아요. 그렇기 때문에 여러분이 새 React 프로젝트를 시작할 때 여러 선택지가 존재할 수 있습니다.

* [HTML 파일과 script 태그로 시작하는 방법](https://beta.reactjs.org/learn/add-react-to-a-website)은 Node.js 설정은 필요 없지만 몇몇 기능이 제한적입니다.
* 최소한의 툴체인으로 시작해 프로젝트를 진행함에 따라 여러 기능들을 추가할 수 있습니다. (배우기에도 좋구요!)  ***최소한의 툴체인으로 시작하는 방법, ...처음의 ~방법과 동일한 형식이면 더 좋을 것 같습니다. 세번째도 마찬가지입니다.***
* 프레임워크는 조금 더 완고합니다. 데이터 fetching이나 라우팅 같은 기능들은 여러분이 직접 설정하지 않아도 프레임워크가 제공해줍니다.

## 작은 툴체인으로 시작하기

만약 여러분이 React를 배운다면, 우리는 [Create React App](https://create-react-app.dev/)을 추천합니다. React를 접하거나 새로운 단일 페이지, 클라이언트 사이드 애플리케이션을 만드는데 있어 가장 유명한 방법입니다. CRA(Create React App)은 React를 위해 만들어졌지만, 라우팅이나 데이터 fetching같은 것들은 설정되어있지 않아요.

먼저, Node.js를 설치합니다. 그리고 terminal(명령 프롬프트)을 열어 아래 명령어를 입력해 프로젝트를 시작합시다.

```shell
npx create-react-app my-app
```

이제 여러분은 방금 만든 애플리케이션을 아래 명령어를 통해 실행시킬 수 있습니다.

```shell
cd my-app
npm start
```

더 많은 정보는 [공식 가이드](https://create-react-app.dev/docs/getting-started)를 통해 얻을 수 있습니다.

> Create React App은 백엔드 로직이나 데이터베이스는 다루지 않습니다. 그래도 어떤 백엔드와도 함께 사용할 수 있습니다. 여러분이 프로젝트를 빌드한다면 정적인 HTML, CSS, 그리고 JS 파일들이 담긴 폴더가 생성됩니다. Create React App은 서버의 이점을 활용하지 않기 때문에 애플리케이션이 최고의 성능을 내도록 보장하지는 않습니다. 만약 로딩 시간을 더 빠르게 단축시키려 하거나, 라우팅이나 서버사이드 로직같은 내장 기능들을 활용하고 싶다면 Create React App 대신 프레임워크를 사용하세요.

**이런 훌륭한 대안들도 있습니다.**

* [Vite](https://vitejs.dev/guide/)
* [Parcel](https://parceljs.org/)

## 완전한 프레임워크로 시작하기

만약 여러분이 프로덕션을 위한 프로젝트를 시작하려 한다면, [Next.js](https://nextjs.org/)가 훌륭한 선택입니다. Next.js는 정적이고 server-rendered 애플리케이션을 만들기 위한 유명하고 가벼운 프레임워크입니다. 라우팅이나 스타일링, 서버사이드 렌더링같은 기능들도 내장되어 있습니다. Next.js를 이용하면 프로젝트를 빠르게 시작하고 실행할 수 있습니다.

[Next.js 재단](https://nextjs.org/learn/foundations/about-nextjs)은 React와 Next.js에 대한 훌륭한 튜토리얼을 제공하고 있습니다.

**이런 훌륭한 대안들도 있습니다.**

* [Gatsby](https://www.gatsbyjs.org/)
* [Remix](https://remix.run/)
* [Razzle](https://razzlejs.org/)

### 커스텀 툴체인

여러분은 나만의 툴체인을 만들고 구성하는걸 더 좋아할 수도 있습니다. 툴체인은 보통 아래와 같은 항목들로 구성됩니다.

* 패키지 매니저(package manager) : third-party 패키지들을 설치하고, 업데이트하고, 관리할 수 있도록 하는 도구입니다. [npm](https://www.npmjs.com/)(Node.js에 내장되어 있습니다), [yarn](https://yarnpkg.com/), [pnpm](https://pnpm.io/)이 유명합니다.
* 컴파일러(compiler) : 현대 언어들과 JSX, 타입 주석같은 추가 문법들을 브라우저가 이해할 수 있도록 컴파일합니다. 인기있는 컴파일러로는 [Babel](https://babeljs.io/), [TypeScript](https://www.typescriptlang.org/), [swc](https://swc.rs/) 등이 있습니다.
* 번들러(bundler) : 여러분이 모듈화된 코드를 작성할 수 있도록 도와주고, 코드들을 합쳐 작은 패키지로 만들어 로드 시간을 줄여줍니다. 인기있는 번들러는 [webpack](https://webpack.js.org/), [Parcel](https://parceljs.org/), [esbuild](https://esbuild.github.io/), [swc](https://swc.rs/) 등이 있습니다.
* minifier : 여러분의 코드를 더 컴팩트하게 만들어 로드 시간을 더 단축시킵니다. [Terser](https://terser.org/), [swc](https://swc.rs/) 등이 유명합니다.
* 서버(server) : 서버 요청을 처리해 여러분이 작성한 컴포넌트들을 HTML을 통해 렌더링 될 수 있도록 합니다. [Express](https://expressjs.com/)가 유명합니다.
* linter : 일반적으로 많이 하는 실수들로부터 코드를 지켜줍니다. [ESLint](https://eslint.org/)가 유명합니다.
* test runner : 여러분이 작성한 코드에 대해 테스트를 돌려줍니다. [Jest](https://jestjs.io/)가 유명합니다.

만약 여러분이 처음부터 여러분만의 JavaScript 툴체인을 만들고자 할 경우 [이 가이드를 참고해보세요.](https://blog.usejournal.com/creating-a-react-app-from-scratch-f3c693b84658) Create React App을 다시 만드는 과정을 담고 있습니다. 큰 프로젝트에서는 하나의 저장소(repository) 안에 여러 패키지들을 담고 싶을 수 있습니다. [Nx](https://nx.dev/react) 또는 [Turborepo](https://turborepo.org/)같은 도구를 쓰는것도 좋은 방법입니다.
