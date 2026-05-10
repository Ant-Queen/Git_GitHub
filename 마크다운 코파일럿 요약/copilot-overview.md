# GitHub Copilot in VS Code - 개요

원문: https://code.visualstudio.com/docs/editor/artificial-intelligence

## 소개

GitHub Copilot은 Visual Studio Code에 AI 에이전트를 가져옵니다. 구축하고 싶은 내용을 설명하면, 에이전트가 접근 방식을 계획하고 코드를 작성한 후 전체 프로젝트에서 결과를 검증합니다. Copilot의 내장 에이전트, Anthropic 및 OpenAI 같은 공급자의 타사 에이전트, 또는 사용자 정의 에이전트를 선택하여 로컬, 백그라운드 또는 클라우드에서 실행할 수 있습니다. 더 작은 변경 사항이나 더 정확한 제어가 필요한 경우, 인라인 제안과 채팅이 편집기에서 직접 정확한 제어를 제공합니다.

## 에이전트 (Agents)

에이전트는 자율적으로 코딩 작업을 완료하는 AI 어시스턴트입니다. 전통적인 코드 완성과 달리 다음 몇 줄을 제안하는 대신, 에이전트는 목표를 받고 이를 단계로 나누고, 프로젝트 전체에서 파일을 편집하고, 명령을 실행하며, 무언가 잘못될 때 자체 수정합니다.

### 에이전트 사용 사례

- **기능 완전히 구축**: 기능을 자연어로 설명하면 에이전트가 프로젝트를 스캐폴딩하고 여러 파일에 걸쳐 논리를 구현하고 테스트를 실행합니다.
- **디버깅 및 실패한 테스트 수정**: 에이전트에 실패한 테스트를 지정하면 오류를 읽고 코드베이스 전체에서 근본 원인을 추적하고 수정을 적용하고 다시 실행합니다.
- **코드베이스 리팩토링 또는 마이그레이션**: 에이전트에게 마이그레이션 계획(예: 한 프레임워크에서 다른 프레임워크로)을 계획하도록 요청하면 파일 전체에 조정된 변경사항을 적용합니다.
- **웹 앱 테스트 및 상호작용(실험)**: 에이전트에게 통합 브라우저에서 웹 앱을 열도록 요청하여 기능을 확인하고 레이아웃 문제를 확인하고 스크린샷을 찍습니다.
- **풀 요청을 통한 협업**: 클라우드 에이전트에 작업을 위임하여 브랜치를 생성하고 변경사항을 구현하고 팀 리뷰를 위해 풀 요청을 엽니다.

### 계획 전에 구축

내장 Plan 에이전트를 사용하여 코드를 작성하기 전에 구조화된 구현 계획으로 작업을 분해합니다. Plan 에이전트는 코드베이스를 분석하고 명확한 질문을 하며 단계별 계획을 생성합니다.

### 어디서나 에이전트 실행

에이전트는 작업이 필요한 위치에서 실행됩니다:
- **로컬(VS Code)**: 대화형 작업에 이상적
- **백그라운드(CLI)**: 자동화된 작업에 이상적
- **클라우드**: GitHub를 통한 팀 협업에 이상적
- **타사 제공자**: Anthropic, OpenAI 등

### 세션 중앙 관리

Chat 패널의 Sessions 뷰에서 모든 활성 세션을 모니터링하고 로컬, 백그라운드, 클라우드에서 실행되는지 여부에 관계없이 세션 간을 전환할 수 있습니다.

### Agents App

전용 인터페이스에서 에이전트 앱을 사용하여 프롬프트, 세션 모니터링, AI 설정 구성에 집중할 수 있습니다.

관련 문서: https://code.visualstudio.com/docs/copilot/agents-app

## 타이핑하면서 AI 지원

더 작은 변경사항이나 더 정확한 제어가 필요한 경우, Copilot이 편집기에서 직접 지원합니다.

### 인라인 제안

