# VS Code Agents 창 정리

원문: https://code.visualstudio.com/docs/agents/agents-window

---

## 1. 한 줄 정리

`Agents window`는 VS Code 에디터와 별도로 실행되는 전용 창으로, 여러 작업공간의 에이전트 세션을 한곳에서 관리하고 비교하며 실행하는 에이전트 중심 워크플로우를 제공합니다.

---

## 2. 준비물

- Visual Studio Code 설치
- GitHub Copilot 접근 권한
- GitHub 로그인 및 Copilot 구독 활성화

> Agents 창은 GitHub 인증이 필요하며, 이미 VS Code에서 GitHub에 로그인되어 있다면 해당 계정으로 자동 로그인됩니다.

---

## 3. Agents 창 열기

Agents 창을 여는 방법:

- VS Code 제목 표시줄에서 `Open in Agents` 버튼 클릭
- 명령 팔레트에서 `Chat: Open Agents Window` 실행 (`Ctrl+Shift+P`)
- 명령줄에서 `code --agents` 실행
- 브라우저에서 `https://insiders.vscode.dev/agents` 열기

> `Open in Agents` 버튼을 숨기고 싶으면 제목 표시줄에서 오른쪽 클릭 후 `Hide 'Open in Agents'` 선택할 수 있습니다.

---

## 4. 인터페이스 구성

Agents 창의 주요 구성 요소:

1. 세션 목록
   - 사이드바에서 현재 활성화된 모든 에이전트 세션을 표시합니다.
   - 작업공간별로 그룹화되고, 세션 이름 변경, 완료 표시, 고정 등의 명령을 사용할 수 있습니다.
2. 사용자화 패널
   - 에이전트 맞춤 설정(Agent, Skills, Instructions, Hooks, MCP 서버, 플러그인 등)에 접근합니다.
3. 채팅 영역
   - 에이전트와 대화를 주고받는 메인 영역입니다.
   - 여러 세션 뷰를 나란히 열어 비교할 수 있습니다.
4. 변경 사항 패널
   - 에이전트가 만든 파일 변경, 추가, 삭제 내용을 리뷰합니다.

---

## 5. 에이전트 세션 시작하기

Agents 창에서는 세션을 시작할 때 작업공간을 직접 선택할 수 있습니다.

1. 사이드바의 `New` 버튼 클릭 또는 `Ctrl+N` 누르기
2. 작업공간 드롭다운에서 로컬 폴더 또는 GitHub 저장소 선택
3. 에이전트 유형 선택
   - 폴더: `Copilot CLI` 또는 `Claude agent` 선택
   - GitHub 저장소: `Copilot Cloud` 세션 생성
4. 필요 시 커스텀 에이전트, 언어 모델, 권한 수준 등 추가 설정
5. 요청 내용을 프롬프트에 입력하고 Enter

> `Alt+Enter` 또는 Alt 클릭 시, 현재 세션을 유지한 채 새 세션을 백그라운드로 시작할 수 있습니다.

---

## 6. 세션 관리

세션 목록은 워크스페이스 별 혹은 시간 기준으로 그룹화할 수 있습니다.

- 선택한 세션은 채팅 패널에 전체 대화 기록을 표시합니다.
- 활성 세션 변경 시 Changes 패널과 파일 탐색기가 해당 세션 상태로 업데이트됩니다.
- 세션별 파일 변경 통계를 확인하고, 필요한 세션을 쉽게 찾아볼 수 있습니다.

---

## 7. 변경 사항 검토

Changes 패널은 에이전트가 만든 수정 사항을 자세히 보여줍니다.

- Files 탭: 작업공간 파일 탐색기
- Changes 탭: 에이전트가 변경한 파일 목록
- 파일 선택 시 diff 보기로 수정 내용을 비교
- 기본은 다중 파일 diff 편집기, `sessions.changes.openSingleFileDiff` 설정으로 단일 파일 diff로 전환 가능

### 피드백 주기

- 변경 파일에서 코드 범위를 선택하고 `Add Feedback` 클릭
- 코멘트를 입력해 에이전트에게 수정 요청
- `Submit Feedback`으로 보낸 후 에이전트가 반영하고 코멘트를 해결합니다

### 변경 적용 옵션

- Commit: 폴더 격리 방식에서 변경 사항을 워크스페이스에 직접 커밋
- Merge: worktree 격리 방식에서 병합하고 PR 생성
- Checkout: Copilot Cloud 세션의 브랜치를 로컬로 체크아웃
- Discard: 변경사항 취소

---

## 8. 로컬에서 변경 사항 검증

Agents 창에서 에이전트가 만든 변경 사항을 실행 환경으로 검증할 수 있습니다.

