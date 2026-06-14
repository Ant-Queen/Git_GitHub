# VS Code Copilot 계획 에이전트 개요

## 개요

Plan 에이전트는 작업을 구현하기 전에 상세한 계획을 만들도록 도와줍니다. 요구 사항을 검토하고 구현 및 검증 단계를 설계하여 더 체계적으로 AI 기반 개발을 진행할 수 있습니다.

## 작업 계획 방법

1. 채팅 뷰(`Ctrl+Alt+I`)를 열고 Agents 드롭다운에서 `Plan`을 선택합니다.
   - 또는 채팅 입력창에 `/plan`과 작업 설명을 함께 입력하여 바로 계획을 시작할 수 있습니다.
2. 고수준 작업을 입력하고 전송합니다.
   - 예: `Implement a user authentication system with OAuth2 and JWT`
   - 또는 `/plan Add unit tests for all API endpoints`
3. 에이전트가 필요한 경우 추가 질문을 하면 답변합니다.
4. Plan 에이전트가 고수준 계획 요약과 구현 및 검증 단계를 생성합니다.
5. 계획 초안을 검토하고 요구 사항에 맞게 반복해서 수정합니다.
6. 계획이 완성되면 동작을 시작하거나 편집기로 계획 프롬프트를 열어 추가 검토를 진행합니다.

### 계획 구현 방법

- 같은 세션에서 계속 구현을 진행할 수 있습니다.
- 또는 새로운 [Copilot CLI 세션](https://code.visualstudio.com/docs/copilot/agents/copilot-cli)을 시작하여 백그라운드에서 계획을 실행할 수 있습니다.

### 계획 파일 저장

- Plan 에이전트는 구현 계획을 세션 메모리 파일(`/memories/session/plan.md`)에 자동으로 저장합니다.
- `Chat: Show Memory Files` 명령을 실행한 후 `plan.md`를 선택하여 해당 파일을 확인할 수 있습니다.
- 세션이 종료되면 세션 메모리는 지워지므로 이후 세션에서는 해당 계획 파일을 사용할 수 없습니다.

## 계획 사용자화

Plan 프로세스를 팀 워크플로에 맞게 조정할 수 있습니다.

- 커스텀 계획 에이전트 만들기
  - [커스텀 에이전트](https://code.visualstudio.com/docs/copilot/customization/custom-agents)를 정의하여 아키텍처 지침, 문서 형식, 단계별 산출물 등 특정 플래닝 요구를 강제할 수 있습니다.
- 모델 선택
  - `chat.planAgent.defaultModel` 설정으로 Plan 에이전트의 기본 모델을 선택합니다.
  - `github.copilot.chat.implementAgent.model` 설정으로 구현 단계에서 사용할 모델을 선택합니다.
- 추가 도구 제공(실험적)
  - `github.copilot.chat.planAgent.additionalTools` 설정을 사용해 Plan 에이전트가 조사 및 계획 단계에서 추가 도구에 접근하도록 구성합니다.
  - 예: 내부 데이터 소스 또는 툴에 연결하는 MCP 서버를 추가합니다.

## 관련 리소스

- 에이전트 메모리: https://code.visualstudio.com/docs/copilot/agents/memory
- 에이전트 도구 구성: https://code.visualstudio.com/docs/copilot/agents/agent-tools
- 컨텍스트 엔지니어링 안내서: https://code.visualstudio.com/docs/copilot/guides/context-engineering-guide

## 도움말 및 지원

- 커뮤니티에 질문하기
- 기능 요청 제출하기
- 이슈 보고하기
