# VS Code에서 에이전트로 계획 세우기

VS Code의 Plan 에이전트를 사용하면 구현을 시작하기 전에 요구사항을 충족하는 상세한 구현 계획을 만들 수 있습니다. todo 목록을 통해 전체 목표에 집중하고 진행 상황을 효과적으로 추적할 수 있습니다.

이 문서는 Plan 에이전트와 todo 목록을 VS Code에서 사용하는 방법을 설명합니다.

## 작업 계획 세우기

작업을 계획하려면 채팅 보기에서 내장된 Plan 에이전트를 사용하고, 작업을 설명한 다음 생성된 계획을 반복적으로 다듬습니다.

1. `Ctrl+Alt+I`를 눌러 채팅 보기를 열고 에이전트 드롭다운에서 `Plan`을 선택합니다.
   - 또는 `/plan` 뒤에 작업 설명을 입력하여 한 번에 Plan 에이전트로 전환하고 계획을 시작할 수 있습니다.
2. 고수준 작업(기능, 리팩터링, 버그 등)을 입력하고 제출합니다. 예:

   ```text
   Implement a user authentication system with OAuth2 and JWT
   ```

3. 에이전트가 작업을 조사한 후 묻는 확인 질문에 답변합니다.
4. Plan 에이전트가 고수준 계획 요약, 구현 단계 및 검증 단계를 생성합니다. 계획 초안을 검토하고 요구사항을 만족할 때까지 후속 프롬프트로 반복합니다.
5. 계획이 완료되면 구현을 시작하거나 편집기에서 계획 프롬프트를 열어 추가로 검토할 수 있습니다.

   - 계획을 구현하려면 동일한 세션에서 계속 진행하거나 새로운 Copilot CLI 세션을 시작해 백그라운드에서 계획을 구현할 수 있습니다.

> Tip: Plan 에이전트는 구현 계획을 세션 메모리 파일(`/memories/session/plan.md`)에 자동 저장합니다. `Chat: Show Memory Files` 명령을 실행하고 목록에서 `plan.md`를 선택하면 이 파일에 액세스할 수 있습니다. 세션 메모리는 대화가 종료되면 삭제되므로 이후 세션에서는 사용할 수 없습니다.

## 계획 사용자화

계획 프로세스를 팀의 워크플로우에 맞게 조정할 수 있습니다.

- **맞춤 계획 에이전트 생성**
  - [사용자 정의 에이전트](https://code.visualstudio.com/docs/agent-customization/custom-agents)를 정의하여 아키텍처 가이드라인을 적용하거나 특정 계획 산출물을 요구할 수 있습니다.
- **계획 및 구현 모델 선택**
  - `chat.planAgent.defaultModel` 설정을 사용하여 Plan 에이전트의 기본 모델을 선택합니다.
  - `github.copilot.chat.implementAgent.model` 설정을 사용하여 구현 단계 모델을 선택합니다.
- **계획 에이전트에 추가 도구 연결(실험적)**
  - `github.copilot.chat.planAgent.additionalTools` 설정을 사용하여 연구 및 계획 단계에서 Plan 에이전트가 추가 도구에 액세스하도록 할 수 있습니다.
  - 예를 들어 MCP 서버를 사용해 내부 데이터 소스나 도구에 연결할 수 있습니다.

## 관련 자료

- [연구 에이전트로 심층 조사 실행](https://code.visualstudio.com/docs/agents/agent-types/copilot-cli#_run-deep-research-with-the-research-agent)
- [VS Code 에이전트 메모리](https://code.visualstudio.com/docs/agents/memory)
- [에이전트 도구 구성](https://code.visualstudio.com/docs/agents/agent-tools)
- [컨텍스트 엔지니어링 사용자 가이드](https://code.visualstudio.com/docs/agents/guides/context-engineering-guide)

## 도움말 및 지원

- 커뮤니티에 질문하기: https://stackoverflow.com/questions/tagged/vscode
- 기능 요청: https://go.microsoft.com/fwlink/?LinkID=533482
- 문제 보고: https://www.github.com/Microsoft/vscode/issues
