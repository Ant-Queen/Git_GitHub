# VS Code의 에이전트 사용 가이드

원문: 
- Overview: https://code.visualstudio.com/docs/copilot/agents/overview
- Tutorial: https://code.visualstudio.com/docs/copilot/agents/agents-tutorial
- Planning: https://code.visualstudio.com/docs/copilot/agents/planning
- Cloud Agents: https://code.visualstudio.com/docs/copilot/agents/cloud-agents

## 에이전트란?

에이전트는 자율적으로 코딩 작업을 완료하는 AI 어시스턴트입니다. 높은 수준의 목표를 설명하면, 에이전트는 목표를 단계로 나누고, 프로젝트 전체에서 파일을 편집하고, 명령을 실행하며, 무언가 잘못될 때 자체 수정합니다.

예를 들어, 실패한 테스트를 제안하는 대신, 에이전트는 근본 원인을 식별하고, 코드를 수정하고, 테스트를 다시 실행하고, 변경사항을 커밋합니다.

## 에이전트 타입

### 선택 기준 표

| 작업 | 추천 에이전트 |
|------|-------------|
| 아이디어를 상호작용적으로 브레인스토밍, 탐색 또는 반복 | 로컬 에이전트 |
| 코드베이스에 대한 답변 얻기 | 로컬 에이전트 (Ask) |
| 구조화된 구현 계획 만들기 | 로컬 에이전트 (Plan) |
| 편집기 컨텍스트가 필요한 문제 해결(테스트 실패, 린팅 오류) | 로컬 에이전트 |
| 통합 브라우저로 웹 앱 구축 및 테스트 | 로컬 에이전트 |
| VS Code 확장 도구 또는 MCP 서버 사용 | 로컬 에이전트 |
| 계속 작업하는 동안 잘 정의된 작업 구현 | Copilot CLI 또는 클라우드 에이전트 |
| 여러 변형 또는 개념증명 탐색 | Copilot CLI 또는 클라우드 에이전트 |
| 팀 검토 및 협업을 위한 PR 만들기 | 클라우드 에이전트 |
| GitHub 이슈를 에이전트에 할당 | 클라우드 에이전트 |
| 특정 AI 제공자 사용(Anthropic, OpenAI) | 타사 에이전트 |

### 에이전트 타입 상세 설명

#### 1. 로컬 에이전트 (Local Agent)
- VS Code 에이전트 루프를 사용하여 편집기에서 대화식으로 실행
- 워크스페이스, 도구, 모델에 완벽히 접근 가능
- 즉각적인 피드백과 반복이 필요한 작업에 이상적

#### 2. Copilot CLI (백그라운드 에이전트)
- 머신에서 백그라운드로 실행
- Git 워크트리를 선택사항으로 사용하여 파일 변경 격리
- 계속 작업하는 동안 자동화된 작업에 이상적

#### 3. 클라우드 에이전트
- 원격 인프라에서 실행
- GitHub 풀 요청과 통합하여 팀 협업
- 잘 정의된 범위와 모든 필요한 컨텍스트가 있는 작업에 이상적

#### 4. 타사 에이전트
- Anthropic, OpenAI 등의 제공자
- 로컬 또는 클라우드에서 실행 가능

## 에이전트 선택하기

### 에이전트 타입 선택
Chat 뷰의 에이전트 대상 드롭다운에서 에이전트 타입을 선택합니다.

### 에이전트 선택
Chat 뷰의 에이전트 드롭다운에서 특정 에이전트를 선택합니다.

#### 내장 에이전트

- **Agent**: 파일 전체에서 자율적으로 계획하고 구현, 터미널 명령 실행, 도구 호출
- **Plan**: 구현 계획 생성
- **Ask**: 코딩 개념, 코드베이스, VS Code에 대한 질문에 답변 (파일 변경 없음)

#### 커스텀 에이전트
구체적인 역할을 가정하는 에이전트를 만들고, 고유한 도구와 지시사항을 정의합니다.

더 자세한 내용: https://code.visualstudio.com/docs/copilot/customization/custom-agents

## 권한 수준 선택

에이전트는 자율적으로 작업하지만, 도구 및 터미널 명령 호출에 대한 자율성을 제어할 수 있습니다.

| 권한 수준 | 설명 |
|----------|------|
| 기본 승인 (Default Approvals) | VS Code 설정의 기본값 사용. 기본적으로 읽기 전용 및 안전 도구는 명시적 승인 필요 없음 |
| 승인 우회 (Bypass Approvals) | 확인 없이 모든 도구 호출 자동 승인. 에이전트가 질문을 할 수 있음 |
| 자동 조종 (Autopilot - Preview) | 모든 도구 호출 자동 승인, 질문 자동 응답, 작업 완료까지 자율적으로 계속 |

영구적 설정: `chat.permissions.default` 설정 구성

## 세션 간 에이전트 핸드오프

한 에이전트에서 다른 에이전트로 진행 중인 작업을 핸드오프합니다:

1. 로컬 에이전트 세션에서 Chat 뷰의 세션 타입 드롭다운에서 다른 에이전트 타입 선택
2. Copilot CLI 세션에서 `/delegate` 명령 입력
3. 클라우드 에이전트로 위임

VS Code는 새 세션을 생성하고 전체 대화 기록과 컨텍스트를 이어갑니다.

## Plan 에이전트로 작업 계획하기

### 작업 계획 방법

