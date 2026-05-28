# VS Code Extension Marketplace 정리

Visual Studio Code 확장 마켓플레이스 페이지(`https://code.visualstudio.com/docs/configure/extensions/extension-marketplace`)를 한국어로 요약한 문서입니다.

## 개요

VS Code 확장은 언어 지원, 디버거, 도구 등을 추가하여 개발 환경을 확장합니다. 확장은 VS Code 내부에서 Marketplace를 탐색하고 설치할 수 있으며, 확장 저자는 VS Code API를 통해 기능을 기여합니다.

## 확장 탐색

- 활동 표시줄의 확장 아이콘을 클릭하거나 `View: Extensions` 명령(`Ctrl+Shift+X`)으로 확장 뷰를 엽니다.
- Marketplace에서 인기 있는 확장 목록을 볼 수 있습니다.
- 각 확장 항목에는 설명, 게시자, 다운로드 수, 별점이 표시됩니다.
- 확장 항목을 선택하면 세부 정보 페이지가 표시됩니다.
- 프록시 환경에서는 Marketplace 액세스를 위해 프록시 서버를 구성해야 합니다.

## 확장 설치

### 확장 찾기 및 설치

- 예시로 `TODO Highlight` 확장을 설치할 수 있습니다.
- 확장 뷰 검색 상자에 `todo`를 입력하여 관련 확장을 찾습니다.
- 확장 ID는 `publisher.extension` 형식으로 고유합니다. 예: `wayou.vscode-todo-highlight`.
- 확장 세부 정보 페이지에서 `Install` 버튼을 클릭하여 설치합니다.
- 설치 후 `Install` 버튼은 `Manage` 톱니바퀴 버튼으로 바뀝니다.
- 확장을 설치한 뒤 소스 코드에서 `TODO:` 같은 주석을 열면 확장이 동작하는 예시를 확인할 수 있습니다.

### 설치 후 관리

- 확장은 명령 팔레트(`Ctrl+Shift+P`)에서 해당 확장의 명령을 사용할 수 있습니다.
- 확장 설정은 Settings 편집기(`Ctrl+,`)에서 조정할 수 있습니다.
- 확장을 제거하려면 `Manage` 버튼의 컨텍스트 메뉴에서 `Uninstall`을 선택합니다.

## 확장 세부 정보

- 확장 세부 정보 페이지에서 README, 기능 기여, 변경 로그, 종속성을 확인할 수 있습니다.
- Extension Pack은 설치 시 함께 설치되는 확장 목록을 보여줍니다.

## 확장 뷰 필터 및 명령

- 확장 뷰에서 필터 메뉴를 사용하여 다음을 표시할 수 있습니다:
  - 업데이트 가능 확장
  - 사용 중인/사용 중지된 확장
  - 워크스페이스 추천 확장
  - 인기 확장
- 확장 목록은 설치 수, 평점, 이름, 게시일, 업데이트 날짜별로 정렬할 수 있습니다.
- 추가 명령은 `...` 메뉴에서 실행할 수 있으며, 확장 업데이트, 활성화/비활성화 등을 제어할 수 있습니다.
- `Extension Bisect` 유틸리티로 문제를 일으키는 확장을 찾을 수 있습니다.

### 검색

- 검색 상자에 확장 이름, 도구, 언어를 입력하여 찾습니다.
- 정확한 확장 식별자를 알고 있다면 `@id:publisher.extension`을 사용하세요.

### 프리릴리스 버전 설치

- 확장 설치 버튼의 드롭다운에서 `Install Pre-Release Version`을 선택하여 프리릴리스 버전을 설치할 수 있습니다.

### 설치 권장 및 동기화

- Settings Sync가 활성화된 경우, 확장도 여러 기기에서 동기화됩니다.
- 특정 확장을 설치하되 동기화하지 않으려면 확장 항목을 마우스 오른쪽 클릭하고 `Install (Do not Sync)`를 선택합니다.

## 확장 관리

### 설치된 확장 목록

- 확장 뷰는 기본적으로 설치된 확장과 추천 확장을 표시합니다.
- `Extensions: Focus on Installed View` 명령을 사용하면 설치된 확장만 볼 수 있습니다.

### 확장 제거

- `Manage` 버튼에서 `Uninstall`을 선택하여 확장을 제거합니다.
- 제거 후 확장 호스트를 다시 시작하라는 메시지가 표시될 수 있습니다.

### 확장 비활성화

