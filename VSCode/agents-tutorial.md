 
# VS Code 에이전트 튜토리얼 (한글 정리)

> 원문: https://code.visualstudio.com/docs/agents/agents-tutorial

## 개요
이 튜토리얼은 VS Code에서 제공하는 다양한 에이전트(로컬 에이전트, Plan/백그라운드 에이전트(Copilot CLI), 클라우드 에이전트)를 사용해 간단한 todo 앱을 만들고 확장하는 전체 흐름을 안내합니다. 각 에이전트는 목적과 상호작용 방식이 다르므로 상황에 맞게 활용합니다.

---

## 사전 준비
- `Visual Studio Code` 설치
- VS Code에서 AI 기능(에이전트) 활성화
- (클라우드 워크플로우 사용 시) `GitHub` 계정 및 리포지토리

팁: 에이전트 관련 설정은 조직 정책에 의해 제한될 수 있습니다. `chat.agent.enabled` 등이 비활성화되어 있으면 관리자에게 문의하세요.

---

## 단계별 가이드

### 1단계 — 로컬 에이전트로 앱 골격 만들기
로컬 에이전트는 즉시 상호작용하며 피드백을 받을 수 있는 작업에 적합합니다(예: 프로젝트 초기 스캐폴딩, 반복적 코드 생성).

1. 새 프로젝트 폴더 생성 및 Git 초기화

```bash
mkdir todo-app
cd todo-app
git init
```

2. VS Code에서 폴더를 엽니다.
3. Chat 보기(단축: `Ctrl+Alt+I`)를 열고 Agents 드롭다운에서 `Agent` 선택
4. 채팅 입력창에 스캐폴드 요청 입력 예시:

```text
Create a simple todo app with HTML, CSS, and JavaScript. Include an input field to add todos, a list to display them, and a delete button for each item.
```

5. 에이전트가 생성하는 파일을 검토하고 `Keep` 또는 `Undo`로 변경 수락/거부
6. `index.html`을 열어 우측 상단의 Preview 버튼으로 통합 브라우저에서 확인
7. 추가 프롬프트로 기능 확장(예: 완료 표시, 스타일링, 접근성 개선)

팁: 로컬 에이전트는 코드를 즉시 생성·반영하므로 빠른 반복 작업에 유용합니다.

---

### 2단계 — Plan 에이전트와 Copilot CLI로 구현 위임
Plan 에이전트는 기능을 설계·분해하고 Copilot CLI 같은 백그라운드 도구에 실제 구현을 위임할 때 사용합니다. Copilot CLI는 `git worktree`를 활용해 변경을 격리하고 백그라운드에서 작업합니다。

1. 현재 변경사항을 커밋하여 작업 상태를 정리합니다。
2. Chat 보기에서 새 채팅을 열고 Agents 드롭다운에서 `Plan` 선택
3. Plan 에이전트에 보낼 예시 프롬프트:

```text
Create a plan to add a dark/light theme toggle to the app. The toggle should switch between themes and persist the user's preference.
```

4. 계획을 다듬은 후 `Start Implementation > Continue in Copilot CLI`를 선택하여 구현을 Copilot CLI에 위임
5. Copilot CLI는 별도의 Git worktree에서 변경을 수행합니다。 필요하면 `Copy Changes`로 현재 변경사항을 복사합니다。
6. Sessions 뷰에서 진행 상황을 모니터링하고, 구현이 끝나면 변경 파일을 검토
7. Chat 보기에서 `Apply`를 눌러 변경을 메인 워크스페이스에 적용

팁: Copilot CLI가 백그라운드에서 작업하는 동안 로컬에서 다른 작업을 계속할 수 있습니다。

---

### 3단계 — 클라우드 에이전트로 협업 및 PR 생성
클라우드 에이전트(Copilot cloud agent)는 원격에서 실행되며, GitHub PR 기반의 협업 워크플로우에 적합합니다。

1. 프로젝트를 GitHub에 게시하고 원격 리포지토리를 설정합니다。
   - Command Palette에서 `Publish to GitHub` 명령 실행
   - 또는 `Git: Add Remote`로 원격을 추가
2. Chat 보기에서 새 세션을 만들고 세션 타입에서 `Cloud` 선택
3. 클라우드 에이전트에 보낼 예시 프롬프트:

```text
Redesign the todo app layout to improve user experience. Update colors, spacing, typography, and add animations to give it a modern look.
```

4. 클라우드 에이전트는 브랜치와 Pull Request를 생성합니다。
5. Sessions 뷰 또는 PR 링크에서 변경사항과 리뷰를 추적
6. 에이전트가 생성한 PR을 검토하고, 필요 시 체크아웃 후 적용

팁: `GitHub Pull Requests` 확장과 함께 사용하면 PR 추적이 더 편리합니다。

---

## 예시 프롬프트 모음
- 스캐폴딩: "Create a simple todo app with HTML, CSS, and JavaScript..."
- 계획(Plan): "Create a plan to add a dark/light theme toggle..."
- 리디자인(Cloud): "Redesign the todo app layout to improve user experience..."

---

## 다음 단계 및 추가 리소스
- 에이전트 유형과 사용 사례: https://code.visualstudio.com/docs/agents/overview
- Plan 및 조사: https://code.visualstudio.com/docs/agents/planning
- 커스텀 에이전트 가이드: https://code.visualstudio.com/docs/agent-customization/custom-agents

---

## 도움말 및 지원
- 페이지 하단의 'Ask the community' 링크 또는 GitHub 이슈로 피드백 제출

---

## 주의사항
- 조직 정책으로 인해 에이전트 기능이 제한될 수 있습니다. 관리자에게 확인하세요。
- Copilot 구독 및 정책은 변경될 수 있으니 공식 문서를 확인하세요。

---

작성일: 2026-06-15

