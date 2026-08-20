# VSCode 에디터 03.05 설정 동기화 (Settings Sync)

## 한줄 요약
Settings Sync는 계정에 설정, 확장, 키바인딩, 스니펫 등을 동기화해 여러 기기에서 동일한 개발 환경을 유지하게 해줍니다.

## 핵심 개념
- 동기화는 사용자 계정(Microsoft 또는 GitHub)으로 로그인해 클라우드에 설정을 저장합니다.
- 동기화 대상: Settings, Keybindings, Extensions, Snippets, UI State, Tasks, Launch, 그리고 언어 설정 등.
- 충돌이 발생하면 병합 또는 덮어쓰기를 선택할 수 있습니다.

## 주요 기능
- `Turn on Settings Sync`로 활성화 후 동기화 항목 선택.
- 동기화된 항목은 계정 연결 후 자동으로 백업되고 다른 기기에서 복원 가능.
- 동기화 데이터는 언제든지 설정에서 초기화하거나 특정 항목을 제외할 수 있음.

## 실무 팁
- 개인 기기와 회사 기기에서 서로 다른 환경을 유지하려면 동기화 항목을 세심하게 선택하세요(예: Extensions 제외).
- 동기화 충돌 시 우선 한쪽을 로컬로 받아보고 변경사항을 검토한 후 병합하세요.
- 팀 전체의 기본 확장 목록을 권장하려면 동기화 대신 `extensions.json`으로 권장 사항을 제공하세요.

## 핵심 정리
Settings Sync는 여러 디바이스에서 개발 환경을 일관되게 유지하는 데 유용하지만, 민감 데이터나 기기별 차이를 고려해 동기화 항목을 선택해야 합니다.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/configure/settings-sync