1. Chat 뷰 열기 (Ctrl+Alt+I)
2. 에이전트 드롭다운에서 Plan 선택
3. 높은 수준의 작업 설명(기능, 리팩토링, 버그 등) 입력
4. 명확한 질문에 답변
5. Plan 에이전트가 높은 수준의 계획 요약, 구현 및 검증 단계 생성
6. 계획을 반복하고 완료되면 구현 시작

### Plan 에이전트 커스터마이징

- 커스텀 계획 에이전트 생성 및 특정 지시사항 정의
- `chat.planAgent.defaultModel` 설정으로 기본 모델 선택
- `github.copilot.chat.implementAgent.model` 설정으로 구현 단계 모델 선택
- `github.copilot.chat.planAgent.additionalTools` 설정으로 추가 도구 추가

관련 문서: https://code.visualstudio.com/docs/copilot/agents/planning

## 클라우드 에이전트

### GitHub Copilot 클라우드 에이전트

GitHub 인프라에서 실행되는 주요 클라우드 에이전트입니다.

주요 기능:
- GitHub 리포지토리 전체 대규모 리팩토링
- 높은 수준의 요구사항에서 완전한 기능 구현
- 자동 풀 요청 생성 및 상세한 설명
- 코드 검토 통합 및 피드백 대응

### 타사 클라우드 에이전트

Claude 코딩 에이전트, Codex 코딩 에이전트 등의 옵션도 있습니다.

### 클라우드 에이전트 세션 시작

#### 새로운 클라우드 에이전트 세션 생성

1. Chat 뷰에서 세션 목록 드롭다운의 "New Chat" 선택
2. 세션 타입 드롭다운에서 Cloud 선택
3. 클라우드 에이전트 제공자 선택 및 프롬프트 입력

예제 프롬프트:
```
리팩토링 및 보안 강화: 인증 모듈을 리팩토링하여 보안 및 성능을 개선합니다. 
OAuth2 및 JWT를 구현하고 사용자 세션에 대한 데이터베이스 쿼리를 최적화합니다.
```

#### 로컬/백그라운드 에이전트에서 클라우드 에이전트로 핸드오프

1. Chat 뷰에서 진행 중인 로컬 에이전트 세션 열기
2. 세션 타입 드롭다운에서 Cloud 선택
3. 전체 대화 컨텍스트가 클라우드 에이전트로 전달됨

Plan 에이전트 사용 시, "Start Implementation" 드롭다운에서 "Continue in Cloud" 선택.

### 클라우드 에이전트 세션 보기 및 관리

Chat 뷰에서 세션 목록을 필터링하여 클라우드 에이전트 세션만 표시:

1. Chat 뷰의 세션 필터에서 "Cloud Agents" 선택
2. 세션 선택하여 Chat 뷰에서 세션 상세 정보 열기
3. 선택사항: 세션 우클릭 > "Open as Editor"로 에디터 탭으로 열기

관련 문서: https://code.visualstudio.com/docs/copilot/agents/cloud-agents

## 에이전트 튜토리얼: 실습 가이드

### 1단계: 로컬 에이전트로 앱 스캐폴딩

기본 TODO 앱 구조 만들기:

1. 새 프로젝트 폴더 생성 및 Git 초기화
   ```bash
   mkdir todo-app
   cd todo-app
   git init
   ```

2. VS Code에서 폴더 열기

3. Chat 뷰 열기 (Ctrl+Alt+I) 및 에이전트 드롭다운에서 Agent 선택

4. 프롬프트 입력:
   ```
   Create a simple todo app with HTML, CSS, and JavaScript. 
   Include an input field to add todos, a list to display them, 
   and a delete button for each item.
   ```

5. 에이전트가 파일을 생성하면서 "Keep" 또는 "Undo"로 변경사항 수락/거부

6. Live Preview 확장이 설치되어 있다면 index.html을 미리 보기로 볼 수 있음

추가 프롬프트로 기능 향상:
```
Mark todos as completed with a strikethrough effect.
```

### 2단계: Copilot CLI로 기능 계획 및 구현

백그라운드에서 계획 실행:

1. 현재 변경사항을 Source Control 뷰에서 커밋

2. Chat 뷰에서 "New Chat" > 새 로컬 에이전트 세션 시작

3. 에이전트 드롭다운에서 Plan 선택

4. 계획 프롬프트:
   ```
   Create a plan to add a dark/light theme toggle to the app. 
   The toggle should switch between themes and persist the user's preference.
   ```

5. 명확한 질문에 답변

6. 계획이 마음에 들면 "Start Implementation" > "Continue in Copilot CLI" 선택

7. Copilot CLI가 Git 워크트리를 생성하고 구현 시작

8. Sessions 뷰에서 진행 상황 추적

9. 완료되면 변경사항 검토 후 "Apply" 선택

### 3단계: 클라우드 에이전트로 협업 기능 추가

GitHub를 통해 팀 협업:

1. 프로젝트를 GitHub 리포지토리로 발행

2. Chat 뷰에서 "New Chat" > Cloud 선택

3. 프롬프트:
   ```
   Redesign the todo app layout to improve user experience. 
   Update colors, spacing, typography, and add animations 
   to give it a modern look.
   ```

4. 클라우드 에이전트가 브랜치와 풀 요청을 GitHub에서 생성

5. Sessions 뷰 또는 GitHub PR 확장에서 진행 상황 추적

6. 완료 후 풀 요청 검토 후 병합

관련 문서: https://code.visualstudio.com/docs/copilot/agents/agents-tutorial

---

**최종 업데이트**: 2026년 5월 6일