# VS Code 프로필 정리

## 개요

Visual Studio Code의 프로필(Profile)은 설정, 확장, UI 레이아웃 등을 묶어서 저장하고 빠르게 전환할 수 있게 해줍니다. 기본 프로필을 유지하면서 언어별, 작업별, 데모용, 교육용 등 다양한 맞춤 구성을 분리해서 사용할 수 있습니다.

## 프로필 편집기 열기

프로필 편집기는 한 곳에서 프로필을 만들고 관리하는 전용 UI입니다.

- `파일 > 기본 설정 > 프로필` 메뉴에서 열기
- 활동 표시줄 하단의 관리(톱니바퀴) 버튼에서 열기

프로필 편집기는 기본적으로 모달 오버레이로 열립니다.

## 프로필 생성

프로필을 생성하려면 프로필 편집기에서 `새 프로필` 버튼을 클릭합니다.
새 프로필 생성 시 다음 옵션을 선택할 수 있습니다.

- 프로필 이름
- 아이콘
- 템플릿 또는 기존 프로필에서 복사
- 빈 프로필 생성

### 프로필 복사 옵션

- 기존 프로필 또는 템플릿에서 복사
- 빈 프로필로 생성
- 필요한 구성 항목만 선택하여 복사할 수 있음
  - 예: 설정, 키보드 단축키, 확장, 스니펫, 작업 등

### 프로필 미리보기

- `미리보기` 버튼을 선택하면 새 VS Code 창이 열리고 해당 프로필이 적용된 상태를 확인할 수 있습니다.
- 확인 후 `생성` 버튼으로 프로필을 완성합니다.

## 현재 프로필 확인

현재 활성 프로필은 다음 위치에서 확인할 수 있습니다.

- VS Code 제목 표시줄
- 활동 표시줄의 관리 버튼에 마우스를 올렸을 때 툴팁
- 프로필 편집기

아이콘을 설정한 경우 해당 아이콘이 관리 버튼에 표시되고, 아이콘이 없으면 활성 프로필 이름의 앞 두 글자가 배지로 표시됩니다.

> 기본 프로필(Default Profile)을 사용하는 경우 프로필 이름이 표시되지 않습니다.

## 프로필 구성

프로필은 일반 VS Code 구성처럼 다음 내용을 포함합니다.

- 설정
- 확장 설치/제거/비활성화
- UI 레이아웃 변경
- 키보드 단축키
- 스니펫
- 작업

프로필이 활성화된 상태에서 변경한 내용은 해당 프로필에 저장됩니다.

## 폴더 & 작업 영역 연관

프로필은 현재 폴더 또는 작업 영역과 연관됩니다. 폴더를 열면 해당 폴더에 연결된 프로필이 자동으로 활성화됩니다.

- 프로필 편집기의 `폴더 및 작업 영역` 섹션에서 연관된 폴더 목록 확인 가능

## 프로필 관리

### 프로필 전환

- 명령 팔레트에서 `Profiles: Switch Profile` 명령 실행
- 프로필 편집기에서 전환할 프로필 옆의 `현재 창에 사용` 버튼 클릭

### 프로필 편집

- 프로필 편집기에서 프로필 이름, 아이콘, 구성 내용을 수정할 수 있습니다.

### 프로필 삭제

- 프로필 편집기에서 `프로필 삭제` 버튼 선택
- 명령 팔레트에서 `Delete Profile` 명령으로 삭제 가능

### 새 창에서 프로필 열기

- 프로필 편집기의 `새 창에 사용` 옵션을 통해 새 VS Code 창에서 특정 프로필을 사용할 수 있습니다.
- `파일 > 프로필로 새 창 열기` 메뉴로 직접 선택 가능합니다.

### 모든 프로필에 설정 적용

- 설정 편집기에서 `Apply Setting to all Profiles` 동작 사용
- 이 옵션을 켜면 해당 설정이 모든 프로필에 적용됩니다.
- 언제든지 이 동작을 끄면 일반 프로필별 동작으로 되돌릴 수 있습니다.

### 모든 프로필에 확장 적용

- 확장 보기에서 `Apply Extension to all Profiles` 동작 사용
- 선택한 확장을 모든 프로필에서 사용 가능하도록 만듭니다.
- 이후 이 동작을 끌 수 있습니다.

## 머신 간 동기화

- Settings Sync를 사용하여 프로필을 여러 머신에 동기화할 수 있습니다.
- `Settings Sync: Configure` 드롭다운에서 `Profiles`를 체크해야 합니다.

> 주의: SSH, 컨테이너, WSL 등의 원격 창에서는 확장이 원격 창으로 동기화되지 않습니다.

## 프로필 공유

### 내보내기

- 프로필 편집기에서 `Export...`를 선택
- GitHub gist 또는 로컬 파일로 저장 가능

#### GitHub gist로 저장

- GitHub에 로그인한 후 비공개 gist로 프로필을 저장
- 공유용 URL이 생성됨
- VS Code 웹(`vscode.dev`)에서 해당 URL을 열면 프로필 내용을 확인하고 필요한 항목만 선택하여 가져올 수 있음

#### 로컬 파일로 저장

