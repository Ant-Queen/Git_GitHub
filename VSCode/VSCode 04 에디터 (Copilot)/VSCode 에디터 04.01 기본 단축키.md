# VSCode 에디터 04.01 기본 단축키 (Default Keybindings)

## 한줄 요약
VS Code의 기본 단축키(키 바인딩) 전체 목록과 형식, 사용자 정의 방법을 설명합니다.

## 핵심 개념
- 기본 단축키는 플랫폼별(Windows/macOS/Linux)로 정의되어 있으며 JSON 형식으로 표현됩니다.
- 키 바인딩 항목은 `key`, `command`, `when`(조건) 필드를 가집니다.
- 기본 키 바인딩 파일은 읽기 전용이며, 사용자 설정은 `keybindings.json`에 추가해 오버라이드합니다.

## 주요 내용
- 기본 단축키 전체 목록은 공식 문서에서 검색 및 복사 가능.
- 복합 키 시퀀스(예: `Ctrl+K Ctrl+C`)와 단일 조합 모두 지원.
- `when` 조건을 사용해 특정 컨텍스트에서만 단축키 활성화 가능(예: `editorTextFocus`).

## 실무 팁
- 자주 쓰는 단축키를 팀 표준으로 정해 `keybindings.json` 스니펫으로 공유하세요.
- 단축키 충돌이 발생하면 명령 팔레트에서 해당 키를 검색해 우선순위를 조정하세요.
- 플랫폼별 차이를 고려해 스크립트나 문서에서 플랫폼별 안내를 추가하세요.

## 핵심 정리
기본 단축키는 사용자의 생산성 핵심 요소입니다. `keybindings.json`을 통해 쉽게 사용자화하고 팀과 공유할 수 있습니다.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/reference/default-keybindings
