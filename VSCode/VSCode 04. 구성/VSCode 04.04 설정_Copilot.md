# VS Code 설정 정리

Visual Studio Code의 설정 페이지(`https://code.visualstudio.com/docs/configure/settings`)를 한국어로 요약한 문서입니다.

## 개요

VS Code는 거의 모든 편집기 동작, UI, 확장 기능을 설정으로 사용자화할 수 있습니다. 설정은 JSON 파일로 저장되며, Settings UI 또는 직접 `settings.json`을 편집하여 변경할 수 있습니다.

## 설정 범위

### 사용자 설정

- 개인 설정으로, 현재 컴퓨터의 모든 VS Code 인스턴스에 적용됩니다.
- 예: 글꼴 크기를 `14`로 설정하면 모든 VS Code 창에서 동일하게 적용됩니다.
- 열기 방법:
  - 명령 팔레트에서 `Preferences: Open User Settings`
  - Settings 편집기에서 `User` 탭
  - 명령 팔레트에서 `Preferences: Open User Settings (JSON)`

### 워크스페이스 설정

- 특정 프로젝트에만 적용되는 설정입니다.
- 프로젝트별로 `node_modules`나 빌드 구성과 같은 값을 다르게 설정할 때 유용합니다.
- 워크스페이스 설정은 프로젝트 루트의 `.vscode/settings.json`에 저장됩니다.
- 열기 방법:
  - 명령 팔레트에서 `Preferences: Open Workspace Settings`
  - Settings 편집기에서 `Workspace` 탭
  - 명령 팔레트에서 `Preferences: Open Workspace Settings (JSON)`
- 모든 사용자 설정이 워크스페이스 설정으로 지원되는 것은 아닙니다. 예: 업데이트 및 보안 관련 일부 설정은 워크스페이스 범위에서 무시됩니다.

## Settings 편집기

- Settings 편집기는 그래픽 인터페이스로, `File > Preferences > Settings` 또는 `Ctrl+,`로 엽니다.
- 기본적으로 modal overlay 형태로 열리며, `workbench.editor.useModal`을 설정해 동작을 변경할 수 있습니다.
- 설정을 변경하면 즉시 적용됩니다.
- 수정된 설정은 왼쪽에 색 막대로 표시되어 쉽게 구분할 수 있습니다.
- 각 설정 항목의 톱니바퀴 아이콘(`Shift+F9`)을 클릭하면 다음과 같은 옵션을 사용할 수 있습니다:
  - 기본값으로 재설정
  - 설정 ID 복사
  - JSON 이름-값 쌍 복사
  - Settings URL 복사
- 특정 설정으로 바로 이동하는 URL 형식: `vscode://settings/<settingName>`

### Settings 그룹

- 관련 설정이 그룹별로 정리되어 있어 빠르게 찾을 수 있습니다.
- `Commonly Used` 그룹이 상단에 있으며 자주 사용하는 설정을 보여줍니다.
- 확장 기능은 자신만의 설정 그룹을 `Extensions` 아래에 추가할 수 있습니다.

### Settings 필터

- 검색 상자에 키워드를 입력하면 관련 설정만 표시됩니다.
- `@modified`: 기본값과 다른 설정만 필터링합니다.
- `@ext:<extensionId>`: 특정 확장에 속한 설정 검색
- `@feature:<feature>`: 기능별 설정 검색
- `@haspolicy`: 정책으로 제어되는 설정 검색
- `@id:<settingId>`: 설정 ID로 검색
- `@lang:<languageId>`: 언어별 설정 필터링
- `@tag:<tag>`: 예를 들어 `@tag:workspaceTrust`, `@tag:accessibility`, `@tag:advanced` 등
- `@tag:advanced`는 기본적으로 숨겨진 고급 설정을 표시합니다. 항상 표시하려면 `workbench.settings.alwaysShowAdvancedSettings`를 사용합니다.
- 검색어 기록이 저장되고 `Ctrl+Z`, `Ctrl+Y`로 실행 취소/다시 실행할 수 있습니다.
- 검색 상자의 오른쪽에 있는 `Clear Settings Search Input` 버튼으로 검색어를 빠르게 지울 수 있습니다.

## 확장 설정

