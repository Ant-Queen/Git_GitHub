# VS Code Copilot 개념 개요 정리

## 개요

Visual Studio Code의 AI 기능은 GitHub Copilot과 대형 언어 모델(LLM)을 기반으로 합니다. 이 기능은 여러 상호작용 방식으로 제공되며, 간단한 인라인 제안부터 에이전트를 통한 전체 기능 구현까지 다양한 워크플로를 지원합니다.

## 한눈에 보는 AI 기능

- 에이전트(Agents): 파일 읽기, 다중 파일 변경, 명령 실행, 반복 개선을 수행하는 자율 세션입니다. 전체 기능 구현, 리팩터링, 마이그레이션 같은 멀티스텝 작업에 적합합니다.
- 채팅(Chat): 에이전트와 다중 대화를 나누는 기본 인터페이스입니다. 작업 할당, 질문, 아이디어 탐색, 설명 요청 등에 사용합니다. Agent, Ask, Plan, 사용자 정의 에이전트 간 전환할 수 있습니다.
- 인라인 채팅(Inline chat): 에디터 내부에서 바로 열리는 가벼운 채팅 인터페이스로, 빠르고 집중된 코드 수정에 적합합니다.
- 인라인 제안(Inline suggestions): 입력 중에 고스트 텍스트 형태로 나타나는 코드 제안입니다. 에이전트 루프나 도구를 사용하지 않고, 특수화된 완성 모델을 이용합니다. Next edit suggestions(NES)는 다음 편집 위치까지 예측합니다.
- 스마트 액션(Smart actions): 커밋 메시지 생성, 진단 오류 수정 등 워크플로에 통합된 원클릭 AI 작업입니다.

## 핵심 개념

- 언어 모델(Language models): 모든 AI 기능의 기반이 되는 모델입니다. 어떤 모델을 선택하고 구성할지 결정합니다.
- 컨텍스트(Context): 모델이 사용하는 정보입니다. 파일 콘텐츠, 대화 기록, 코드베이스 상태 등이 포함됩니다.
- 도구(Tools): 에이전트가 개발 환경에서 동작하거나 외부 서비스와 연결할 수 있게 해주는 메커니즘입니다.
- 에이전트(Agents): 에이전트 루프, 에이전트 유형, 서브에이전트, 메모리, 계획 수립 등 에이전트 작동 원리를 설명합니다.
- 맞춤화(Customization): 명령어, 프롬프트 파일, 커스텀 에이전트, 스킬, 후크, 플러그인 등으로 AI 동작을 사용자 맞춤형으로 조정하는 방법입니다.
- 신뢰 및 안전(Trust and safety): 제어 메커니즘, AI 한계, 보안 고려 사항을 다룹니다.

## 관련 자료

- Copilot 시작하기: https://code.visualstudio.com/docs/copilot/getting-started
- VS Code에서 에이전트 사용하기: https://code.visualstudio.com/docs/copilot/agents/overview
- AI 기능 사용 모범 사례: https://code.visualstudio.com/docs/copilot/best-practices

## 도움말 및 지원

- Copilot 관련 커뮤니티 질문
- 기능 요청
- 이슈 보고


※ 이 문서는 VS Code의 AI 기능 개요를 빠르게 이해하기 위한 요약본입니다.