Copilot은 입력하면서 코드 제안을 제공합니다(한 줄 완성부터 전체 코드 블록까지). Next edit suggestions은 현재 편집에 따라 다음 논리적 변경을 예측합니다.

관련 문서: https://code.visualstudio.com/docs/copilot/ai-powered-suggestions

### 인라인 채팅

편집기에서 직접 Ctrl+I를 눌러 채팅 프롬프트를 열고, 변경사항을 설명하면 Copilot이 그 자리에서 편집을 제안합니다.

관련 문서: https://code.visualstudio.com/docs/copilot/chat/inline-chat

### 스마트 액션

VS Code는 커밋 메시지 생성, 기호 이름 바꾸기, 오류 수정, 프로젝트 전체 의미론적 검색 등의 일반적인 작업을 위한 미리 정의된 AI 기반 작업을 포함합니다.

관련 문서: https://code.visualstudio.com/docs/copilot/copilot-smart-actions

## 워크플로우에 맞게 AI 커스터마이즈

에이전트는 프로젝트의 규칙을 이해하고, 올바른 도구를 가지고 있고, 작업에 적합한 모델을 사용할 때 가장 잘 작동합니다.

### 커스터마이징 옵션

- **커스텀 지시사항**: 프로젝트 전체 코딩 규칙을 정의하여 AI가 처음부터 스타일과 일치하는 코드를 생성하도록 합니다.
- **에이전트 스킬**: Copilot에 VS Code, GitHub Copilot CLI, GitHub Copilot cloud agent 전체에서 작동하는 전문화된 기능을 가르칩니다.
- **커스텀 에이전트**: 코드 검토자 또는 문서 작성자 같은 특정 역할을 가정하는 에이전트를 만들고, 고유한 도구와 지시사항을 가지도록 합니다.
- **MCP 서버**: MCP 서버 또는 Marketplace 확장의 도구로 에이전트를 확장합니다.
- **훅**: 자동화 및 정책 시행을 위해 특정 이벤트에서 커스텀 명령을 실행합니다.

관련 문서: https://code.visualstudio.com/docs/copilot/customization/overview

## 시작하기

### 1단계: Copilot 설정

상태 표시줄의 Copilot 아이콘 위에 마우스를 올리고 "Set up Copilot"을 선택합니다. 로그인 방법을 선택하고 프롬프트를 따릅니다.

### 2단계: 첫 번째 에이전트 세션 시작

1. Chat 뷰 열기 (Ctrl+Alt+I)
2. 구축하고 싶은 내용을 설명하는 프롬프트 입력
3. 생성된 코드 검토
4. `/init`을 입력하여 프로젝트를 AI용으로 구성

더 자세한 내용: https://code.visualstudio.com/docs/copilot/getting-started

## 지원

GitHub Copilot Chat 지원은 GitHub에서 제공합니다: https://support.github.com

보안, 개인정보, 규정준수, 투명성에 대해 더 알아보려면:
https://copilot.github.trust.page/faq

## 가격

GitHub Copilot은 월간 제한이 있는 무료 버전으로 시작하거나 다양한 유료 요금제 중에서 선택할 수 있습니다.

자세한 정보: https://docs.github.com/en/copilot/get-started/plans

**중요**: 2026년 4월 20일부터 Copilot Pro, Copilot Pro+, 학생 요금제의 새 가입이 일시 중단되고 있으며 주간 사용 제한이 강화되고 있습니다.

## 다음 단계

- [Quickstart: VS Code에서 GitHub Copilot 시작하기](https://code.visualstudio.com/docs/copilot/getting-started)
- [튜토리얼: VS Code에서 에이전트 시작하기](https://code.visualstudio.com/docs/copilot/agents/agents-tutorial)
- [워크플로우에 맞게 AI 커스터마이즈하기](https://code.visualstudio.com/docs/copilot/customization/overview)

---

**최종 업데이트**: 2026년 5월 6일