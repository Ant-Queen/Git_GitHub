# GitHub Copilot in VS Code - 공식 페이지 정리

원문: https://code.visualstudio.com/docs/copilot

## 1. 개요

GitHub Copilot은 Visual Studio Code에 AI 기반 개발 지원 기능을 통합합니다. 자연어로 원하는 작업을 설명하면 Copilot이 계획을 세우고 코드를 작성하며, 필요한 경우 테스트와 검증도 수행합니다.

Copilot은 크게 두 가지 방식으로 동작합니다:
- **에이전트 기반 워크플로우**: 로컬, 백그라운드, 클라우드에서 독립 실행형 작업을 수행하는 AI 세션
- **편집기 기반 지원**: 인라인 제안, 인라인 채팅, 스마트 액션을 통해 코드 작성 중 즉각적인 도움 제공

## 2. Agents (에이전트)

에이전트는 단순한 코드 완성기를 넘어서서 전체 작업을 자율적으로 처리합니다. 목표를 받고 이를 단계로 나누며, 프로젝트 내부 파일을 편집하고, 명령을 실행하고, 오류를 스스로 수정합니다.

### 에이전트 특징
- 작업을 계획하고 여러 파일을 수정
- 필요한 도구를 호출하고 명령을 실행
- 실패를 감지하고 스스로 수정 시도
- 요청과 상태를 세션으로 저장하여 중단/재개 가능

### 에이전트 실행 위치
- **로컬**: VS Code 내부에서 대화형으로 실행
- **백그라운드**: Copilot CLI를 통해 비동기 작업으로 실행
- **클라우드**: GitHub 기반 원격 에이전트로 협업 작업 처리

### 에이전트 활용 사례
- 기능 완전 구현
- 실패한 테스트 디버깅 및 수정
- 코드베이스 리팩토링과 마이그레이션
- 웹 앱 자동 테스트 및 상호작용
- 풀 요청 생성 및 협업

### 세션 관리

Chat 패널의 Sessions 뷰에서 모든 에이전트 세션을 관리합니다. 실행 중인 세션, 상태, 변경 내용, 전략을 한곳에서 확인하고 전환할 수 있습니다.

### Agents App

에이전트 중심 UI를 별도 창으로 제공하는 **Agents App**을 통해 프롬프트, 세션, AI 설정 관리에 집중할 수 있습니다.

관련 링크:
- https://code.visualstudio.com/docs/copilot/agents-app

## 3. What can you build (무엇을 만들 수 있나요)

Copilot 에이전트는 단순한 코드 조각을 넘어서 전체 기능을 구현하거나 문제를 해결할 수 있습니다.

### 대표적인 활용
- **전체 기능 구축**: 설명 한 줄로 프로젝트 스캐폴딩, 기능 구현, 테스트까지 수행
- **테스트 기반 디버깅**: 실패한 테스트를 분석하고 원인 파악 후 코드 수정 및 재실행
- **리팩토링/마이그레이션**: 프레임워크 전환이나 코드 구조 변경을 자동으로 적용
- **웹 앱 자동 테스트**: 통합 브라우저에서 페이지를 열고 클릭, 입력, 레이아웃을 검증
- **풀 요청 생성**: 클라우드 에이전트가 브랜치를 생성하고 PR을 작성

### 추가 활용 예시
- 접근성 검사 및 UI 문제 탐지
- API 통합 테스트 수행
- 상태 관리 및 UX 개선
- 기존 코드베이스에 새로운 기능 추가

## 4. Getting started (시작하기)

### Copilot 설정
1. VS Code 상태 표시줄에서 Copilot 아이콘 위에 마우스를 올림
2. `Set up Copilot` 선택
3. 로그인 방법을 선택하고 구독 또는 무료 플랜 등록

### 첫 에이전트 세션 시작
1. Chat 뷰 열기 (`Ctrl+Alt+I`)
2. 원하는 작업을 자연어로 입력
3. 생성된 코드와 변경 내용을 확인
4. `/init` 입력으로 프로젝트를 AI용으로 초기화

### 추천 흐름
- 새로운 기능을 한 줄로 설명하고 구현 요청
- 생성된 파일과 변경 사항을 리뷰
- 필요 시 추가 요구 사항을 넣어 반복

관련 링크:
- https://code.visualstudio.com/docs/copilot/getting-started

## 5. AI assistance as you type (타이핑 중 AI 지원)

코드 작성 중 Copilot은 다양한 방식으로 도움을 줍니다.

### 인라인 제안
- 자동 완성 형태로 코드 추천
- 한 줄 또는 전체 블록 완성
- `Tab`으로 수락
- 주석 기반 힌트로 원하는 구조를 제시 가능

### 인라인 채팅
- 편집기에서 `Ctrl+I`로 즉시 채팅 열기
- 선택한 코드 또는 현재 문맥을 기반으로 변경 제안
- 순간적인 리팩토링, 설명, 수정 요청에 유리

### 스마트 액션
- 커밋 메시지 생성
- 코드 오류 수정
- 기호 이름 변경 제안
- 테스트 생성 및 실패 수정
- Markdown alt 텍스트 생성
- 코드 검토 및 리뷰

관련 링크:
- https://code.visualstudio.com/docs/copilot/ai-powered-suggestions
- https://code.visualstudio.com/docs/copilot/chat/inline-chat
- https://code.visualstudio.com/docs/copilot/copilot-smart-actions

## 6. Customize AI for your workflow (워크플로우 맞춤 AI)

Copilot은 기본 동작 외에도 프로젝트별 규칙과 도구를 연결하여 맞춤형 AI 환경을 제공합니다.

### 주요 구성 요소
- **Custom Instructions**: 프로젝트 코딩 스타일, 명명 규칙, 아키텍처 기준 등을 정의
- **Agent Skills**: 반복 작업과 전문 기능을 재사용 가능한 스킬로 패키징
- **Custom Agents**: 특정 역할과 도구 세트를 가진 에이전트를 생성
- **MCP Servers**: 외부 데이터, API, 브라우저 자동화 도구를 AI에 연결
- **Hooks**: 에이전트 작업 흐름 중 지정된 시점에 자동화 실행

관련 링크:
- https://code.visualstudio.com/docs/copilot/customization/overview

## 7. Support & Pricing (지원 및 가격)

### 지원
- GitHub Copilot Chat 지원: https://support.github.com
- Copilot 신뢰 센터 FAQ: https://copilot.github.trust.page/faq

### 가격
- **Copilot Free**: 월별 제한된 인라인 제안 및 채팅 사용 가능
- **유료 플랜**: 더 많은 사용량과 고급 기능 제공
- **2026년 4월 20일 공지**: Copilot Pro, Pro+, 학생 요금제 신규 가입 일시 중단 및 주간 사용 제한 강화

관련 링크:
- https://docs.github.com/en/copilot/get-started/plans

## 8. Next steps (다음 단계)

- [Quickstart: VS Code에서 GitHub Copilot 시작하기](https://code.visualstudio.com/docs/copilot/getting-started)
- [튜토리얼: VS Code에서 에이전트 시작하기](https://code.visualstudio.com/docs/copilot/agents/agents-tutorial)
- [워크플로우에 맞게 AI 커스터마이즈하기](https://code.visualstudio.com/docs/copilot/customization/overview)

---

**최종 업데이트**: 2026년 5월 9일