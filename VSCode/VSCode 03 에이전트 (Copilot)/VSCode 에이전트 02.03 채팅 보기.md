# VS Code 에이전트 채팅 보기

VS Code의 Chat view는 에디터 옆에서 에이전트와 함께 작업할 수 있는 코드 중심 인터페이스입니다. 현재 워크스페이스 안에서 프롬프트를 입력하고, 에이전트가 생성한 변경 사항을 검토하며, 코딩과 디버깅을 계속할 수 있습니다.

## 1. 전제 조건

- Visual Studio Code 설치
- GitHub Copilot 접근 권한
- Copilot 구독 설정 및 인증 완료

## 2. Chat view 열기

Chat view를 여는 방법:

- VS Code 제목 표시줄의 Chat 메뉴에서 `Open Chat` 선택
- `Ctrl+Alt+I` 단축키 사용
- 명령줄에서 `code chat` 실행

Chat view는 보조 사이드바에 열립니다.

### 레이아웃 옵션

Chat view는 여러 레이아웃을 지원합니다:

- 사이드바(기본): 채팅을 코드 옆에 두고 작업하기에 적합합니다.
- 편집기 탭: 채팅을 에디터 탭으로 열어 더 넓게 보거나 세션을 나란히 비교할 때 유리합니다.
- 별도 창: 멀티 모니터 환경에서 채팅을 분리해 사용할 때 좋습니다.

## 3. 인터페이스 개요

Chat view의 주요 구성 요소:

1. 세션 목록: 현재 워크스페이스 세션을 보고 관리
2. 대화 영역: 대화 기록과 에이전트 응답, 작업 내용 표시
3. 입력 영역: 프롬프트 입력 및 세션 설정(에이전트 대상, 에이전트 유형, 모델, 권한 수준)

Chat view는 컴팩트 모드와 나란히 보기 모드 두 가지로 전환할 수 있습니다.

## 4. 채팅 세션 시작

Chat view에서 에이전트 세션을 시작하는 방법:

1. `New Chat (+)` 선택 또는 `Ctrl+N` 입력
2. `Agent Target` 드롭다운에서 실행 위치 선택
   - 예: 로컬 에이전트 선택하여 워크스페이스와 도구에 접근
3. `Agent` 드롭다운에서 에이전트 선택
   - 예: `Agent`를 선택하면 에이전트가 작업을 판단하고 워크스페이스를 변경
4. 필요하면 언어 모델과 권한 수준을 선택
5. 수행할 작업을 설명하는 프롬프트를 입력하고 `Enter`

에이전트는 작업을 단계별로 분해하고 파일을 편집하며 명령을 실행하고, 문제가 생기면 스스로 수정합니다.

## 5. 코드와 함께 작업하기

Chat view는 메인 VS Code 창에서 실행되므로, 에이전트가 작업해도 에디터 상태를 유지할 수 있습니다.

- 에디터에서 변경 파일을 열고 인라인 diff 검토
- 편집 오버레이를 사용해 개별 변경을 `Keep` 또는 `Undo`
- 디버거 사용, 작업 실행, 테스트 수행으로 에이전트 변경 검증
- 확장 및 노트북에 접근하며, 에이전트가 노트북을 직접 편집할 수 있음
- 원격 개발 중인 경우에도 동일한 컨텍스트와 도구에 접근

## 6. Agents 창과 세션 공유

Chat view와 Agents 창은 동일한 에이전트 세션을 공유합니다.

- Chat view에서 시작한 세션은 Agents 창에서 바로 사용 가능
- 반대로 Agents 창에서 시작한 세션도 Chat view에서 이어서 사용 가능
- 세션 기록과 컨텍스트가 유지되어 인터페이스 간 전환이 매끄럽다

Agents 창으로 전환하려면 제목 표시줄의 `Open in Agents` 버튼을 클릭하거나 명령 팔레트에서 `Chat: Open Agents Window` 실행, 또는 `code --agents` 명령 사용합니다.

## 7. 다음 단계

- [Interact with chat](https://code.visualstudio.com/docs/chat/copilot-chat): 컨텍스트 추가, 효과적인 프롬프트 작성, 변경 검토
- [Manage chat sessions](https://code.visualstudio.com/docs/agents/sessions/chat-sessions): 채팅을 에디터 탭과 창에서 열고 세션 정리
- [Use the Agents window](https://code.visualstudio.com/docs/agents/agents-window): 여러 프로젝트에서 에이전트를 관리

---

> 이 문서는 VS Code 공식 `Chat view` 페이지를 바탕으로 한국어로 요약 정리한 내용입니다.
