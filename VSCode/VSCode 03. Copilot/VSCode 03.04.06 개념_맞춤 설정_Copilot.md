# VS Code Copilot 커스터마이제이션 개요 정리

## 개요

Copilot의 AI는 일반적인 지식을 가지고 있지만 프로젝트별 규칙, 팀 관행, 코드 구조를 알지는 못합니다. 커스터마이제이션은 AI가 이러한 컨텍스트를 이해하고 일관된 결과를 내도록 도와주는 방법입니다.

## 커스터마이제이션 옵션 요약

- 항상 적용되는 지침: 프로젝트 전체에 규칙을 적용합니다.
- 파일 기반 지침: 파일 패턴이나 설명에 따라 서로 다른 규칙을 적용합니다.
- 프롬프트 파일: 반복하는 작업을 슬래시 명령으로 저장합니다.
- 에이전트 스킬: 다단계 워크플로를 도와주는 도메인별 도구 모음을 제공합니다.
- 커스텀 에이전트: 특정 역할과 도구 제한을 가진 전문 에이전트를 만듭니다.
- MCP: 외부 API, 데이터베이스, 클라우드 서비스에 연결하는 도구를 제공합니다.
- 후크: 에이전트 라이프사이클 지점에서 쉘 명령을 자동으로 실행합니다.
- 에이전트 플러그인: 커뮤니티 또는 팀에서 제공하는 패키지 형태의 커스터마이제이션입니다.

## 커스텀 인스트럭션(Custom instructions)

- Markdown 파일 형태로 코딩 표준과 프로젝트 컨텍스트를 정의합니다.
- 채팅 요청 시 자동으로 포함되므로 매번 규칙을 반복할 필요가 없습니다.
- 가장 간단하고 시작하기 좋은 커스터마이제이션입니다.

### 종류

- 항상 적용되는 지침(Always-on instructions)
  - `.github/copilot-instructions.md` 파일에 작성합니다.
  - 전체 프로젝트에 적용할 규칙, 코드 스타일, 명명 규칙 등을 정의합니다.
- 파일 기반 지침(File-based instructions)
  - `.instructions.md` 파일로 정의합니다.
  - 파일 경로 패턴이나 작업 설명에 따라 서로 다른 규칙을 적용합니다.
  - 예: `.tsx` 파일에 React 패턴을 적용하거나 백엔드 API 파일에 별도 규칙 적용.

## 프롬프트 파일(Prompt files)

- 자주 사용하는 프롬프트를 재사용 가능한 Markdown 파일로 저장합니다.
- 슬래시 명령으로 채팅에서 쉽게 호출할 수 있습니다.
- 특정 파일, 도구, 컨텍스트를 참조하여 작업에 필요한 정보를 미리 제공합니다.
- 컴포넌트 생성, 테스트 케이스 작성, PR 설명 작성 등 반복 작업에 유용합니다.

## 에이전트 스킬(Agent skills)

- 다단계 작업을 수행하는 도메인별 툴킷입니다.
- 프롬프트 파일과 달리 하나의 특정 프롬프트가 아니라 명령, 스크립트, 리소스를 포함합니다.
- API 문서 생성, 보안 감사, 데이터베이스 마이그레이션 등 복잡한 작업에 적합합니다.
- 오픈 표준(`agentskills.io`) 기반이므로 여러 에이전트 유형에서 작동합니다.

## 커스텀 에이전트(Custom agents)

- AI에 특정 페르소나와 도구 세트를 부여합니다.
- 예: 보안 리뷰어 에이전트는 코드 분석 도구만 사용하고 보안 중심 지침을 따릅니다.
- 각 에이전트는 `.agent.md` 파일로 정의됩니다.
- 사용 가능한 도구, 언어 모델 옵션, 위임 로직 등을 설정할 수 있습니다.
- 다른 에이전트에 위임(delegation)하여 멀티스텝 워크플로를 구성할 수 있습니다.

## MCP (Model Context Protocol)

- MCP는 AI를 외부 도구와 데이터에 연결하는 오픈 표준입니다.
- MCP 서버를 통해 데이터베이스 쿼리, API 호출, 클라우드 서비스 접근 등의 도구를 제공합니다.
- 로컬 또는 원격으로 실행할 수 있으며, 리소스, 프롬프트, 대화형 앱도 함께 제공할 수 있습니다.
- MCP가 없으면 AI는 코드와 터미널 외부의 외부 시스템에 접근할 수 없습니다.

## 후크(Hooks)

- 에이전트 세션의 특정 시점에 쉘 명령을 자동 실행합니다.
- 예: 파일 편집 후 포맷터 실행, 린트 검사를 통과하지 않으면 커밋 차단, 도구 호출 기록 저장.
- 후크는 AI의 행동을 안내하는 지침과 달리 결정적인 결과를 보장합니다.

## 에이전트 플러그인(Agent plugins)

- 커스터마이제이션의 패키지 버전입니다.
- 플러그인을 설치하면 슬래시 명령, 스킬, 커스텀 에이전트, 후크, MCP 서버 등의 조합을 한 번에 적용할 수 있습니다.
- 커뮤니티 모범 사례를 채택하거나 팀 내부 도구를 공유할 때 유용합니다.
- 현재 프리뷰 단계입니다.

## 어떻게 시작할까?

- 프로젝트 전체 규칙이 필요하면 커스텀 인스트럭션으로 시작합니다.
- 반복 작업이 많으면 프롬프트 파일을 추가합니다.
- 외부 API나 데이터가 필요하면 MCP를 연결합니다.
- 특정 역할이 필요한 경우 커스텀 에이전트를 만듭니다.
- 에이전트 라이프사이클에 따라 자동 명령이 필요하면 후크를 구성합니다.

## 관련 자료

- 커스터마이제이션 시작하기: https://code.visualstudio.com/docs/copilot/customization/overview
- 커스텀 인스트럭션: https://code.visualstudio.com/docs/copilot/customization/custom-instructions
- 프롬프트 파일: https://code.visualstudio.com/docs/copilot/customization/prompt-files
- 에이전트 스킬: https://code.visualstudio.com/docs/copilot/customization/agent-skills
- 커스텀 에이전트: https://code.visualstudio.com/docs/copilot/customization/custom-agents
- MCP 서버: https://code.visualstudio.com/docs/copilot/customization/mcp-servers
- 후크: https://code.visualstudio.com/docs/copilot/customization/hooks
- 에이전트 플러그인: https://code.visualstudio.com/docs/copilot/customization/agent-plugins
- 에이전트 개념: https://code.visualstudio.com/docs/copilot/concepts/agents
- 도구 개념: https://code.visualstudio.com/docs/copilot/concepts/tools
- 컨텍스트 개념: https://code.visualstudio.com/docs/copilot/concepts/context

## 도움말 및 지원

- VS Code 커뮤니티 질문
- 기능 요청
- 이슈 보고