- 확장을 완전히 제거하지 않고 일시적으로 비활성화할 수 있습니다.
- 비활성화는 전역 또는 현재 워크스페이스에 대해 설정할 수 있습니다.
- 비활성화 후에는 확장 호스트를 다시 시작해야 합니다.

### 확장 활성화

- 비활성화된 확장은 `Enable` 또는 `Enable (Workspace)` 명령으로 다시 활성화할 수 있습니다.
- `Enable All Extensions` 명령도 사용할 수 있습니다.

### 자동 업데이트

- VS Code는 확장 업데이트를 자동으로 확인하고 설치합니다.
- 업데이트 후 확장 호스트를 다시 시작하라는 메시지가 표시됩니다.
- 자동 업데이트를 끄려면 `Disable Auto Update for All Extensions` 명령 또는 `extensions.autoUpdate` 설정을 사용합니다.
- 확장별 자동 업데이트도 마우스 오른쪽 클릭 메뉴에서 조정할 수 있습니다.
- 확장 업데이트 확인을 완전히 끄려면 `extensions.autoCheckUpdates`를 `false`로 설정합니다.

### 수동 업데이트

- 자동 업데이트를 끄면 `@updates` 필터를 사용하여 업데이트 가능한 확장을 확인할 수 있습니다.
- 개별 확장의 `Update` 버튼을 클릭하거나 `Update All Extensions`를 사용하여 일괄 업데이트할 수 있습니다.
- 자동 확인도 비활성화된 경우 `Check for Extension Updates` 명령으로 업데이트를 확인합니다.

## 추천 확장

- `Show Recommended Extensions` 명령으로 추천 확장 목록을 볼 수 있습니다.
- 추천 확장은 다음을 기반으로 합니다:
  - 워크스페이스 추천
  - 최근에 연 파일 추천

### 추천 무시

- 추천을 무시하려면 확장 세부 정보 페이지의 `Manage` 메뉴에서 `Ignore Recommendation`을 선택합니다.

## 확장 구성

- 확장마다 설정 방식과 요구 사항이 다릅니다.
- 일부 확장은 Settings 편집기에 설정을 추가하고, 다른 확장은 별도 구성 파일이나 외부 도구가 필요합니다.
- 확장 README 또는 Marketplace 페이지를 참조하여 설치 및 구성 방법을 확인합니다.

## 명령줄에서 확장 관리

- 명령줄에서 확장을 나열, 설치, 제거할 수 있습니다.
- 예:
  - `code --list-extensions`
  - `code --show-versions`
  - `code --install-extension publisher.extension`
  - `code --uninstall-extension publisher.extension`
  - `code --install-extension myextension.vsix`
  - `code --enable-proposed-api publisher.extension`
- 확장 식별자는 세부 정보 페이지에서 확인할 수 있습니다.

## 확장 뷰 필터

### 정렬

- `@sort:installs` - 설치 수 기준 내림차순
- `@sort:name` - 이름 순
- `@sort:publishedDate` - 게시일 순
- `@sort:rating` - 평점 순
- `@sort:updateDate` - 업데이트 날짜 순

### 카테고리 및 태그

- `category:` 및 `tag:` 필터를 사용하여 범주나 태그별로 검색할 수 있습니다.
- 지원 카테고리 예:
  - Azure, Data Science, Debuggers, Education, Extension Packs, Formatters, Keymaps,
    Language Packs, Linters, Machine Learning, Notebooks, Others, Programming Languages,
    SCM Providers, Snippets, Testing, Themes, Visualization
- 두 단어 이상의 카테고리 이름은 따옴표로 묶어야 합니다. 예: `category:"SCM Providers"`
- 태그는 자유 문자열이며 IntelliSense로 제공되지 않습니다.

### 확장 뷰 필터 목록

- `@builtin` - 내장 확장
- `@deprecated` - 더 이상 사용되지 않는 확장
- `@disabled` - 비활성화된 설치 확장
- `@enabled` - 활성화된 확장
- `@featured` - 추천 확장
- `@installed` - 설치된 확장
- `@popular` - 인기 확장
- `@recentlyPublished` - 최근 게시된 확장
- `@recommended` - 추천 확장
- `@updates` - 업데이트 가능 확장
- `@workspaceUnsupported` - 현재 워크스페이스에서 지원되지 않는 확장
- 필터를 조합할 수 있습니다. 예: `@installed @category:themes`

