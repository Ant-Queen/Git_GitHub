# VS Code 에이전트 스킬(Agent Skills)

## 개요
Agent Skills는 특정 작업을 수행하기 위한 재사용 가능한 기능 블록입니다. 지침, 스크립트, 예제 파일을 함께 묶어서 AI가 필요할 때 동적으로 불러올 수 있습니다.

Agent Skills는 다음에 적합합니다.

- 테스트, 디버깅, 배포 같은 반복 작업을 자동화할 때
- 작업 단계를 문서화하고 재사용 가능한 워크플로우로 만들 때
- 여러 AI 도구(VS Code, Copilot CLI, 클라우드 에이전트)에서 공유할 때

## Agent Skills와 Custom Instructions 차이

- Agent Skills: 작업 기반, 명시적 호출 또는 자동 적재, 스크립트/리소스를 포함
- Custom Instructions: 프로젝트 규칙, 자동 적용 지침, 주로 텍스트 지침

## 스킬 생성

### 스킬 디렉터리 위치

- 워크스페이스: `.github/skills/`, `.claude/skills/`, `.agents/skills/`
- 사용자 프로필: `~/.copilot/skills/`, `~/.claude/skills/`, `~/.agents/skills/`

`chat.agentSkillsLocations` 설정으로 경로를 추가할 수 있습니다.

### 스킬 파일 구조

스킬은 디렉터리 하나와 `SKILL.md` 파일로 구성됩니다.

```text
.github/skills/my-skill/
  SKILL.md
  script.sh
  examples/
```

### `SKILL.md` 형식

`SKILL.md`는 YAML frontmatter와 Markdown 본문으로 구성됩니다.

```markdown
---
name: skill-name
description: Description of what the skill does and when to use it
argument-hint: '[target] [options]'
user-invocable: true
disable-model-invocation: false
context: inline
---
# Skill Instructions

스킬 사용 방법과 예시를 작성합니다.
```

### 주요 frontmatter 필드

- `name`: 고유 식별자. 디렉터리 이름과 일치해야 하며 소문자, 숫자, 하이픈만 허용됩니다.
- `description`: 스킬이 수행하는 작업과 사용 사례를 설명합니다.
- `argument-hint`: `/` 명령어 사용 시 입력란 힌트로 표시됩니다.
- `user-invocable`: 슬래시 명령어 메뉴에 표시할지 여부.
- `disable-model-invocation`: AI가 자동으로 스킬을 불러오지 못하게 막을지 여부.
- `context`: `inline` 또는 `fork`. 큰 스킬을 별도 서브에이전트로 실행하려면 `fork`를 사용합니다.

### 스킬 본문 작성

- 스킬의 목표와 절차를 명확히 설명합니다.
- 예제, 명령어, 참고 파일 링크를 함께 제공합니다.
- 추가 파일을 참조할 때 상대 경로 Markdown 링크를 사용합니다.

## 스킬 사용

- 채팅 입력에서 `/`를 입력하면 스킬 목록이 표시됩니다.
- `/skill-name` 같은 명령어로 실행할 수 있습니다.
- 스킬 이름은 플러그인에서 자동 네임스페이스로 변환될 수 있습니다.

### 접근 제어

- 기본: `user-invocable`이 생략될 경우 스킬이 메뉴에 표시되고 AI가 자동 로드할 수 있습니다.
- `user-invocable: false`: 메뉴에는 표시되지 않지만 AI가 상황에 맞게 자동 로드합니다.
- `disable-model-invocation: true`: 명시적 호출만 허용됩니다.

## Forked Context (실험적)

`context: fork`를 설정하면 스킬이 별도 서브에이전트에서 실행됩니다. 이 경우 스킬의 중간 추론은 부모 대화에 남지 않고 최종 결과만 전달되어 메인 채팅 컨텍스트가 깨끗하게 유지됩니다.

사용 예시:

- 대규모 코드 리뷰
- 긴 조사 또는 분석 작업
- 메인 대화와 격리된 작업

> 이 기능은 실험적이며 `github.copilot.chat.skillTool.enabled` 설정이 필요합니다.

## 스킬 공유 및 확장

- `github/awesome-copilot`와 `anthropics/skills` 같은 커뮤니티 저장소에서 스킬을 가져올 수 있습니다.
- 플러그인에 포함된 스킬도 사용할 수 있습니다. 설치된 플러그인은 `Configure Skills` 메뉴에 나타납니다.

## 확장 기능으로 스킬 제공하기

VS Code 확장 프로그램은 `chatSkills` 기여 포인트를 사용해 스킬을 제공합니다.

```json
{
  "contributes": {
    "chatSkills": [
      {
        "path": "./skills/my-skill/SKILL.md"
      }
    ]
  }
}
```

확장 스킬도 일반 스킬과 동일한 형식을 따릅니다.

## Agent Skills 표준

Agent Skills는 오픈 표준으로, VS Code 외에도 GitHub Copilot CLI, Copilot cloud agent 등에서 호환 가능합니다.

## 팁

- 스킬을 작게 분리하여 재사용성을 높입니다.
- `description`을 구체적으로 작성하면 AI가 적절하게 로드할 확률이 높아집니다.
- 스크립트나 예제 파일을 함께 두면 스킬의 실용성이 커집니다.
- `context: fork`는 메인 대화에 영향을 주지 않는 작업에 유리합니다.