1. 세션을 열거나 시작
2. 툴바의 `Tasks` 드롭다운에서 `Add Task` 선택
3. 작업 이름, 명령, 자동 실행 옵션, 저장 위치 지정
4. 추가된 작업을 실행하여 빌드, 테스트, 서버 실행 등 확인

### 통합 브라우저

- `localhost` 링크를 선택하면 통합 브라우저에서 앱을 열 수 있습니다.
- 각 세션마다 브라우저 탭이 분리되어, 세션 전환 시 해당 세션의 탭 상태를 유지합니다.
- 통합 터미널에서 `localhost` 링크를 클릭해도 브라우저를 열 수 있습니다.

---

## 9. 원격 환경에서 사용하기

Agents 창은 원격 머신과 브라우저에서도 사용할 수 있습니다.

- 브라우저 기반: `https://insiders.vscode.dev/agents`
- SSH: 작업공간 드롭다운에서 원격 SSH 연결 선택
- Dev Tunnels: 개발용 터널에 연결하여 세션 관리

---

## 10. 하나의 세션에서 여러 채팅 실행

Copilot CLI 세션에서는 세션 내부에 여러 개의 독립 채팅 탭을 열 수 있습니다.

- `+` 버튼으로 새 채팅 탭 생성
- 각 채팅은 별도의 대화 기록과 상태를 가짐
- 채팅 간 전환, 이름 변경, 닫기 가능
- 첫 채팅은 기본 채팅이며 닫을 수 없습니다

---

## 11. 세션을 나란히 열기

여러 세션을 동시에 옆에 두고 비교할 수 있습니다.

- 세션 목록에서 우클릭 후 `Open to the Side`
- 드래그 앤 드롭으로 뷰 영역에 세션 추가
- Alt + 선택으로 옆에 열기

> 활성 세션만 터미널, 파일, 변경 내용이 반영됩니다. 뷰 고정(pin) 기능으로 표시를 유지할 수 있습니다.

---

## 12. 에이전트 사용자화

Customizations 패널에서 프로젝트나 사용자 단위로 에이전트 동작을 조정할 수 있습니다.

- Agents: 사용자화된 에이전트 페르소나 정의
- Skills: 재사용 가능한 작업 패키지 추가
- Instructions: 코드 스타일, 규칙, 선호도 설정
- Hooks: 세션 단계별 스크립트 실행
- MCP Servers: 외부 서비스 연결
- Plugins: 미리 패키지된 커스텀 기능 설치

---

## 13. 폴더 신뢰

새 폴더나 저장소를 열 때 폴더 신뢰 확인이 필요합니다.

- 신뢰하지 않으면 Agents 창에서 세션을 시작할 수 없습니다.
- VS Code 본창과 동일한 워크스페이스 신뢰 상태를 공유합니다.

---

## 14. 기타 설정과 확장

- Agents 창은 VS Code 설정을 그대로 공유합니다.
- Agents 창 전용 설정을 사용하려면 해당 범위를 지정하여 오버라이드할 수 있습니다.
- 확장 기능도 Agents 창에서 사용할 수 있습니다.
- 일부 확장은 설치 후 자동 활성화되고, 필요 시 `extensions.supportAgentsWindow` 설정으로 강제 활성화할 수 있습니다.

---

## 15. 제한 사항

현재 Agents 창에서 주의할 점:

- 통합 브라우저를 자동으로 열 수 없으며, 명령으로 열어야 합니다.
- 지원되는 에이전트 유형은 `Copilot CLI`, `Copilot Cloud`, `Claude agent`입니다.
- 로컬 에이전트 또는 일부 서드파티 에이전트는 메인 VS Code 창에서 관리해야 합니다.
- Copilot Cloud 세션은 GitHub 저장소에서만 지원됩니다.
- `Plan` 에이전트는 드롭다운에 없지만 `/plan` 명령을 사용할 수 있습니다.
- 여러 채팅은 현재 Copilot CLI 세션에서만 지원됩니다.
- 멀티 루트 세션은 아직 지원되지 않습니다.

---

## 16. 정리

Agents 창은 여러 프로젝트와 세션을 한곳에서 관리하고, 에이전트 결과를 비교하면서 안전하게 검토하는 데 유용한 도구입니다. 에디터 창과 함께 사용하면 코드 중심 작업과 에이전트 중심 작업을 자연스럽게 오가며 개발할 수 있습니다.

---

## 17. 다음 단계

- [Chat overview](https://code.visualstudio.com/docs/chat/chat-overview)
- [Manage chat sessions](https://code.visualstudio.com/docs/chat/chat-sessions)
- [Remote agent sessions](https://code.visualstudio.com/docs/agents/remote-agent-sessions)
