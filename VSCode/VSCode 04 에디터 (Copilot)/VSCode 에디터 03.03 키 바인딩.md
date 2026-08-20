# VSCode 에디터 03.03 키 바인딩 (Keybindings)

## 한줄 요약
단축키(키 바인딩)를 사용자 정의하고, `keybindings.json` 또는 단축키 편집기로 관리하는 방법을 안내합니다.

## 핵심 개념
- 키 바인딩은 명령에 키 조합을 연결하는 설정입니다.
- 단축키 편집기(UI)로 검색·바인딩·충돌 해소 가능하며, JSON 편집기로 직접 수정할 수 있습니다.
- `when` 절을 사용해 특정 컨텍스트(예: 에디터 포커스, 특정 언어)에서만 동작하도록 설정합니다.

## 주요 기능
- `Preferences: Open Keyboard Shortcuts`로 UI 편집기 열기.
- `Preferences: Open Keyboard Shortcuts (JSON)`로 `keybindings.json` 직접 편집.
- 키 바인딩 추가/제거, 우선순위(사용자 > 워크스페이스 > 기본값), 충돌 경고 제공.
- `keybindings.json` 예시 구조: `[{ "key": "ctrl+k ctrl+c", "command": "editor.action.commentLine", "when": "editorTextFocus" }]`

## 실무 팁
- 팀 표준 단축키를 문서화하고 `keybindings.json` 스니펫으로 공유하면 일관성 유지에 도움이 됩니다.
- 자주 쓰는 키 조합이 OS나 다른 앱과 충돌하면 다른 조합으로 재할당하세요.
- 복잡한 멀티키 바인딩(ctrl+k ctrl+c 등)을 사용하면 실수 입력을 줄일 수 있습니다.

## 핵심 정리
키 바인딩은 UI와 JSON 두 방법으로 관리할 수 있으며, `when` 조건을 활용하면 상황별 단축키를 정교하게 설정할 수 있습니다.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/configure/keybindings
