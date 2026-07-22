# VSCode 에디터 02.13 워크스페이스 신뢰

## 한줄 요약
Workspace Trust는 낯선 코드가 자동으로 실행되는 것을 방지해 보안을 강화하는 기능입니다. 신뢰하지 않는 워크스페이스는 Restricted Mode로 열립니다.

## 핵심 개념
- Restricted Mode: 터미널, 태스크, 디버깅, 일부 확장, 에이전트 등 자동 실행 기능을 제한합니다.
- 트러스트 상태는 폴더 단위로 관리되며, 부모 폴더 신뢰를 상속할 수 있습니다.
- Workspace Trust 설정은 `security.workspace.trust.*` 관련 항목으로 제어합니다.

## 동작 방식
- 새로운 폴더를 열면 기본적으로 Restricted Mode로 열리고, 배너에서 신뢰 여부를 선택할 수 있습니다.
- 신뢰 시 모든 기능이 활성화되고, 신뢰하지 않으면 위험 소지가 있는 자동 실행을 차단합니다.
- 확장별로 Restricted Mode에서 제한/비활성화 동작을 정의할 수 있습니다.

## 실무 팁
- 공개 저장소나 처음 받아본 코드일 때는 Restricted Mode로 검토 후 신뢰하세요.
- 팀 내부에 신뢰된 루트 폴더 구조를 만들면 반복적인 신뢰 선택을 줄일 수 있습니다.
- 예외적으로 특정 확장을 Restricted Mode에서 활성화하려면 `extensions.supportUntrustedWorkspaces` 설정을 사용하세요.

## 핵심 정리
Workspace Trust는 안전하게 외부 코드를 검토하고 실행하지 않도록 돕는 보호막입니다. 의심스러운 코드는 Restricted Mode로 먼저 확인하세요.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/editing/workspaces/workspace-trust