- `.code-profile` 확장자로 프로필 파일을 로컬로 저장

### 가져오기

- 프로필 편집기에서 `Import Profile...` 선택
- GitHub gist URL 또는 로컬 프로필 파일 선택
- 가져온 프로필을 수정한 뒤 `생성`하여 등록

## 프로필 활용 예시

- 데모: 데모 전용 확장, 설정, UI 레이아웃을 가진 별도 프로필 생성
- 교육: 학생용 맞춤 구성과 확장을 담은 프로필 공유
- 문제 보고: `빈 프로필(Empty Profile)`로 확장과 설정을 초기화하여 문제 원인 진단
- 언어/작업별 환경: JavaScript 프론트엔드, Python 백엔드 등 작업별 프로필 사용

## 프로필 템플릿

VS Code는 여러 기본 프로필 템플릿을 제공합니다. 새 프로필 생성 시 템플릿을 선택할 수 있습니다.

### Python 템플릿

- 확장: autoDocstring, Container Tools, Even Better TOML, Python, Python Environments, Remote Development, Ruff 등
- 설정: `python.analysis.autoImportCompletions`, `python.analysis.fixAll`, `editor.defaultFormatter` 등

### Data Science 템플릿

- 확장: Data Wrangler, GitHub Copilot, Jupyter, Python, Remote Development, Ruff 등
- 설정: `editor.inlineSuggest.enabled`, `editor.lineHeight`, `files.autoSave`, `jupyter.themeMatplotlibPlots`, `files.exclude` 등

### Doc Writer 템플릿

- 확장: Code Spell Checker, Markdown Checkboxes, Markdown Emoji, Markdown Footnotes, Markdown Preview GitHub Styling, Markdown Preview Mermaid Support, markdownlint, Word Count, Read Time 등
- 설정: `workbench.colorTheme`, `editor.minimap.enabled`, `editor.fontLigatures`, `files.autoSave`, `markdown.validate.enabled`, `workbench.startupEditor` 등

### Node.js 템플릿

- 확장: Container Tools, Dev Containers, DotENV, EditorConfig, ESLint, JavaScript snippets, Jest, Edge Tools, npm Intellisense, Prettier, Rest Client, YAML 등
- 설정: `editor.formatOnPaste`, `git.autofetch`, 언어별 기본 포매터 등

### Angular 템플릿

- 확장: Angular Language Service, Angular Schematics, angular2-switcher, Dev Containers, EditorConfig, ESLint, JavaScript snippets, Jest, Material Icon Theme, Edge Tools, Playwright, Prettier, Rest Client, YAML 등
- 설정: `editor.formatOnPaste`, `git.autofetch`, 언어별 기본 포매터, `workbench.iconTheme` 등

### Java General 템플릿

- 확장: Debugger for Java, IntelliCode, IntelliCode API Usage Examples, Language Support for Java by Red Hat, Maven for Java, Project Manager for Java, Test Runner for Java 등

### Java Spring 템플릿

- 확장: Spring Boot Dashboard, Spring Boot Tools, Spring Initializr Java Support 등
- 설정: `boot-java.rewrite.reconcile` 등

## 명령줄 사용

- `code <폴더> --profile "프로필 이름"` 명령으로 특정 프로필을 사용하여 VS Code를 실행할 수 있습니다.
- 지정한 프로필이 없으면 같은 이름의 빈 프로필이 새로 생성됩니다.

## 자주 묻는 질문

### 프로필은 어디에 저장되나요?

- Windows: `%APPDATA%\Code\User\profiles`
- macOS: `$HOME/Library/Application Support/Code/User/profiles`
- Linux: `$HOME/.config/Code/User/profiles`

Insiders 버전의 경우 `Code - Insiders` 폴더를 사용합니다.

### 임시 프로필(Temporary Profile)이란?

- `Profiles: Create a Temporary Profile` 명령으로 생성
- 빈 프로필로 시작하며 자동 생성된 이름이 붙음
- VS Code를 닫으면 삭제됨
- 새로운 구성이나 확장 테스트에 유용함

### 다른 프로필의 설정을 상속할 수 있나요?

- 현재는 프로필 간 상속 기능을 지원하지 않습니다.
- 새 프로필 생성 시 다른 프로필 또는 기본 프로필에서 복사할 수는 있지만, 이후에는 연결이 유지되지 않습니다.

### 프로젝트에서 프로필을 제거하려면?

- 프로젝트를 기본 프로필로 되돌리면 됩니다.
- `Developer: Reset Workspace Profiles Associations` 명령으로 현재 폴더에 할당된 모든 프로필을 기본 프로필로 초기화할 수 있습니다.
- 이 명령은 프로필을 삭제하지 않습니다.

### 프로필 내보내기 시 일부 설정이 누락되는 이유는?

- 머신별 설정(로컬 경로 등)은 다른 컴퓨터에서 유효하지 않기 때문에 내보내지 않습니다.

### 새 프로필 생성 시 템플릿이 보이지 않는 이유는?

- 템플릿은 인터넷에 연결되어 있어야 다운로드할 수 있습니다.
- 인터넷 연결 상태를 확인하세요.