- 설치된 확장은 자신의 설정을 Settings 편집기 `Extensions` 섹션에 추가합니다.
- 확장 보기(`Ctrl+Shift+X`)에서 확장을 선택하면 `Feature Contributions` 탭에서 확장 설정을 확인할 수 있습니다.
- 확장 개발자는 `contributes.configuration`을 통해 사용자 설정을 정의할 수 있습니다.

## Settings JSON 파일

- 설정 값은 `settings.json` 파일에 저장됩니다.
- 사용자 설정 위치:
  - Windows: `%APPDATA%\Code\User\settings.json`
  - macOS: `$HOME/Library/Application Support/Code/User/settings.json`
  - Linux: `$HOME/.config/Code/User/settings.json`
- 워크스페이스 설정 파일 위치:
  - 프로젝트 루트의 `.vscode/settings.json`
- 멀티 루트 워크스페이스에서는 워크스페이스 구성 파일 내부에 저장됩니다.
- `settings.json`을 직접 편집하려면 명령 팔레트에서 `Preferences: Open User Settings (JSON)` 또는 `Preferences: Open Workspace Settings (JSON)`을 사용합니다.
- Settings 편집기에서 특정 설정을 JSON으로 편집할 때는 IntelliSense가 제공되고, 이름/값 쌍 복사 기능도 사용할 수 있습니다.
- `settings.json` 파일은 스마트 완성과 설명 툴팁, JSON 오류 표시를 지원합니다.
- 일부 설정은 Settings UI에서 직접 편집할 수 없고 `settings.json`에서만 변경 가능합니다. 예: Workbench: Color Customizations.
- 항상 `settings.json`으로 작업하려면 `workbench.settings.editor`를 `json`으로 설정하면 됩니다.

## 설정 초기화

- 개별 설정은 Settings 편집기에서 톱니바퀴 아이콘을 통해 기본값으로 재설정할 수 있습니다.
- 모든 변경된 설정을 초기화하려면 `settings.json`에서 중괄호 `{}` 사이의 내용을 삭제하면 됩니다.
- 주의: 삭제 후 이전 값은 복구할 수 없습니다.

## 언어별 설정

### 언어별 에디터 설정

- 언어별로 다른 설정을 지정할 수 있습니다.
- Settings 편집기에서 필터 버튼을 눌러 언어 옵션을 선택하거나 `@lang:<languageId>`을 입력합니다.
- 언어 필터가 활성화된 상태로 설정을 변경하면 해당 언어에 대한 설정이 저장됩니다.
- 예: CSS 언어 필터로 `diffEditor.codeLens`를 설정하면 CSS에만 적용됩니다.
- 언어별 설정은 다음처럼 `settings.json`에 작성됩니다:
  ```json
  "[javascript][typescript]": {
    "editor.maxTokenizationLineLength": 2500
  }
  ```
- 단일 언어 블록과 다중 언어 블록이 모두 있는 경우, 단일 언어 값이 우선합니다.

### 언어별 설정 편집 방법

- 명령 팔레트에서 `Preferences: Configure Language Specific Settings` 실행
- 언어 선택 후 해당 언어 필터가 적용된 Settings 편집기가 열립니다.
- `workbench.settings.editor`가 `json`이면 새 언어 항목이 있는 `settings.json`이 열립니다.
- 파일의 우측 하단 상태 표시줄에서 언어 모드를 선택한 뒤 `Configure '<language_name>' language based settings`를 선택해 설정할 수도 있습니다.
- 언어별 설정은 비언어별 설정보다 우선합니다.
- 동일 언어에 대해 사용자/워크스페이스 설정이 모두 있으면, 워크스페이스 설정이 우선 적용됩니다.
- 여러 언어별 설정은 전체 언어 문자열(`"[typescript][javascript]"`) 단위로 병합되며, 개별 언어 ID별 우선순위가 적용되지 않습니다.

## 프로필 설정

- VS Code 프로필 기능을 사용하면 서로 다른 사용자화 세트를 저장하고 빠르게 전환할 수 있습니다.
- 프로필을 변경하면 해당 프로필의 사용자 설정만 적용됩니다.
- 프로필 설정 파일 위치:
  - Windows: `%APPDATA%\Code\User\profiles\<profile ID>\settings.json`
  - macOS: `$HOME/Library/Application Support/Code/User/profiles/<profile ID>/settings.json`
  - Linux: `$HOME/.config/Code/User/profiles/<profile ID>/settings.json`
