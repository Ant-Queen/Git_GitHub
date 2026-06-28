# VS Code 프롬프트 파일(Prompt Files)

## 개요
프롬프트 파일은 자주 사용하는 작업을 `/` 명령어로 실행할 수 있는 재사용 가능한 Markdown 파일입니다. 각 프롬프트 파일은 작업 지침, 도구 목록, 모델 설정 등을 포함할 수 있습니다.

## 위치
- 워크스페이스: `.github/prompts/` 폴더
- 사용자 프로필: VS Code 사용자 데이터의 prompt 파일 폴더

`chat.promptFilesLocations` 설정으로 추가 경로를 구성할 수 있습니다.

## 파일 형식
프롬프트 파일은 `.prompt.md` 확장자를 사용하며, 선택적 YAML frontmatter와 본문을 가집니다.

```markdown
---
name: create-react-form
description: Generate a React form component
argument-hint: '[formName]'
agent: ask
model: GPT-5 (copilot)
tools: ['browser', 'search']
---

# Create a React form component

Generate a React component for a form named `${input:formName}`.
```

### 주요 frontmatter 필드
- `description`: 프롬프트 설명
- `name`: `/` 명령어로 사용할 이름
- `argument-hint`: 입력 힌트
- `agent`: 실행할 에이전트(ask, agent, plan, 또는 커스텀 에이전트)
- `model`: 사용할 모델
- `tools`: 사용할 도구 목록

> `tools`에 지정된 도구가 실제로 없으면 VS Code가 무시합니다.

## 프롬프트 파일 생성

1. Agent Customizations editor에서 Prompts 탭 열기
2. New Prompt(Workspace) 또는 New Prompt(User) 선택
3. 파일 이름과 내용을 작성

또는 명령 팔레트에서 `Chat: New Prompt File`을 실행합니다.

### AI로 생성
- `/create-prompt` 명령어로 원하는 작업을 설명하면 VS Code가 프롬프트 파일을 자동 생성해줍니다.
- 진행 중 대화를 재사용하여 프롬프트로 저장할 수도 있습니다.

## 사용 방법

- 채팅 입력에 `/`를 입력하고 프롬프트 이름을 선택
- `/create-react-form formName=MyForm`처럼 인수를 추가
- 명령 팔레트에서 `Chat: Run Prompt` 실행
- 편집기에서 프롬프트 파일을 열고 재생 버튼 클릭

### 도구 목록 우선순위
1. 프롬프트 파일의 `tools`
2. 참조된 커스텀 에이전트의 `tools`
3. 현재 선택된 에이전트의 기본 도구

## 팁
- 명확한 기대 출력 형식을 설명합니다.
- 예시 입력/출력을 포함합니다.
- `${selection}`, `${input:variableName}` 등의 변수를 활용합니다.
- 다른 지침 파일을 참조해 중복을 줄입니다.

## 동기화
- Settings Sync를 통해 사용자 prompt 파일을 여러 장치에서 동기화할 수 있습니다.

## 문제 해결
- 프롬프트가 보이지 않으면 파일 위치와 `chat.promptFilesLocations`를 확인
- 프롬프트 파일 출처는 `Configure Prompt Files`에서 확인 가능

## 요약
프롬프트 파일은 반복되는 작업을 손쉽게 실행 가능한 커맨드형 프롬프트로 변환하는 도구입니다. 명확한 구조와 적절한 변수 사용으로 워크플로우를 크게 단순화할 수 있습니다.
