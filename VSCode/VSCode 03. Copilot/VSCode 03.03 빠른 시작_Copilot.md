# VS Code Copilot 시작하기 정리

## 개요

GitHub Copilot은 VS Code에서 AI 기반 코딩 경험을 제공합니다. 이 튜토리얼에서는 작업 관리 웹 앱을 만들면서 Copilot의 주요 기능을 실습합니다.

## 사전 요구 사항

- VS Code가 설치되어 있어야 합니다.
- GitHub Copilot에 접근할 수 있어야 합니다.
- Copilot 구독이 없으면 VS Code 내에서 무료로 가입할 수 있으며, 월별 인라인 제안 및 AI 크레딧을 받습니다.

> 2026년 4월 20일부터 Copilot Pro, Pro+, Max, Student 플랜 신규 가입이 일시 중지될 수 있습니다.

## 1단계: 인라인 제안 체험하기

1. 새 폴더를 만들고 VS Code에서 엽니다.
2. `index.html` 파일을 만듭니다.
3. HTML을 입력하기 시작하면 Copilot이 인라인 제안을 제공합니다.
4. `Tab`을 눌러 제안을 수락합니다.
5. `<body>` 태그 안에 콘텐츠를 계속 작성하면 Copilot이 관련 HTML 요소를 계속 제안합니다.
6. 여러 제안이 보이면 `Alt+]`, `Alt+[`, 또는 고스트 텍스트 위로 마우스를 올려 탐색할 수 있습니다.

- 인라인 제안은 자동으로 작동하며, 보일러플레이트 코드나 반복적인 패턴 작성에 특히 유용합니다.

## 2단계: 에이전트로 완성된 기능 만들기

1. `Ctrl+Alt+I`를 눌러 Chat 뷰를 엽니다.
2. 에이전트 드롭다운에서 `Agent`를 선택합니다.
3. 다음 프롬프트를 입력하고 Enter를 누릅니다.

```text
Create a complete task manager web application with the ability to add, delete, and mark tasks as completed. Include modern CSS styling and make it responsive. Use semantic HTML and ensure it's accessible. Separate markup, styles, and scripts into their own files.
```

4. 에이전트가 `index.html`, `styles.css`, `script.js` 등의 파일을 생성하고 코드를 작성합니다.
5. 생성된 파일을 검토한 후 `Keep`를 선택하여 변경 내용을 적용합니다.
6. `index.html` 파일을 통합 브라우저에서 열어 미리보기를 확인합니다.
7. 추가 기능을 요청하려면 다음과 같이 입력합니다.

```text
Add a filter system with buttons to show all tasks, only completed tasks, or only pending tasks. Update the styling to match the existing design.
```

- 에이전트는 여러 파일에 걸친 변경을 조정하여 기능을 완성합니다.
- 모델별로 결과가 다를 수 있으므로 모델 드롭다운에서 다른 모델을 선택해 볼 수 있습니다.

## 3단계: 인라인 채팅으로 정밀 수정하기

1. JavaScript 파일을 열고 새로운 작업을 추가하는 코드를 찾습니다.
2. 해당 코드 블록을 선택하고 `Ctrl+I`를 눌러 에디터 인라인 채팅을 엽니다.
3. 다음 프롬프트를 입력합니다.

```text
Add input validation to prevent adding empty tasks and trim whitespace from task text.
```

4. 변경 내용을 검토하고 `Keep`를 선택하여 적용합니다.

- 에디터 인라인 채팅은 특정 코드 블록에 대해 작은 수정, 버그 수정, 리팩터링, 예외 처리 등의 정밀 작업에 적합합니다.

## 4단계: AI 경험 개인화하기

### 커스텀 인스트럭션 만들기

1. 프로젝트 루트에 `.github` 폴더를 만듭니다.
2. `.github/copilot-instructions.md` 파일을 생성합니다.
3. 다음과 같은 내용을 추가합니다.

```markdown
# Project general coding guidelines

## Code Style
- Use semantic HTML5 elements (header, main, section, article, etc.)
- Prefer modern JavaScript (ES6+) features like const/let, arrow functions, and template literals

## Naming Conventions
- Use PascalCase for component names, interfaces, and type aliases
- Use camelCase for variables, functions, and methods
- Prefix private class members with underscore (_)
- Use ALL_CAPS for constants

## Code Quality
- Use meaningful variable and function names that clearly describe their purpose
- Include helpful comments for complex logic
- Add error handling for user inputs and API calls
```

4. 파일을 저장하면 해당 프로젝트의 모든 채팅 상호작용에 지침이 적용됩니다.
5. 다음 프롬프트로 테스트합니다.

```text
Add a dark mode toggle button to the task manager.
```

- `/init` 명령은 프로젝트 구조와 코딩 패턴을 분석하여 커스텀 인스트럭션을 자동 생성합니다.

### 코드 리뷰용 커스텀 에이전트 만들기

1. 명령 팔레트에서 `Chat: New Custom Agent`를 실행합니다.
2. `.github/agents` 폴더를 선택합니다.
3. 이름을 `Reviewer`로 지정합니다.
4. `Reviewer.agent.md` 파일 내용을 다음과 같이 작성합니다.

```markdown
---
name: 'Reviewer'
description: 'Review code for quality and adherence to best practices.'
...
tools: ['vscode/askQuestions', 'vscode/vscodeAPI', 'read', 'agent', 'search', 'web']
---
# Code Reviewer agent

You are an experienced senior developer conducting a thorough code review. Your role is to review the code for quality, best practices, and adherence to [project standards](../copilot-instructions.md) without making direct code changes.

When reviewing code, structure your feedback with clear headings and specific examples from the code being reviewed.

## Analysis Focus
- Analyze code quality, structure, and best practices
- Identify potential bugs, security issues, or performance problems
- Evaluate accessibility and user experience considerations

## Important Guidelines
- Ask clarifying questions about design decisions when appropriate
- Focus on explaining what should be changed and why
- DO NOT write or suggest specific code changes directly
```

5. 저장 후 Chat 뷰에서 `Reviewer` 에이전트를 선택하여 사용합니다.
6. 다음과 같이 입력하여 테스트합니다.

```text
Review my full project
```

- 커스텀 에이전트는 특정 역할에 맞춘 분석이나 리뷰를 수행합니다.

## 5단계: 스마트 액션 사용하기

1. `Ctrl+Shift+G`로 소스 제어 뷰를 엽니다.
2. Git 저장소가 없으면 `Initialize Repository`를 선택합니다.
3. 변경 파일을 스테이징합니다.
4. 스파클 아이콘을 선택하여 커밋 메시지를 생성합니다.

- AI는 변경 내용, 수정 유형, 범위 등을 분석하여 표현력 있는 커밋 메시지를 만듭니다.
- 필요하면 다른 스타일의 메시지를 다시 생성할 수 있습니다.

- 스마트 액션은 디버깅, 테스트 등 다른 워크플로에서도 유용하게 통합됩니다.

## 다음 단계

- Copilot Quickstart: `https://code.visualstudio.com/docs/copilot/getting-started`
- Agents tutorial: `https://code.visualstudio.com/docs/copilot/agents/agents-tutorial`
- AI 개인화: `https://code.visualstudio.com/docs/copilot/customization/overview`
- MCP 도구: `https://code.visualstudio.com/docs/copilot/customization/mcp-servers`
