# 에디터 세팅하기
적절히 잘 준비된 에디터는 코드를 더 읽기 쉽게, 그리고 빠르게 쓸 수 있도록 해줍니다.
또한 작성중에 버그를 찾아낼 수 있도록 도와줍니다. 이번이 에디터 세팅이 처음이거나,
현재 쓰는 에디터를 조정하려는 경우 몇가지 추천사항이 있습니다.
> 여러분이 배울 것들
> - 가장 인기있는 에디터가 어떤 것들인지
> - 코드를 자동포매팅하는 방법
## 여러분이 쓰게될 에디터
[VS Code](https://code.visualstudio.com)는 최근 가장 많이 쓰는 에디터중 하나입니다.
 큰 확장프로그램 마켓을 제공할 뿐더러, GitHub과 같은 인기있는 서비스들과 잘 연동될 수 있습니다.
 아래 기능들은 VS Code 확장프로그램으로 추가될 수 있을 뿐더러 구성도 용이하게 할 수 있습니다.
다음은 React 커뮤니티에서 사용되는 다른 에디터들입니다.
- [WebStorm](https://www.jetbrains.com/webstorm/)은 JavaScript에 특화된 통합개발환경입니다.
- [Sublime Text](https://www.sublimetext.com/)은 JSX, TypeScript에 대해 [syntax highlighting](https://stackoverflow.com/questions/65555800/how-to-make-sublime-3-open-js-files-with-jsx-syntax/70960574#70960574)과 자동완성기능을 제공합니다.
- [Vim](https://www.vim.org/)은 모든 종류의 텍스트를 작성, 수정하는데 있어 효율적으로 만들어진 설정 변경이 자유로운 텍스트 에디터입니다. UNIX 시스템과 Apple OS X에 "vi"라는 이름으로 포함되어 있습니다.
## 추천하는 에디터 기능들
어떤 기능들은 에디터에 포함되어 있지만, 없는 기능들은 확장프로그램을 추가해야합니다.
여러분이 선택한 에디터가 어떤 기능을 포함하는지 확인해봅시다.
### Linting
코드 linter 들은 여러분이 코드를 쓸때 문제를 찾아주고, 빠르게 수정할 수 있도록 해줍니다.
JavaScript를 위해 쓰이는 오픈소스인 [ESLint](https://eslint.org/)가 유명합니다.
- [React 추천 설정으로 ESLint 설치하기](https://www.npmjs.com/package/eslint-config-react-app)([Node 설치](https://nodejs.org/en/download/current/)를 확인하세요)
- [공식 확장 프로그램으로 VSCode에 ESLint 설치하기](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
### Formatting
여러분의 코드를 공유할 때, [탭 vs 공백](https://www.google.com/search?q=tabs+vs+spaces)으로 다른 기여자들과 토론하는 것은 지양하고 싶으실거에요.
다행히도, [Prettier](https://prettier.io/)는 정해진 규칙에 맞춰 여러분의 코드를 새로 포매팅하여 정리해줍니다.
Prettier를 실행하면 모든 여러분의 탭들이 공백으로 변경되고 들여쓰기, 따옴표등이 설정에 맞춰 변경될거에요. 이상적인 세팅을 위해 Prettier는 파일을 저장할때 실행되어 빠르게 변경해줍니다.

다음과 같은 과정을 통해 [VSCode의 Prettier 확장프로그램](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)을 설치할 수 있습니다
1. VS Code 실행
2. Quick Open(단축키 Ctrl/Cmd+p)
3. `ext install esbenp.prettier-vscode` 입력
4. 엔터
### Formatting on save
저장하다 코드를 포매팅하는걸 추천합니다. VS Code는 관련 세팅을 갖고있습니다.
1. VS Code에서 `CTRL/CMD + SHIFT + P` 입력
2. `settings` 입력
3. 엔터
4. 검색창에 `format on save` 입력
5. `format on save` 옵션 체크되었는지 확인
> ESLint가 기본설정을 갖고 있다면, Prettier와 충돌할 가능성이 있습니다.
> `eslint-config-prettier`를 활용해서 ESLint의 포매팅 규칙을 비활성화 하는 것을 추천합니다.
> 그렇게 하면 ESLint가 논리적인 실수만 잡도록 할 수 있습니다.
> pull request가 머지되기전에 파일들을 포매팅되게 하고싶다면, `prettier --check`를 활용하세요.