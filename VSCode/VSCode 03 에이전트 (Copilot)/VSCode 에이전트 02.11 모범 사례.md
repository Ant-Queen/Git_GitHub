# VS Code에서 AI 사용 시 모범 사례

이 문서는 Visual Studio Code에서 AI를 효과적으로 사용하는 방법에 대한 권장사항을 설명합니다. 각 섹션은 행동 가능한 지침과 참고 문서를 제공합니다.

## AI에 맞게 프로젝트 최적화하기

프로젝트와 코드베이스를 AI 친화적으로 구성하면 AI 응답의 정확도를 높이고 팀의 코딩 표준과 관행을 더 잘 따르게 할 수 있습니다.

VS Code는 여러 가지 AI 행동 구성 메커니즘을 지원합니다. 채팅에서 `/init`을 입력하면 프로젝트용 시작 구성 파일을 생성할 수 있습니다.

- 커스텀 지침: 프로젝트 전체 코딩 표준 및 아키텍처 컨텍스트
- 커스텀 에이전트: TDD, 보안 감사 등 특화된 워크플로우 또는 페르소나
- 스킬: 테스트, 배포 등 도메인별 기능
- 도구 및 MCP 서버: 데이터베이스, API, CLI 등 외부 시스템 연결

효과적인 프로젝트 구성 팁:

- 지침 파일을 간결하게 유지하세요. 채팅마다 로드되므로 핵심 정보만 담습니다.
- 비표준 규칙, 아키텍처 결정, 환경 설정처럼 코드에서 추론하기 어려운 정보를 포함하세요.
- `applyTo` 패턴으로 언어별 또는 폴더별 지침을 분리하세요.
- 활성 도구 수를 제한하세요. 필요한 경우에만 도구를 사용하면 더 빠르고 관련성 높은 응답을 얻을 수 있습니다.

