# VS Code 맞춤형 지침(Custom Instructions)

## 개요
Custom Instructions는 VS Code의 AI에게 프로젝트 특화 규칙, 스타일, 아키텍처 요구사항을 지속적으로 알려주는 방법입니다. 채팅 요청마다 자동으로 포함되어 AI 결과가 일관되도록 합니다.

## 지침 파일 유형

### 1. 항상 적용되는 지침

- `.github/copilot-instructions.md`: 워크스페이스 전체에 자동 적용됩니다.
- `AGENTS.md`: 여러 AI 에이전트를 사용하는 프로젝트에서 공통 지침을 적용할 때 유용합니다.
- 조직 수준 지침: GitHub 조직 전반에 걸쳐 공유할 수 있습니다.
- `CLAUDE.md`: Claude Code 호환성을 위한 파일입니다.

### 2. 파일 기반 지침

- `*.instructions.md`: 특정 파일 유형이나 폴더에만 적용할 수 있는 지침입니다.
- `applyTo` 속성에 glob 패턴을 지정하여 자동 적용 대상을 설정합니다.
- 파일 작업이나 언어별 요구사항을 구체적으로 정의할 때 적합합니다.

## 지침 파일 위치

기본 검색 위치는 다음과 같습니다.

- 워크스페이스: `.github/instructions` 폴더
- Claude 형식 워크스페이스: `.claude/rules` 폴더
- 사용자 프로필: `~/.copilot/instructions`, `~/.claude/rules`, 또는 사용자 데이터 위치

`chat.instructionsFilesLocations` 설정으로 추가 경로를 정의하거나 특정 위치를 비활성화할 수 있습니다.

## `.github/copilot-instructions.md` 사용법

워크스페이스 루트에 `.github/copilot-instructions.md` 파일을 두면 해당 프로젝트의 모든 채팅 요청에 지침이 자동 포함됩니다. 일반적으로 다음과 같은 내용을 담습니다.

- 프로젝트 스타일 규칙
- 선호 라이브러리
- 보안 정책
- 코드 작성 방침

## `.instructions.md` 파일 형식

`*.instructions.md` 파일은 선택적 YAML frontmatter와 Markdown 본문으로 구성됩니다.

예시:

```markdown
---
name: 'Python Standards'
description: 'Python 파일에 적용되는 스타일 규칙'
applyTo: '**/*.py'
---
# Python coding standards
- Follow PEP 8.
- Use type hints for public functions.
- Write docstrings for public functions.
```

### frontmatter 주요 항목

- `name`: 파일 이름 대신 UI에 표시되는 이름
- `description`: 툴팁에 보이는 설명
- `applyTo`: 자동 적용 대상 glob 패턴

## `AGENTS.md`와 `CLAUDE.md`

- `AGENTS.md`: 워크스페이스 루트 또는 하위 폴더에 두어 복수 에이전트에 공통 지침을 제공합니다.
- `CLAUDE.md`: Claude 기반 도구와의 호환성을 위해 사용하며, VS Code에서도 자동 인식합니다.
- `chat.useAgentsMdFile`, `chat.useClaudeMdFile` 설정으로 사용을 켜거나 끌 수 있습니다.

## 설정 기반 지침

VS Code는 아래 설정을 통해 지침 적용 방식을 제어합니다.

- `chat.instructionsFilesLocations`: 지침 파일 검색 위치 구성
- `chat.includeApplyingInstructions`: glob 패턴 기반 지침 적용 여부
- `chat.includeReferencedInstructions`: markdown 링크 참조 지침 포함 여부
- `chat.useAgentsMdFile`: `AGENTS.md` 사용 여부
- `chat.useClaudeMdFile`: `CLAUDE.md` 사용 여부

> 참고: 설정 기반 지침은 점차 deprecated 될 수 있으므로, 파일 기반 지침 사용을 권장합니다.

## 지침 우선순위

여러 소스에서 지침이 존재할 때 VS Code는 모두 제공하지만 충돌이 발생할 경우 다음 우선순위를 따릅니다.

1. 사용자 수준 개인 지침
2. 리포지토리 수준 지침 (`.github/copilot-instructions.md`, `AGENTS.md`)
3. 조직 수준 지침

## 효과적인 지침 작성 팁

- 간결하고 구체적으로 작성합니다.
- 추상적인 규칙보다 예시를 함께 제공합니다.
- 규칙의 이유를 포함하면 AI가 더 일관되게 적용합니다.
- 여러 규칙이 필요한 경우 여러 항목으로 나눕니다.
- `.instructions.md` 파일을 사용해 언어·프레임워크별 규칙을 분리합니다.

## 문제 해결

- 지침이 적용되지 않을 때는 파일 위치와 `applyTo` 패턴을 먼저 확인합니다.
- `.github/copilot-instructions.md`는 루트의 `.github` 폴더에 있어야 합니다.
- `*.instructions.md` 파일은 `chat.instructionsFilesLocations`에서 검색 가능한 위치에 있어야 합니다.
- AI 응답의 참조 섹션에서 어떤 지침이 사용됐는지 확인합니다.

## 동기화 및 공유

- `Settings Sync`를 사용하면 개인 지침과 prompt 파일을 여러 장치에서 동기화할 수 있습니다.
- 조직 수준 지침은 GitHub 조직 설정을 통해 공유할 수 있습니다.
