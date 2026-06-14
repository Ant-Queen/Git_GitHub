# VS Code 에이전트 튜토리얼

이 튜토리얼은 VS Code에서 여러 에이전트 유형을 사용하여 todo 앱을 만들고 기능을 확장하며 협업까지 진행하는 과정을 안내합니다.

## 1. 전제 조건

튜토리얼을 완료하려면 다음이 필요합니다.

- 컴퓨터에 Visual Studio Code가 설치되어 있어야 함
- Live Preview 확장 설치 (todo 앱 미리보기를 위해)
- GitHub 계정
- GitHub Copilot 구독

## 2. 단계 1: 로컬 에이전트로 앱 스캐폴딩

로컬 에이전트는 즉각적인 피드백과 결과가 필요한 대화형 작업에 적합합니다.

1. 새 프로젝트 폴더를 만들고 Git 버전 관리를 초기화합니다.
   - `mkdir todo-app`
   - `cd todo-app`
   - `git init`
2. 프로젝트 폴더를 VS Code에서 엽니다.
3. 채팅 보기에서 `Agent`를 선택합니다.
   - `Ctrl+Alt+I`로 채팅 뷰 열기
   - 에이전트 옵션이 보이지 않으면 `chat.agent.enabled` 설정을 확인
4. 다음 프롬프트를 입력하여 todo 앱 구조를 생성합니다.
   - `Create a simple todo app with HTML, CSS, and JavaScript. Include an input field to add todos, a list to display them, and a delete button for each item.`
5. 에이전트가 생성하는 파일을 검토하고 `Keep` 또는 `Undo`로 변경 사항을 수락하거나 취소합니다.
6. 통합 브라우저에서 변경 사항을 미리보기 합니다.
   - `index.html`을 열고 `Preview` 버튼 클릭
   - Live Preview 확장 설치 필요
7. 추가 프롬프트를 보내 앱을 개선합니다.
   - 예: `Mark todos as completed with a strikethrough effect.`

이 과정을 통해 로컬 에이전트를 사용해 실시간으로 코드를 생성하고 반복할 수 있습니다.

## 3. 단계 2: Copilot CLI로 기능 계획 구현

이 단계에서는 `Plan` 에이전트를 사용해 기능 구현 계획을 세운 뒤 Copilot CLI에 넘겨 백그라운드에서 실행합니다.

1. 변경 사항을 커밋하여 깔끔한 상태로 만듭니다.
2. 채팅 보기에서 새 채팅을 시작합니다.
3. 에이전트 드롭다운에서 `Plan`을 선택한 뒤 다음 프롬프트를 입력합니다.
   - `Create a plan to add a dark/light theme toggle to the app. The toggle should switch between themes and persist the user's preference.`
4. `Plan` 에이전트가 계획을 다듬기 위해 추가 질문을 할 수 있습니다.
5. 준비되면 `Start Implementation > Continue in Copilot CLI`를 선택하여 Copilot CLI로 계획을 넘깁니다.
6. Copilot CLI가 Git worktree를 생성하고 기능 구현을 시작합니다.
   - 변경 사항을 사용하려면 `Copy Changes` 선택
7. 세션 뷰에서 Copilot CLI 진행 상황을 확인합니다.
8. 완료되면 변경된 파일을 검토하거나 `View All Changes`로 다중 파일 diff를 확인합니다.
9. `Apply`를 선택하여 변경 사항을 메인 작업 영역에 적용합니다.

Copilot CLI는 백그라운드에서 독립적으로 작업하므로 메인 워크스페이스를 방해하지 않고 여러 작업을 동시에 진행할 수 있습니다.

## 4. 단계 3: 클라우드 에이전트로 기능 협업

이 단계에서는 클라우드 에이전트를 사용해 앱 레이아웃을 재설계하고 GitHub 풀 리퀘스트 협업을 진행합니다.

1. 프로젝트를 GitHub 리포지토리에 게시하고 원격을 추가합니다.
   - Command Palette에서 `Publish to GitHub` 실행
   - `Git: Add Remote` 실행
2. 새 채팅을 시작합니다.
3. 세션 유형 드롭다운에서 `Cloud`를 선택하고 다음 프롬프트를 입력합니다.
   - `Redesign the todo app layout to improve user experience. Update colors, spacing, typography, and add animations to give it a modern look.`
4. 클라우드 에이전트가 새 세션을 시작하고 브랜치 및 PR을 생성합니다.
5. 세션 뷰에서 진행 상황을 확인하거나 PR 링크를 클릭합니다.
6. GitHub Pull Requests 확장 설치 시 `Copilot on my Behalf` 뷰에서도 PR 상태를 볼 수 있습니다.
7. 완료되면 클라우드 에이전트가 PR을 사용자에게 할당합니다.
8. 세션 뷰에서 세션을 마우스 오른쪽 클릭하여 추가 옵션을 확인하거나 `Checkout` 또는 `Apply`를 선택합니다.

클라우드 에이전트는 원격 리소스를 활용하고 GitHub 풀 리퀘스트를 통해 협업할 수 있도록 지원합니다.

## 5.  이후 단계

계속해서 에이전트를 더 깊이 활용하려면 다음 내용을 확인하세요.

- 에이전트 유형과 사용 시기
- `Plan` 에이전트로 계획 및 조사 작업 수행
- 커스텀 에이전트 생성

---

> 이 문서는 VS Code 공식 `Agents tutorial` 페이지를 기반으로 한국어로 요약 정리한 내용입니다.
