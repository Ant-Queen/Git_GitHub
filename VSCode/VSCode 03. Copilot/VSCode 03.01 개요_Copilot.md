# VS Code Copilot 개요 정리

## 개요

GitHub Copilot은 VS Code에서 AI 기반 코딩 지원을 제공합니다. 사용자는 자연어로 원하는 작업을 설명하면 에이전트가 계획을 세우고, 코드 변경을 적용하고, 테스트 실행을 통해 결과를 검증합니다.

Copilot은 다음과 같은 방식으로 동작합니다.

- 빌트인 에이전트
- 타사 에이전트(Anthropic, OpenAI 등)
- 커스텀 에이전트
- 로컬, 백그라운드, 클라우드에서 실행

## Agents (에이전트)

### 에이전트란?

에이전트는 자율적으로 코딩 작업을 수행하는 AI 도우미입니다. 단순 코드 완성이 아니라 목표를 받아 작업을 분해하고, 여러 파일을 편집하고, 명령을 실행하며 스스로 수정합니다.

### 주요 기능

- 작업을 목표로 받아 단계별 계획 수립
- 에이전트 세션 내에서 지속적인 대화 유지
- 작업을 중단, 재개, 다른 에이전트로 전달 가능

### 에이전트 실행 위치

- 로컬: VS Code에서 인터랙티브 작업
- 백그라운드: 자동화된 작업
- 클라우드: 풀 리퀘스트 기반 팀 협업

### 세션 관리

- 여러 에이전트 세션을 병렬로 실행 가능
- Chat 패널의 Sessions 뷰에서 상태 확인, 파일 변경 검토, 세션 전환

### Agents Window (Preview)

- 에디터 중심 창과 에이전트 중심 창을 선택해서 사용 가능
- 에이전트 중심 창은 프롬프트 기반 작업과 세션 조율에 적합
- 변경 사항 검토, AI 커스터마이제이션(에이전트, 스킬, 설명, 후크, MCP 서버) 접근 가능
- SSH 또는 dev tunnel을 통해 원격 세션을 모니터링하거나 브라우저에서 세션 확인 가능

## What can you build (무엇을 만들 수 있나)

### 대표 사용 사례

- 기능 전체 구현: 자연어로 기능을 설명하여 프로젝트 전체를 설계하고 구현
- 테스트 디버깅: 실패한 테스트를 분석하고 원인 파악, 수정 후 재실행
- 리팩터링/마이그레이션: 코드베이스를 일괄적으로 수정하거나 프레임워크를 이전
- 웹 앱 테스트(실험적): 통합 브라우저에서 기능 검증, 레이아웃 문제 점검, 스크린샷 촬영
- 풀 리퀘스트 협업: 클라우드 에이전트가 브랜치 생성, 변경 구현, PR 생성

## Getting started (시작하기)

### 1단계: Copilot 설정

1. 상태 표시줄의 Copilot 아이콘 위에 마우스를 올리고 `Set up Copilot` 선택
2. 로그인 방법 선택 후 안내에 따라 가입 또는 인증
3. Copilot Free 플랜 또는 기존 유료 플랜 사용

> 2026년 4월 20일부터 Copilot Pro, Pro+, Max, Student 플랜 신규 가입이 일시 중지될 수 있습니다.

### 2단계: 첫 에이전트 세션 시작

1. Chat 뷰 열기: `Ctrl+Alt+I`
2. 원하는 작업을 자연어로 입력
3. 생성된 코드를 검토
4. `/init` 입력으로 AI 맞춤 설정 생성

## AI assistance as you type (타이핑 중 AI 지원)

### Inline suggestions (인라인 제안)

- 한 줄 완성부터 전체 함수 구현까지 코드 제안을 받음
- 현재 수정 방향에 따른 다음 논리적 변경을 예측

### Inline chat (인라인 채팅)

- `Ctrl+I`로 에디터 내 채팅 입력창 열기
- 특정 리팩터, 설명, 수정 요청을 빠르게 수행
- 컨텍스트 전환 없이 에디터에서 직접 작업

### Smart actions (스마트 작업)

- 일반적인 작업을 위한 AI 액션 제공
- 커밋 메시지 생성, 기호 이름 변경, 오류 수정, 프로젝트 전체 의미 검색 등

## Customize AI for your workflow (워크플로우 맞춤 설정)

Copilot은 프로젝트 규칙, 도구, 모델을 맞춤 구성할 수 있습니다.

### 주요 맞춤 항목

- Custom instructions: 프로젝트별 코딩 컨벤션 정의
- Agent skills: Copilot에 특화된 기능을 학습시킴
- Custom agents: 코드 리뷰어, 문서 작성자 등 특정 역할을 수행하는 에이전트 생성
- MCP servers: MCP 서버 또는 마켓플레이스 확장 도구를 통해 에이전트를 확장
- Hooks: 특정 이벤트에 명령을 실행하여 자동화 및 정책 적용

## Support (지원)

- GitHub Copilot Chat 지원: `https://support.github.com`
- Copilot 보안/개인정보/규정 관련 정보: GitHub Copilot Trust Center FAQ

## Pricing (요금)

- Copilot은 무료로 기본 인라인 제안과 AI 크레딧을 제공합니다.
- 유료 플랜은 더 많은 AI 크레딧을 제공합니다.
- 자세한 요금은 GitHub Copilot 요금 페이지에서 확인 가능합니다.

## Next steps (다음 단계)

- Quickstart: `https://code.visualstudio.com/docs/copilot/getting-started`
- Agents tutorial: `https://code.visualstudio.com/docs/copilot/agents/agents-tutorial`
- Customize AI: `https://code.visualstudio.com/docs/copilot/customization/overview`