자세한 설정은 [customization overview](https://code.visualstudio.com/docs/agent-customization/overview)를 참조하세요.

## 작업에 적합한 도구 선택하기

VS Code AI에는 여러 상호작용 모드가 있습니다. 작업에 맞는 모드를 선택하면 시간 절약과 더 나은 결과를 얻을 수 있습니다.

- 인라인 제안: 코드 작성 흐름 유지, 변수 이름 및 보일러플레이트 생성
- 질문(채팅): 질문, 브레인스토밍, 아이디어 탐색
- 인라인 채팅: 컨텍스트를 전환하지 않고 위치 중심 편집
- 에이전트: 자율 계획과 도구 사용이 필요한 다중 파일 변경
- Plan: 구현 전에 구조화된 계획 수립
- Smart actions: 커밋 메시지 생성, 오류 수정, 심볼 이름 변경 같은 한 단계 작업

## 적절한 에이전트 유형 선택하기

에이전트 작업 시 작업과 워크플로우에 맞는 유형을 선택하세요. 각 유형은 대화형성, 속도, 분리성에서 차이가 있습니다.

- 로컬 에이전트: 대화형 작업에 적합, 워크스페이스 및 도구에 전체 액세스
- 백그라운드 에이전트: 작업이 명확할 때 구현을 오프로드
- 클라우드 에이전트: 팀 협업, 풀 리퀘스트 생성, GitHub 이슈 할당에 적합
- 병렬 세션: 독립적인 작업을 동시에 여러 세션으로 실행
- 에이전트 간 핸드오프: 로컬 에이전트로 탐색 및 계획 후 백그라운드/클라우드 에이전트로 구현

자세한 내용은 [using agents](https://code.visualstudio.com/docs/agents/overview)와 [agents tutorial](https://code.visualstudio.com/docs/agents/agents-tutorial)를 참고하세요.

## 효과적인 프롬프트 작성하기

AI 응답 품질은 프롬프트의 명확성과 구체성에 달려 있습니다.

- 입력, 출력, 제약 조건을 구체적으로 명시하세요. 언어, 프레임워크, 라이브러리와 기대 동작을 포함합니다.
- 복잡한 작업은 잘게 나누세요. 전체 기능을 한 번에 요청하기보다 작은 단계로 분할하면 더 안정적입니다.
- 검증을 위한 예상 출력물 제공: 테스트 케이스, 예상 결과, 수용 기준 등을 포함하세요.
- 모호한 프롬프트는 피하세요. 예: "더 좋게 만들어" 대신 "시간 복잡도를 줄이세요" 또는 "null 값 입력 검증 추가" 등으로 설명합니다.
- 후속 프롬프트로 반복 개선하세요. 잘못된 방향이 보이면 전체 프롬프트를 다시 작성하기보다 추가 메시지로 수정합니다.
- 명확하지 않은 작업은 AI가 먼저 질문하도록 지시하세요.
- 병렬 작업이 있을 때는 병렬 실행을 요청하여 시간을 절약할 수 있습니다.

실용적 프롬프트 예시는 GitHub Copilot 문서에서 확인할 수 있습니다.

## 올바른 컨텍스트 제공하기

적절한 컨텍스트는 AI 응답의 정확도를 높입니다.

- AI는 관련 컨텍스트를 자동으로 검색하지만, 불분명할 때는 파일, 폴더, 심볼을 `#<file>`, `#<folder>`, `#<symbol>`로 참조하세요.
- 웹 페이지나 GitHub 저장소 정보를 가져오려면 `#fetch`를 사용하세요.
- 소스 제어 변경 사항, 터미널 출력, 테스트 실패 등 VS Code 환경 컨텍스트를 참고하여 현재 상태를 알려주세요.
- 이미지나 스크린샷을 추가해 시각적 콘텐츠를 분석하게 할 수 있습니다.
- [통합 브라우저](https://code.visualstudio.com/docs/debugtest/integrated-browser)를 사용해 앱을 미리 보고 페이지 요소를 선택하여 컨텍스트로 사용할 수 있습니다.

자세한 내용은 [adding context to chat prompts](https://code.visualstudio.com/docs/chat/copilot-chat-context) 및 [configuring tools](https://code.visualstudio.com/docs/agents/agent-tools)를 참고하세요.

## 적절한 모델 선택하기

모델마다 강점이 다릅니다. 작업에 맞는 모델을 선택하면 결과가 개선됩니다.

- 작업 복잡도에 맞게 모델 선택: 간단한 작업은 빠른 모델, 계획/디버깅/아키텍처 결정은 추론 최적화 모델
- 최신 모델 사용: 새로운 모델이 기능이 개선된 경우가 많습니다.
- 프롬프트 파일과 에이전트에 모델 고정: 특정 작업에 일관된 모델이 사용되도록 설정
- 실험하고 비교: 같은 프롬프트로 다른 모델을 사용해 결과를 비교해 보세요.
- 추론 노력 조정: 복잡한 작업은 더 높은 thinking effort, 단순 작업은 낮은 effort
- BYOK(자체 API 키) 사용으로 모델 선택과 호스팅 옵션을 확장
- AI 크레딧 소비 고려: 더 강력한 모델은 더 많은 크레딧을 사용합니다.

자세한 내용은 [selecting AI models](https://code.visualstudio.com/docs/agent-customization/language-models)과 [available models for Copilot Chat](https://docs.github.com/en/copilot/using-github-copilot/ai-models/changing-the-ai-model-for-copilot-chat)을 확인하세요.

## 먼저 계획하고 구현하기

여러 파일에 걸친 복잡한 변경은 먼저 계획을 세우고 구현하는 방식이 좋습니다.

1. 탐색: ask 모드 또는 서브에이전트를 사용해 관련 코드를 읽고 이해합니다.
2. 계획: [Plan agent](https://code.visualstudio.com/docs/agents/planning)를 사용해 구조화된 구현 계획을 만듭니다.
3. 구현: 계획에 따라 에이전트 모드로 구현하고, 테스트나 예상 출력을 포함해 자체 검증하도록 합니다.
4. 검토: [체크포인트](https://code.visualstudio.com/docs/chat/chat-checkpoints)를 사용해 진행을 검토하고, 필요하면 되돌리거나 Copilot 코드 리뷰를 요청합니다.

자세한 워크플로우는 [context engineering workflow](https://code.visualstudio.com/docs/agents/guides/context-engineering-guide)를 참조하세요.

## AI 출력 검토 및 검증하기

AI가 생성한 코드는 버그, 보안 문제, 논리 오류가 있을 수 있습니다. 항상 출력을 시작점으로 보고 검토하세요.

- 수락 전에 검토하세요. 생성된 코드를 읽고 에지 케이스, 오류 처리, AI가 가정한 내용을 확인합니다.
- AI 변경 후 테스트를 실행하세요. 프롬프트에 테스트 케이스를 포함해 AI가 스스로 검증하도록 합니다.
- 체크포인트를 사용해 에이전트가 벗어난 경우 되돌리세요.
- 보안 문제를 확인하세요. 주입 취약성, 하드코딩된 비밀, 입력 검증 누락 등을 점검합니다.

자세한 내용은 [GitHub Copilot security](https://code.visualstudio.com/docs/agents/security) 및 [GitHub Copilot Trust Center](https://copilot.github.trust.page/faq)를 참고하세요.

## 컨텍스트 및 세션 관리하기

대화가 불필요한 컨텍스트로 채워지면 응답 품질이 떨어질 수 있습니다.

- 관련 없는 작업은 새 세션에서 시작하세요.
- 더 이상 관련 없는 이전 질문과 응답은 삭제하거나 새 세션을 시작하세요.
- 컨텍스트 압축을 사용하세요. `/compact`를 사용해 가장 관련성 높은 정보만 유지합니다.
- 조사나 탐색을 위해 서브에이전트를 사용하면 메인 컨텍스트가 어질러지지 않습니다.
- 적절한 세션 유형을 선택하세요: 로컬 세션은 빠른 현재 코드 작업, 백그라운드 세션은 별도 실행 작업, 클라우드 세션은 팀 협업에 적합합니다.
- 병렬 세션으로 독립 작업을 분리하세요.
- 다시 시작하기보다 `/fork`를 사용해 대안을 탐색하세요.

자세한 내용은 [session management](https://code.visualstudio.com/docs/agents/sessions/chat-sessions), [workspace indexing](https://code.visualstudio.com/docs/agents/reference/workspace-context), [optimize AI credit usage](https://code.visualstudio.com/docs/agents/guides/optimize-usage)를 참고하세요.

## 큰 코드베이스 작업하기

Copilot은 대규모 복잡한 워크스페이스에서도 효과적으로 작동하도록 설계되었습니다.

- 워크스페이스 인덱싱 사용: VS Code는 의미론적 검색, 언어 인텔리전스, GitHub 코드 검색을 사용해 프로젝트를 인덱싱합니다.
- 멀티 루트 워크스페이스 사용: 모노레포나 여러 서비스가 있는 프로젝트에서 명확한 경계를 제공합니다.
- 프로젝트 수준 지침 제공: 코드만으로 추론하기 어려운 아키텍처, 모듈 경계, 컨벤션 정보를 커스텀 지침에 담으세요.
- 독립 변경 작업을 병렬 세션으로 실행하세요.
- 많은 파일에 걸친 변경은 [Plan agent](https://code.visualstudio.com/docs/agents/planning)를 먼저 사용하세요.

자세한 내용은 [workspace context](https://code.visualstudio.com/docs/agents/reference/workspace-context) 및 [agents](https://code.visualstudio.com/docs/agents/overview)를 확인하세요.

## 관련 자료

- [Context engineering guide](https://code.visualstudio.com/docs/agents/guides/context-engineering-guide)
- [Customization overview](https://code.visualstudio.com/docs/agent-customization/overview)
- [Cheat sheet](https://code.visualstudio.com/docs/agents/reference/copilot-vscode-features)
- [GitHub Copilot security](https://code.visualstudio.com/docs/agents/security)
- [Best Practices for using GitHub Copilot](https://docs.github.com/en/copilot/using-github-copilot/best-practices-for-using-github-copilot)
