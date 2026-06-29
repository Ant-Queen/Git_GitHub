# VS Code 에이전트 튜토리얼 정리

원문: https://code.visualstudio.com/docs/agents/agents-tutorial

---

## 1. 이 튜토리얼의 목표

이 문서는 VS Code에서 에이전트를 어떻게 쓰는지, 실제 예제를 통해 익히는 가이드입니다.

핵심은 다음 3가지입니다.

- 로컬 에이전트로 새 프로젝트를 빠르게 만들기
- Copilot CLI로 백그라운드 작업 처리하기
- 클라우드 에이전트로 GitHub 기반 협업하기

즉, 에이전트를 단순히 질문하는 도구가 아니라, 개발 흐름 전체를 도와주는 도구로 이해하면 됩니다.

---

## 2. 먼저 준비할 것

이 튜토리얼을 따라하려면 아래가 필요합니다.

- Visual Studio Code 설치
- VS Code에서 AI 기능 활성화
- GitHub 계정

특히 클라우드 에이전트 단계는 GitHub 저장소가 필요합니다.

> 참고: 조직 정책에 따라 에이전트 기능이 꺼져 있을 수 있습니다. 그 경우 관리자에게 확인해야 합니다.

---

## 3. Step 1: 로컬 에이전트로 앱 만들기

### 목표

로컬 에이전트를 사용해 간단한 Todo 앱을 처음부터 생성합니다.

### 진행 방식

1. 새 프로젝트 폴더를 만듭니다.
2. Git 저장소로 초기화합니다.
3. VS Code에서 폴더를 열고, Chat view를 엽니다.
4. 에이전트 드롭다운에서 Agent를 선택합니다.
5. 다음처럼 요청합니다.

```text
Create a simple todo app with HTML, CSS, and JavaScript. Include an input field to add todos, a list to display them, and a delete button for each item.
```

### 이 단계에서 중요한 포인트

- 에이전트가 여러 파일을 자동으로 생성합니다.
- 변경사항은 Keep 또는 Undo로 승인/취소할 수 있습니다.
- 생성된 앱은 Preview를 통해 바로 확인할 수 있습니다.

### 예시 확장 요청

```text
Mark todos as completed with a strikethrough effect.
```

이렇게 하면 에이전트가 앱을 계속 개선해줍니다.

### 핵심 요약

로컬 에이전트는 "빠르게 실험하고 바로 확인하고 싶을 때" 아주 유용합니다.

---

## 4. Step 2: Copilot CLI로 기능 계획 구현하기

### 목표

계획형 에이전트로 구현 계획을 세우고, 그다음 Copilot CLI가 백그라운드에서 작업을 처리하게 합니다.

### 진행 방식

1. 현재 작업 기준을 깔끔하게 유지하기 위해 변경사항을 커밋합니다.
2. 새 채팅 세션을 시작합니다.
3. 에이전트 드롭다운에서 Plan을 선택합니다.
4. 다음처럼 요청합니다.

```text
Create a plan to add a dark/light theme toggle to the app. The toggle should switch between themes and persist the user's preference.
```

5. 에이전트가 계획을 제안하면, 필요하면 질문에 답합니다.
6. Start Implementation를 선택해 Copilot CLI로 넘깁니다.

### 이 단계에서 중요한 포인트

- Copilot CLI는 백그라운드에서 작업합니다.
- 작업 중에도 메인 워크스페이스를 계속 사용할 수 있습니다.
- 작업이 끝나면 변경사항을 리뷰하고 Apply할 수 있습니다.

### 핵심 요약

이 단계는 "즉시 상호작용이 필요 없는 작업을 위임할 때" 적합합니다.

---

## 5. Step 3: 클라우드 에이전트로 GitHub 협업하기

### 목표

클라우드 에이전트를 사용해 GitHub 기반으로 기능을 구현하고, PR(풀 리퀘스트)로 협업합니다.

### 진행 방식

1. 프로젝트를 GitHub 저장소로 게시합니다.
2. 저장소를 원격 저장소로 추가합니다.
3. 새 채팅 세션을 열고, 세션 타입을 Cloud로 변경합니다.
4. 다음처럼 요청합니다.

```text
Redesign the todo app layout to improve user experience. Update colors, spacing, typography, and add animations to give it a modern look.
```

5. 클라우드 에이전트가 브랜치와 PR을 자동으로 생성합니다.
6. 세션을 통해 진행 상황을 확인하고, 리뷰할 수 있습니다.

### 핵심 요약

클라우드 에이전트는 "원격 자원과 GitHub 협업이 필요한 작업"에 잘 맞습니다.

---

## 6. 이 튜토리얼에서 배우는 핵심

이 튜토리얼을 통해 알 수 있는 핵심은 다음입니다.

- 로컬 에이전트: 즉각적인 피드백과 빠른 구현에 강함
- Plan + Copilot CLI: 백그라운드 작업 위임에 강함
- 클라우드 에이전트: GitHub 협업과 원격 실행에 강함

즉, 상황에 따라 적절한 에이전트 유형을 선택하면 개발 생산성을 높일 수 있습니다.

---

## 7. 다음으로 공부하면 좋은 주제

- 에이전트 개요
- 에이전트 유형과 선택 기준
- 계획형 에이전트 사용법
- 커스텀 에이전트 만들기