- 프로필에서 설정을 수정하면 해당 프로필용 `settings.json` 파일이 생성됩니다.
- 기본 프로필이 아닌 상태에서 기본 프로필의 `settings.json`을 열려면 명령 팔레트에서 `Preferences: Open Application Settings (JSON)`을 사용합니다.

## 설정 우선순위

- 설정은 여러 범위를 통해 우선순위가 정해집니다.
- 일반적인 우선순위 목록(나중에 나올수록 우선):
  1. Default settings
  2. User settings
  3. Remote settings
  4. Workspace settings
  5. Workspace Folder settings
  6. Language-specific default settings
  7. Language-specific user settings
  8. Language-specific remote settings
  9. Language-specific workspace settings
  10. Language-specific workspace folder settings
  11. Policy settings
- 원시 타입(문자열, 불리언, 숫자, 배열)은 우선순위가 높은 범위의 값이 덮어씁니다.
- 객체 타입 값은 병합됩니다.
- 예: `workbench.colorCustomizations`가 사용자 설정과 워크스페이스 설정에서 모두 정의되면, 두 값을 병합하여 충돌 시 우선순위 높은 값이 적용됩니다.
- 언어별 설정은 비언어별 설정보다 우선합니다.

## 설정과 보안

- 특정 실행 파일을 지정하는 설정은 보안을 위해 사용자 설정에만 허용됩니다.
- 예: 터미널에서 사용할 셸 실행 파일(`terminal.external.windowsExec`, `terminal.external.osxExec`, `terminal.external.linuxExec`)은 워크스페이스 설정에서 정의할 수 없습니다.
- 이러한 설정이 워크스페이스에 포함되어 있으면, VS Code는 처음 워크스페이스를 열 때 경고를 표시하고 무시합니다.

## Settings Sync

- Settings Sync 기능을 사용하면 사용자 설정, 키 바인딩, 확장 등을 여러 컴퓨터 간에 동기화할 수 있습니다.
- Settings 편집기 오른쪽 또는 계정 활동 표시줄에서 `Backup and Sync Settings`를 통해 활성화합니다.
- 원격 창(SSH, 컨테이너, WSL)에서는 확장 동기화가 지원되지 않습니다.

## 기능 수명 주기

- 설정은 기능 상태에 따라 `Experimental`, `Preview`, `Stable`로 표시될 수 있습니다.
- `Experimental` 설정은 초기 사용자용이며 이후 변경 또는 제거될 수 있습니다.
- `Preview` 설정은 기능적으로 완성 단계이지만 안정성 개선이 진행 중입니다.
- Settings 편집기에서는 `@tag:experimental`, `@tag:preview`로 해당 설정을 검색할 수 있습니다.
- `Stable` 설정은 정식 지원 기능입니다.

## 관련 자료

- VS Code 기본 설정 참조: https://code.visualstudio.com/docs/reference/default-settings
- 설정 동기화 가이드: https://code.visualstudio.com/docs/configure/settings-sync

## 자주 묻는 질문

### "Unable to write settings." 오류

- 설정을 변경할 때 "Unable to write into user settings. Please open user settings to correct errors/warnings in it and try again." 메시지가 나오면 `settings.json`이 잘못된 JSON 형식이거나 값이 잘못되었음을 의미합니다.
- 명령 팔레트에서 `Preferences: Open User Settings (JSON)`을 열면 오류가 빨간 밑줄로 표시됩니다.

### 사용자 설정을 초기화하려면?

- 명령 팔레트에서 `Preferences: Open User Settings (JSON)`을 실행합니다.
- 열린 파일에서 중괄호 `{}` 내부를 모두 삭제하고 저장합니다.

### 워크스페이스 설정을 사용하는 이유는?

- 특정 프로젝트에서만 적용할 설정이 필요할 때 사용합니다.
- 예: 언어별 린트 규칙이나 빌드 설정을 한 프로젝트에만 적용하고 싶을 때.

### 확장 설정은 어디서 찾나요?

- 대부분 확장 설정은 Settings 편집기 또는 `settings.json`에서 찾을 수 있습니다.
- 확장 보기(`Ctrl+Shift+X`)에서 확장을 선택하고 `Feature Contributions` 탭을 확인하면 설정 목록이 표시됩니다.
