> TODO : 컴포넌트, props, state 링크 번역본으로 대치
# React 개발자 도구
React 개발자 도구를 통해 React [컴포넌트](https://beta.reactjs.org/learn/your-first-component)를 검사하고, [props](https://beta.reactjs.org/learn/passing-props-to-a-component)와 [state](https://beta.reactjs.org/learn/state-a-components-memory)를 수정하고, 성능 문제를 확인할 수 있습니다.
> 여러분이 배울 것들
> - React 개발자 도구를 설치하는 방법

## 브라우저 확장 프로그램(extension)
React로 만들어진 웹사이트를 디버그하는 가장 쉬운 방법은 React 개발자 도구 브라우저 확장 프로그램을 설치하는겁니다. 아래와 같은 여러 브라우저에서 설치해 이용할 수 있습니다.
- [**Chrome**용 설치하기](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
- [**Firefox**용 설치하기](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)
- [**Edge**용 설치하기](https://microsoftedge.microsoft.com/addons/detail/react-developer-tools/gpphkfbcpidddadnkolkpfckpihlkkil)

여러분은 이제 React를 이용해 만든 웹사이트에 방문한다면 개발자 도구에서 Components 패널과 Profiler 패널을 확인할 수 있을겁니다.
![react-dev-tools-1](https://beta.reactjs.org/images/docs/react-devtools-extension.png)

# Safari와 그 외의 브라우저
Safari와 같은 다른 브라우저들에서는 `react-devtools` npm 패키지를 설치해야 합니다.
```shell
# Yarn
yarn global add react-devtools

# Npm
npm install -g react-devtools
```
그 다음, terminal(명령 프롬프트)에서 개발자 도구를 열어주세요.
```shell
react-devtools
```
마지막으로 `<script>` 태그를 여러분의 웹사이트의 `<head>` 내부에 넣음으로써 여러분의 웹사이트와 개발자 도구를 연결할 수 있습니다.
```html
<html>
    <head>
        <script src="http://localhost:8097"></script>
```
여러분의 웹사이트를 새로고침 하면 브라우저의 개발자 도구에서 아래와 같은 화면을 볼 수 있습니다.
![react-dev-tools-2](https://beta.reactjs.org/images/docs/react-devtools-standalone.png)

## 모바일 환경(React Native)
React 개발자 도구는 [React Native](https://reactnative.dev/)로 만든 앱도 검사할 할 수 있습니다.
React 개발자 도구를 사용하는 가장 쉬운 방법은 전역적으로 설치하는겁니다.
```shell
# Yarn
yarn global add react-devtools

# Npm
npm install -g react-devtools
```
그 다음, terminal(명령 프롬프트)에서 개발자 도구를 열어주세요.
```shell
react-devtools
```
로컬 환경에서 실행되고 있는 React Native 앱과 연결될 것입니다.

> 몇 초 후에도 개발자 도구와 연결되지 않는다면 앱을 새로고침 해보세요

[React Native를 디버깅 하는 방법에 대해 더 알아보기](https://reactnative.dev/docs/debugging)
