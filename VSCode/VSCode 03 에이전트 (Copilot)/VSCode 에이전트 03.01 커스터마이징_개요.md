# VS Code에서 AI 커스터마이징 개요

Visual Studio Code는 AI에게 코드베이스, 코딩 표준, 워크플로우를 가르칠 수 있는 여러 가지 방법을 제공합니다. 이 문서는 커스터마이징 옵션을 소개하고 시작하는 방법을 안내합니다.

## 커스터마이징 시나리오

### 코딩 표준 정의하기

[커스텀 지침](https://code.visualstudio.com/docs/agent-customization/custom-instructions)을 사용해 프로젝트 전체 규칙과 컨벤션을 AI에 공유하세요. 항상 적용되는 지침은 모든 요청에 적용되고, 파일 기반 지침은 특정 파일 유형이나 폴더에만 적용됩니다. 예를 들어 ESLint 규칙을 모든 파일에 적용하고 `.tsx` 파일에는 React 패턴을 강제할 수 있습니다.

### 작업 및 워크플로우 자동화하기

[프롬프트 파일](https://code.visualstudio.com/docs/agent-customization/prompt-files)을 생성하여 컴포넌트 스캐폴딩이나 풀 리퀘스트 준비처럼 자주 반복하는 작업을 자동화하세요.

더 복잡한 다단계 워크플로우나 스크립트, 외부 도구가 필요한 경우에는 [에이전트 스킬](https://code.visualstudio.com/docs/agent-customization/agent-skills)로 패키지화하세요.

### AI 전문화하기

보안 리뷰어, 데이터베이스 관리자, 플래너 등 특정 페르소나를 갖춘 [커스텀 에이전트](https://code.visualstudio.com/docs/agent-customization/custom-agents)를 만드세요. 각 에이전트는 자체 동작, 사용 가능한 도구, 언어 모델 선호도를 정의할 수 있습니다.

작업별로 다른 [언어 모델](https://code.visualstudio.com/docs/agent-customization/language-models)을 선택하거나, 자체 API 키를 사용해 추가 모델에 접근할 수 있습니다.

### 플러그인 검색 및 설치하기

미리 패키지된 커스터마이징 번들을 추가하려면 [에이전트 플러그인](https://code.visualstudio.com/docs/agent-customization/agent-plugins)(미리보기)을 설치하세요. 하나의 플러그인에 슬래시 명령, 스킬, 커스텀 에이전트, 훅, MCP 서버가 포함될 수 있습니다.

### 외부 도구 및 데이터 연결하기

[Model Context Protocol(MCP)](https://modelcontextprotocol.io/)을 통해 데이터베이스, API, 기타 서비스에 AI가 접근하도록 MCP 서버를 추가하세요. [훅](https://code.visualstudio.com/docs/agent-customization/hooks)을 사용하면 파일 편집 후 포매터 실행 또는 보안 정책 적용과 같은 라이프사이클 단계에서 셸 명령을 실행할 수 있습니다.

## 시작하기

AI 커스터마이징은 단계적으로 진행하는 것이 좋습니다. 기본부터 시작해 필요한 만큼 점진적으로 추가하세요. 실습 가이드를 보려면 [Customize AI for your project](https://code.visualstudio.com/docs/agents/guides/customize-copilot-guide)를 참고하세요.

1. 프로젝트 초기화: 채팅에서 `/init`을 입력하여 코드베이스에 맞는 `.github/copilot-instructions.md` 파일을 생성합니다.
2. 대상 규칙 추가: 언어 규칙이나 프레임워크 패턴과 같은 특정 부분에 대해 파일 기반 `*.instructions.md` 파일을 만듭니다.
3. 반복 작업 자동화: 공통 워크플로우에 대한 프롬프트 파일을 만들고 외부 서비스를 연결하기 위해 MCP 서버를 추가합니다.
4. 특화된 워크플로우 생성: 특정 역할에 대한 커스텀 에이전트를 만듭니다. 재사용 가능한 기능은 에이전트 스킬로 패키지화하여 도구 간에 공유합니다.
5. AI로 커스터마이징 생성: 채팅에서 `/create-prompt`, `/create-instruction`, `/create-skill`, `/create-agent`, `/create-hook`을 입력하여 AI 지원으로 커스터마이징 파일을 생성합니다.

## 상위 리포지토리 검색

모노레포 환경에서는 워크스페이스에 리포지토리 루트가 아닌 하위 폴더를 열 수 있습니다. 기본적으로 VS Code는 열린 워크스페이스 폴더 내에서만 커스터마이징 파일을 검색합니다. `chat.useCustomizationsInParentRepositories` 설정을 활성화하면 상위 리포지토리에서도 커스터마이징 파일을 검색합니다.

이 설정을 활성화하면 VS Code는 각 워크스페이스 폴더에서 `.git` 폴더를 찾을 때까지 상위 폴더를 올라가며, 워크스페이스 폴더와 리포지토리 루트 사이의 모든 폴더에서 커스터마이징을 수집합니다.

이 기능은 다음과 같은 경우에 적용됩니다:

- 워크스페이스 폴더에 `.git` 폴더가 없는 경우
- 상위 폴더에 `.git` 폴더가 있는 경우
- 상위 리포지토리 폴더가 [신뢰된 폴더](https://code.visualstudio.com/docs/editing/workspaces/workspace-trust)인 경우

예를 들어:

```
my-monorepo/              # repo root (has .git folder)
├── .github/
│   ├── copilot-instructions.md
│   ├── instructions/
│   │   └── style.instructions.md
│   ├── prompts/
│   │   └── review.prompt.md
│   └── agents/
│       └── reviewer.agent.md
├── packages/
│   └── frontend/          # opened as workspace folder
│       └── src/
```

`packages/frontend/`만 열고 설정을 활성화하면 리포지토리 루트의 커스터마이징 파일도 검색됩니다.

> 참고: `chat.useCustomizationsInParentRepositories` 설정은 기본적으로 비활성화되어 있습니다.

## Agent Customizations 편집기

> 참고: Agent Customizations 편집기는 현재 미리보기입니다.

Agent Customizations 편집기는 모든 에이전트 커스터마이징을 한곳에서 생성하고 관리할 수 있는 중앙 UI를 제공합니다. 편집기는 커스터마이징 유형을 별도 탭으로 정리하고, 구문 강조 및 유효성 검사가 있는 내장 코드 편집기를 제공합니다.

프롬프트를 직접 작성하거나 AI를 사용해 초기 콘텐츠를 생성할 수 있습니다. MCP 서버와 에이전트 플러그인을 추가하려면 편집기에서 마켓플레이스를 직접 탐색하고 설치하거나 기존 항목을 관리할 수 있습니다.

Agent Customizations 편집기를 열려면 채팅 보기에서 `Configure Chat`(기어 아이콘)을 선택하거나 명령 팔레트에서 `Chat: Open Customizations`를 실행하세요.

편집기에서는 [에이전트 유형](https://code.visualstudio.com/docs/agents/overview#_types-of-agents)을 선택하여 로컬 에이전트, Copilot CLI, Claude 에이전트에 대한 커스터마이징을 관리할 수 있습니다.

## 커스터마이징 문제 해결

커스터마이징이 적용되지 않거나 예상치 못한 동작이 발생하면 채팅 보기의 줄임표(...) 메뉴에서 `Show Agent Debug Logs`를 선택하여 [에이전트 문제 해결](https://code.visualstudio.com/docs/agents/agent-troubleshooting/troubleshooting) 로그를 확인하세요.

## 관련 자료

- [Customization concepts](https://code.visualstudio.com/docs/agents/concepts/customization)
- [Customize AI for your project guide](https://code.visualstudio.com/docs/agents/guides/customize-copilot-guide)
