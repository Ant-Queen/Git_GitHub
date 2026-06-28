# VS Code 커스텀 에이전트(Custom Agents)

## 개요
커스텀 에이전트는 특정 역할이나 작업을 수행하도록 AI를 구성하는 방법입니다. 각 에이전트는 도구 목록, 모델, 지침, 서브에이전트, 핸드오프를 고유하게 정의할 수 있습니다.

## 왜 커스텀 에이전트를 사용할까?

- 작업별 기능 제한: 예를 들어 계획 에이전트는 읽기 전용 도구만 사용하고, 구현 에이전트는 코드 편집 도구에 접근하도록 설정할 수 있습니다.
- 일관된 역할 정의: 보안 검토, 테스트 작성, 설계 문서 작성 등 특정 페르소나를 고정할 수 있습니다.
- 워크플로우 연계: 핸드오프 기능으로 에이전트 간 전환을 쉽게 지원합니다.

## 파일 위치

기본 경로는 다음과 같습니다.

- 워크스페이스: `.github/agents/` 폴더
- Claude 형식 워크스페이스: `.claude/agents/` 폴더
- 사용자 프로필: `~/.copilot/agents/` 또는 VS Code 사용자 데이터 경로

`chat.agentFilesLocations` 설정으로 추가 위치를 구성할 수 있습니다.

## 에이전트 파일 구조

커스텀 에이전트는 `.agent.md` 확장자를 가진 Markdown 파일입니다.

### 헤더(frontmatter)

선택적 YAML frontmatter로 아래 항목을 지정할 수 있습니다.

- `name`: 에이전트 이름(지정하지 않으면 파일 이름 사용)
- `description`: 입력란 플레이스홀더와 뷰에 표시될 설명
- `argument-hint`: 입력 힌트 텍스트
- `tools`: 사용할 수 있는 도구 또는 도구 세트 목록
- `agents`: 사용할 수 있는 서브에이전트 목록, `*` 또는 빈 배열 `[]` 사용 가능
- `model`: 사용할 모델 이름 또는 우선 순위 목록
- `user-invocable`: 에이전트 드롭다운에 표시 여부
- `disable-model-invocation`: 다른 에이전트가 서브에이전트로 호출할 수 있는지 여부
- `target`: 대상 환경(`vscode` 또는 `github-copilot`)
- `mcp-servers`: GitHub Copilot 대상 에이전트를 위한 MCP 서버 목록
- `handoffs`: 다음 에이전트로 전환하기 위한 버튼 목록
- `hooks`: 해당 에이전트가 활성화되었을 때만 실행되는 에이전트 범위 훅(Preview)

### 본문

에이전트 본문은 Markdown으로 작성하며, 해당 에이전트가 따라야 할 지침, 목표, 행동 방침을 설명합니다.

- `#tool:<tool-name>` 문법으로 도구를 참조할 수 있습니다.
- 다른 파일을 참조하려면 Markdown 링크를 사용합니다.

## 핸드오프(Handoffs)

핸드오프는 에이전트 간 순차적 워크플로우를 만듭니다. 예를 들어 계획 → 구현 → 리뷰처럼 다음 단계로 자연스럽게 전환할 수 있습니다.

```markdown
---
name: plan-agent
description: Generate an implementation plan
tools: ['search', 'web']
handoffs:
  - label: Start Implementation
    agent: implementation
    prompt: Now implement the plan outlined above.
    send: false
    model: GPT-5.2 (copilot)
---
```

- `label`: 버튼 텍스트
- `agent`: 전환 대상 에이전트
- `prompt`: 전환 시 사용할 기본 메시지
- `send`: true이면 전환 후 자동 제출
- `model`: 특정 모델을 지정할 수 있음

## 에이전트 구조 주요 필드

- `tools`: 에이전트에서 사용할 수 있는 도구 목록. MCP 서버 도구 전체를 포함하려면 `<server name>/*` 형식을 사용합니다.
- `agents`: 서브에이전트 목록. `*`는 모든 에이전트를 허용합니다.
- `model`: 모델 우선순위나 단일 모델 지정 가능.
- `user-invocable`: false면 드롭다운에 표시되지 않지만 서브에이전트로는 사용 가능.
- `disable-model-invocation`: true면 서브에이전트로도 사용 불가.
- `hooks`: 에이전트 범위 훅을 정의하면 이 에이전트가 활성화된 경우에만 실행됩니다.

## 커스텀 에이전트 생성

1. Agent Customizations editor에서 Agents 탭을 엽니다.
2. New Agent(Workspace) 또는 New Agent(User)를 선택합니다.
3. 파일 이름을 지정하고 `.agent.md` 파일을 작성합니다.
4. 필요한 지침, 도구, 모델을 헤더와 본문에 입력합니다.

AI로 생성하려면 `/create-agent`를 사용하여 원하는 역할을 설명하면 에이전트 템플릿을 만들어줍니다.

## 에이전트 관리

- Agents 드롭다운에서 에이전트를 선택하거나 숨길 수 있습니다.
- `chat.agentFilesLocations`로 검색 위치를 추가하거나 변경할 수 있습니다.
- 동일한 에이전트를 여러 워크스페이스에서 재사용하려면 사용자 프로필에 저장합니다.

## 툴 우선순위

Prompt 파일과 커스텀 에이전트 모두 `tools`를 지정할 수 있습니다. 실제 사용 가능한 도구 목록은 다음 순서로 결정됩니다.

1. 프롬프트 파일의 `tools`
2. 연결된 커스텀 에이전트의 `tools`
3. 선택된 에이전트의 기본 도구

## `AGENTS.md` 및 이전 파일

- `.chatmode.md` 등 이전 명칭을 사용하던 파일은 `.agent.md`로 이름을 바꿔야 합니다.
- Claude 형식의 `.md` 파일도 `.claude/agents`에 저장하면 VS Code가 인식합니다.

## 문제 해결

- 에이전트가 나타나지 않을 때: 파일 위치, `name` 필드, `user-invocable` 설정을 확인합니다.
- 도구가 보이지 않을 때: `tools` 목록에 올바른 도구 이름 또는 MCP 서버 경로가 있는지 확인합니다.
- 에이전트가 서브에이전트로 동작하지 않을 때: `disable-model-invocation` 설정을 확인합니다.

## 보안

커스텀 에이전트는 도구 접근을 제한함으로써 보안 제어에 유리합니다. 공유 저장소에 에이전트를 추가할 때는 사용 가능한 도구와 모델을 최소 권한으로 설정해야 합니다.