- 필터를 지정하지 않으면 현재 설치된 확장과 추천 확장이 표시됩니다.

## VSIX에서 설치

- `.vsix` 파일로 패키지된 확장을 설치할 수 있습니다.
- `Extensions: Install from VSIX` 명령 또는 명령 팔레트에서 실행합니다.
- 명령줄에서 `code --install-extension myextension.vsix`로 설치할 수 있습니다.
- 여러 `.vsix`를 동시에 설치하려면 `--install-extension`을 여러 번 지정합니다.
- VSIX로 설치된 확장은 기본적으로 자동 업데이트가 비활성화됩니다.
- 확장 패키징 및 게시에 대해 더 알고 싶다면 `Publishing Extensions` 문서를 참고하세요.

## 워크스페이스 추천 확장

- 특정 워크스페이스에 권장 확장 목록을 공유할 수 있습니다.
- `Extensions: Configure Recommended Extensions (Workspace Folder)` 명령으로 `.vscode/extensions.json` 파일을 생성합니다.
- 멀티 루트 워크스페이스에서는 `.code-workspace` 파일에 `extensions.recommendations`를 추가할 수 있습니다.
- 예:
  ```json
  {
    "recommendations": ["dbaeumer.vscode-eslint", "esbenp.prettier-vscode"]
  }
  ```
- 확장은 `publisher.extension` 형식으로 지정합니다.
- 설치된 확장 auto-complete이 해당 파일에서 지원됩니다.
- 워크스페이스를 처음 열면 VS Code가 추천 확장을 설치하라는 메시지를 표시합니다.

## FAQ

### 확장은 어디에 설치되나요?

- Windows: `%USERPROFILE%\.vscode\extensions`
- macOS: `~/.vscode/extensions`
- Linux: `~/.vscode/extensions`
- `--extensions-dir <dir>` 명령줄 옵션으로 위치를 변경할 수 있습니다.
- `VSCODE_EXTENSIONS` 환경 변수를 설정하여 설치 위치를 변경할 수도 있습니다.

### 확장 설치 시 connect ETIMEDOUT 오류가 발생하면?

- 프록시를 통해 인터넷에 연결하는 경우 발생할 수 있습니다.
- 프록시 서버 지원 설정을 확인하세요.

### Marketplace에서 확장을 직접 다운로드할 수 있나요?

- 확장 검색 결과에서 `Download VSIX` 또는 `Download Specific Version VSIX`를 선택하여 확장 파일을 내려받을 수 있습니다.

### 확장 추천 표시를 중지할 수 있나요?

- `extensions.showRecommendationsOnlyOnDemand`를 `true`로 설정하면 추천 섹션을 제거합니다.
- `extensions.ignoreRecommendations`를 `true`로 설정하면 추천 알림을 숨길 수 있습니다.
- `Show Recommended Extensions` 명령은 언제든지 추천 목록을 확인하는 데 사용할 수 있습니다.

### Marketplace 확장을 신뢰할 수 있나요?

- Marketplace는 악성 확장을 방지하기 위한 보호 조치를 제공합니다.
- 버전 1.97부터 타사 게시자로부터 확장을 처음 설치할 때 게시자 신뢰 확인 대화 상자를 표시합니다.
- 확장 실행 보안에 대해 더 알아보려면 `extension runtime security` 문서를 참조하세요.

### 조직에서 내부 확장을 호스팅할 수 있나요?

- 가능합니다. `Private Marketplace for Extensions` 문서를 확인하세요.

### 확장 서명이 확인되지 않는 경우?

- Marketplace는 게시된 확장을 서명합니다.
- 서명 확인 오류가 발생하면 주의해서 설치를 결정하세요.
- `extensions.verifySignature` 설정을 사용해 서명 확인을 비활성화할 수 있습니다.

### 원격 창에서 확장이 동기화되지 않는 이유는?

- Settings Sync는 SSH, 컨테이너, WSL과 같은 원격 창에 대해 확장을 동기화하지 않습니다.

### 조직에서 특정 확장을 허용하거나 차단할 수 있나요?

- `extensions.allowed` 애플리케이션 설정을 구성하여 허용된 확장만 설치할 수 있습니다.

## 다음 단계

- [Extension API](https://code.visualstudio.com/api)
- [Your First Extension](https://code.visualstudio.com/api/get-started/your-first-extension)
- [Publishing to the Marketplace](https://code.visualstudio.com/api/working-with-extensions/publishing-extension)
