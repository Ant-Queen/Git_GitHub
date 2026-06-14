# 클라우드 에이전트 (Cloud Agents)

클라우드 에이전트는 로컬 머신이 아닌 원격 인프라에서 실행됩니다. VS Code에서는 통합 채팅 보기에서 클라우드 에이전트 세션을 생성하고 관리할 수 있으며, 로컬 또는 백그라운드 에이전트 대화를 클라우드 에이전트로 넘길 수 있습니다.

## 클라우드 에이전트란?

- 로컬 및 백그라운드 에이전트와 달리 원격 인프라에서 실행됩니다.
- VS Code의 통합 채팅 보기에서 모든 클라우드 에이전트 세션을 확인하고 관리할 수 있습니다.
- 작업의 범위가 명확하고 필요한 컨텍스트가 충분한 경우에 적합합니다.
- 코드 리뷰 통합과 풀 리퀘스트 생성 기능을 통해 팀 협업에 효과적입니다.
- 원격 실행 환경이므로 VS Code 내장 도구 및 런타임 컨텍스트(예: 실패한 테스트, 텍스트 선택)에 직접 액세스할 수 없습니다.
- 클라우드 에이전트는 클라우드 에이전트 서비스에 구성된 MCP 서버와 언어 모델만 사용할 수 있습니다.

## 주요 클라우드 에이전트 유형

### GitHub Copilot 클라우드 에이전트

- VS Code에서 사용하는 기본 클라우드 에이전트입니다.
- GitHub 저장소 전체에 대한 대규모 리팩터링을 수행할 수 있습니다.
- 고수준 요구사항에서 기능을 완전히 구현할 수 있습니다.
- 자동 풀 리퀘스트 생성과 상세 설명 작성 기능을 제공합니다.
- 코드 리뷰 통합 및 피드백 처리 기능을 지원합니다.

### 서드파티 클라우드 에이전트

- Claude 코딩 에이전트, Codex 코딩 에이전트 등 다양한 타사 클라우드 에이전트를 지원합니다.
- 사용하려면 Copilot 계정 설정에서 클라우드 서드파티 에이전트 지원을 활성화해야 합니다.
- 해당 공급자의 VS Code 확장을 설치할 필요는 없습니다.

## 클라우드 에이전트 세션 시작하기

### 새 클라우드 에이전트 세션 생성

1. 채팅 보기에서 세션 목록 드롭다운의 `New Chat`을 선택하고 세션 유형으로 `Cloud`를 선택합니다.
2. 또는 명령 팔레트(`Ctrl+Shift+P`)에서 `Chat: New Cloud Agent` 명령을 실행합니다.
3. 클라우드 에이전트 제공자를 선택하고 필요에 따라 커스텀 에이전트와 모델을 선택합니다.
4. 프롬프트를 입력하여 작업을 시작합니다.

예시:
```
Refactor the authentication module to improve security and performance. Implement OAuth2 and JWT for token management, and optimize database queries for user sessions.
```

5. 클라우드 에이전트가 원격에서 작업을 시작하며, 채팅 보기에서 진행 상황을 모니터링하고 상호작용할 수 있습니다.

> GitHub.com에서 이슈 또는 풀 리퀘스트를 Copilot 클라우드 에이전트에 할당한 경우, 해당 세션이 VS Code 세션 목록에 자동으로 표시됩니다.

## 에이전트 세션을 클라우드로 넘기기

- 복잡한 작업은 먼저 로컬 에이전트에서 요구사항을 명확히 한 뒤 클라우드 에이전트로 넘기는 것이 좋습니다.
- 로컬 에이전트 대화를 클라우드 에이전트로 넘기면 전체 채팅 컨텍스트가 전달됩니다.

### 넘기기 방법

1. 채팅 보기에서 진행 중인 로컬 에이전트 세션을 엽니다.
2. 세션 유형 드롭다운에서 `Cloud`를 선택하여 클라우드 에이전트로 전환합니다.
3. 계획 에이전트(`Plan agent`)를 사용 중이라면 `Continue in Cloud`를 선택하여 계획 구현을 클라우드 에이전트로 실행할 수 있습니다.
4. 백그라운드 에이전트 세션을 클라우드로 넘기려면 채팅 입력에 `/delegate`를 입력합니다.

## 클라우드 에이전트 세션 보기 및 관리

- 채팅 보기에서 클라우드 에이전트 세션만 필터링하여 표시할 수 있습니다.
- 세션 목록에서 클라우드 에이전트를 선택하면 채팅 보기에서 세션 세부 정보를 엽니다.
- 편집기 탭(채팅 에디터)으로 세션을 열려면 세션을 오른쪽 클릭하고 `Open as Editor`를 선택합니다.

## 관련 리소스

- [에이전트 개요](https://code.visualstudio.com/docs/agents/overview)
- [Backgroun agents](https://code.visualstudio.com/docs/agents/agent-types/copilot-cli)
- [커스텀 에이전트](https://code.visualstudio.com/docs/agent-customization/custom-agents)
- [GitHub Copilot 클라우드 에이전트 관리](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/manage-agents)
