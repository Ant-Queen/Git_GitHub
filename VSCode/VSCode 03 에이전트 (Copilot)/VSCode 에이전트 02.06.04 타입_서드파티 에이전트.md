# 서드파티 에이전트 (Third-party Agents)

Visual Studio Code의 서드파티 에이전트는 Anthropic, OpenAI 등 외부 공급자가 제공하는 AI 에이전트입니다. VS Code 내에서 통합된 에이전트 세션 관리와 편집기 통합을 통해 서드파티 모델의 고유 기능을 활용할 수 있습니다.

## 서드파티 에이전트를 사용하는 이유

- 고유한 기능 사용: 각 서드파티 에이전트는 자체 강점과 특화 기능을 제공합니다.
- 통합 경험: VS Code에서 모든 에이전트 세션을 한 곳에서 관리할 수 있습니다.
- 풍부한 편집기 통합: 디버깅, 테스트 등 VS Code 기능과 함께 사용할 수 있습니다.
- 결제 관리: 기존 GitHub Copilot 구독을 통해 인증 및 청구를 관리할 수 있습니다.

## 클라우드 서드파티 에이전트 활성화

- VS Code에서 서드파티 클라우드 에이전트를 사용하려면 Copilot 계정 설정에서 서드파티 코딩 에이전트 지원을 활성화해야 합니다.
- GitHub 문서의 [Enabling or disabling third-party coding agents in your repositories](https://docs.github.com/en/copilot/how-tos/manage-your-account/manage-policies#enabling-or-disabling-third-party-coding-agents-in-your-repositories)를 참고하세요.
- 서드파티 공급자의 VS Code 확장을 설치할 필요는 없습니다.

## Claude 에이전트 (미리보기)

Claude 에이전트는 Anthropic의 Claude Agent SDK를 사용하며, VS Code에서 작업을 계획하고 실행하며 반복합니다.

### Claude 세션 시작하기

1. 채팅 보기(`Ctrl+Alt+I`)에서 새 채팅(`+`)을 선택합니다.
2. 로컬 세션 또는 클라우드 세션을 선택합니다.
   - 로컬 세션: 세션 유형 드롭다운에서 `Claude` 선택
   - 클라우드 세션: 세션 유형 드롭다운에서 `Cloud` 선택 후 `Partner Agent`에서 `Claude` 선택
3. 프롬프트를 입력하고 에이전트가 작업을 수행하도록 합니다.

Claude 에이전트는 작업을 진행하면서 필요한 도구를 자율적으로 결정하고 워크스페이스에 변경을 적용합니다.

### Claude 슬래시 명령어

Claude 에이전트는 고급 워크플로우를 위한 전용 슬래시 명령어를 지원합니다. 채팅 입력란에 `/`를 입력하여 사용 가능한 명령어를 확인할 수 있습니다.

- `/agents`: 특정 작업용 특수 Claude 에이전트를 생성 및 관리합니다.
- `/hooks`: 도구 실행 전후에 실행할 라이프사이클 훅을 구성합니다.
- `/memory`: 프로젝트 전반에서 Claude 에이전트에 지속적인 컨텍스트를 제공하는 `CLAUDE.md` 메모리 파일을 여거나 편집합니다.
- `/init`: 새 `CLAUDE.md` 메모리 파일을 초기화합니다.
- `/pr-comments`: 풀 리퀘스트의 코멘트를 가져옵니다.
- `/review`: 풀 리퀘스트의 코드 변경을 검토합니다.
- `/security-review`: 현재 브랜치의 보류 중인 코드 변경에 대한 보안 검토를 수행합니다.

### Claude 권한 모드

Claude 에이전트는 특정 작업을 수행하기 전에 권한을 요청합니다. 기본적으로 워크스페이스 내 파일 편집은 자동 승인되고, 터미널 명령 실행 등 다른 작업은 확인이 필요할 수 있습니다.

변경 사항 적용 방식:
- 자동 편집: Claude가 작업을 진행하면서 자율적으로 워크스페이스를 수정
- 승인 요청: 변경 사항 적용 전에 사용자 검토 요청
- 계획: 작업을 시작하기 전에 의도된 접근 방식을 개략적으로 제시

> `github.copilot.chat.claudeAgent.allowDangerouslySkipPermissions` 설정은 모든 권한 검사를 건너뜁니다. 인터넷에 연결되지 않은 격리된 샌드박스 환경에서만 사용하세요.

## OpenAI Codex

OpenAI Codex 에이전트는 OpenAI의 Codex를 사용하여 코딩 작업을 자율적으로 수행합니다. VS Code에서 대화형으로 실행하거나 백그라운드에서 unattended 모드로 실행할 수 있습니다.

### 사전 요구사항

- Copilot Pro+ 구독으로 인증 필요
- 로컬 세션의 경우 `OpenAI Codex` 확장 설치 필요
- Copilot Pro+ 구독을 통해 Codex에 추가 설정 없이 접근할 수 있습니다.

### Codex 세션 시작하기

1. 채팅 보기(`Ctrl+Alt+I`)에서 새 채팅(`+`)을 선택합니다.
2. 로컬 또는 클라우드 세션을 선택합니다.
   - 로컬 세션: 세션 유형 드롭다운에서 `Codex` 선택
   - 클라우드 세션: 세션 유형 드롭다운에서 `Cloud` 선택 후 `Partner Agent`에서 `Codex` 선택
3. 프롬프트를 입력하고 에이전트가 작업하도록 합니다.

Codex 에이전트를 사용 중지하려면 VS Code에서 `OpenAI Codex` 확장을 비활성화하거나 제거합니다.

## 자주 묻는 질문

- 기존 Copilot 구독으로 서드파티 에이전트를 사용할 수 있나요?
- 서드파티 에이전트는 공급자의 VS Code 확장을 사용하는 것과 어떻게 다른가요?
- Claude/Codex 에이전트가 두 가지 유형으로 나뉘는 이유는 무엇인가요?

## 관련 자료

- [에이전트 개요](https://code.visualstudio.com/docs/agents/overview)
- [서드파티 에이전트 소개](https://docs.github.com/en/copilot/concepts/agents/about-third-party-agents)
