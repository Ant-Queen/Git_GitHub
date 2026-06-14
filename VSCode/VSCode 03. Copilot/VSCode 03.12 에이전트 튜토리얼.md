# VS Code Copilot 에이전트 튜토리얼

## 개요

이 튜토리얼은 VS Code에서 여러 에이전트 유형을 사용하여 Todo 앱을 만들고 개선하는 방법을 안내합니다. 로컬 에이전트, Copilot CLI, 클라우드 에이전트를 순차적으로 사용하며 각 워크플로를 체험합니다.

## 사전 준비

- VS Code 설치
- Live Preview 확장 설치 (Todo 앱 미리보기용)
- GitHub 계정
- GitHub Copilot 구독

## 1단계: 로컬 에이전트로 앱 골격 만들기

### 목적
- 로컬 에이전트를 사용해 HTML/CSS/JavaScript 기반 Todo 앱의 초기 구조를 생성합니다.
- 즉시 피드백과 실시간 코드 편집이 필요한 인터랙티브 작업에 적합합니다.

### 절차
1. 새 프로젝트 폴더 생성 후 Git 초기화
   - `mkdir todo-app`
   - `cd todo-app`
   - `git init`
2. 프로젝트 폴더를 VS Code에서 엽니다.
3. 채팅 뷰(`Ctrl+Alt+I`)에서 Agents 드롭다운으로 `Agent` 선택
4. 채팅 입력에 다음 프롬프트 입력
   - `Create a simple todo app with HTML, CSS, and JavaScript. Include an input field to add todos, a list to display them, and a delete button for each item.`
5. 에이전트가 생성한 파일을 검토하고 `Keep` 또는 `Undo`로 변경 사항을 수락 또는 거부합니다.
6. 통합 브라우저에서 변경 사항을 미리보기
   - `workbench.browser.openLocalhostLinks` 설정을 구성
   - `index.html` 파일에서 Preview 버튼 클릭
7. 추가 프롬프트를 보내 앱을 확장합니다.
   - 예: `Mark todos as completed with a strikethrough effect.`

### 팁
- 미리보기 버튼이 보이지 않으면 Live Preview 확장 설치 여부를 확인합니다.
- 로컬 에이전트로 실시간 변경과 반복 개선을 수행할 수 있습니다.

## 2단계: Copilot CLI로 기능 계획 구현하기

### 목적
- Plan 에이전트로 기능 구현 계획을 만들고 Copilot CLI에 전달하여 배경에서 작업을 수행합니다.
- 직접 개입하지 않고도 작업을 분리하고 메인 워크스페이스 충돌을 줄일 수 있습니다.

### 절차
1. Source Control에서 현재 변경 사항 커밋하여 깔끔한 상태로 만듭니다.
2. 채팅 뷰에서 `New Chat (+) > New Chat`으로 새 로컬 에이전트 세션 시작
3. Agents 드롭다운에서 `Plan` 선택
4. 다음 프롬프트 입력
   - `Create a plan to add a dark/light theme toggle to the app. The toggle should switch between themes and persist the user's preference.`
5. Plan 에이전트가 질문할 경우 필요한 답변을 제공합니다.
6. `Start Implementation > Continue in Copilot CLI` 선택하여 계획을 Copilot CLI로 전달
7. Copilot CLI가 Git worktree를 생성하고 기능 구현을 시작합니다.
   - `Copy Changes`를 선택하여 현재 변경 사항을 Copilot CLI로 전파
8. Sessions 뷰에서 Copilot CLI 세션 진행 상태를 확인
9. 에이전트 작업이 완료되면 변경된 파일을 검토하거나 `View All Changes`로 전체 diff 확인
10. `Apply`를 선택하여 메인 워크스페이스에 변경 사항 적용

### 팁
- Copilot CLI가 백그라운드에서 실행되는 동안 메인 작업을 계속할 수 있습니다.
- 여러 Copilot CLI 세션을 동시에 실행하여 다양한 작업을 병렬로 수행할 수 있습니다.

## 3단계: 클라우드 에이전트로 기능 협업하기

### 목적
- Copilot 클라우드 에이전트를 사용하여 GitHub PR 기반 협업 워크플로를 체험합니다.
- 원격 인프라에서 작업하며 GitHub 리포지토리, PR, 이슈와 통합합니다.

### 절차
1. 프로젝트를 GitHub 리포지토리에 게시하고 원격 추가
   - `Publish to GitHub` 명령 실행
   - `Git: Add Remote`로 리포지토리 원격 추가
2. 채팅 뷰에서 `New Chat (+) > New Chat` 실행
3. 세션 타입 드롭다운에서 `Cloud` 선택
4. 다음 프롬프트 입력
   - `Redesign the todo app layout to improve user experience. Update colors, spacing, typography, and add animations to give it a modern look.`
5. 클라우드 에이전트가 새로운 세션을 시작하고 GitHub 브랜치 및 PR을 생성합니다.
6. Sessions 뷰 또는 PR 링크에서 진행 상황을 추적합니다.
7. GitHub Pull Requests 확장 설치 시 `Copilot on my Behalf` 보기에서 PR 상태를 확인할 수 있습니다.
8. 작업이 완료되면 PR이 검토를 위해 사용자에게 할당됩니다.
9. 세션을 마우스 오른쪽 버튼으로 클릭하거나 세션을 선택해 `Checkout` 또는 `Apply` 등 추가 옵션을 사용합니다.

### 팁
- 클라우드 에이전트는 즉시 피드백이 필요 없는 작업, 원격 실행, GitHub 협업에 적합합니다.

## 4단계: 다음 단계

- 에이전트 유형과 사용 시점을 더 알아보기: `https://code.visualstudio.com/docs/copilot/agents/overview`
- Plan 에이전트로 작업 계획 및 조사하기: `https://code.visualstudio.com/docs/copilot/agents/planning`
- 사용자 정의 에이전트 만들기 탐색: `https://code.visualstudio.com/docs/copilot/customization/custom-agents`

## 도움말 및 지원

- 커뮤니티에 질문
- 기능 요청 제출
- 이슈 보고
