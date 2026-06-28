# VS Code 커스텀 지시사항 (Custom Instructions)

## 개요

커스텀 지시사항은 모든 채팅 요청에 자동으로 영향을 미치는 프로젝트 전체의 코딩 가이드라인 및 규칙을 정의합니다. 매번 채팅에서 수동으로 문맥을 포함시킬 필요 없이, 마크다운 파일에서 커스텀 지시사항을 설정하여 일관된 AI 응답을 보장합니다.

## 커스텀 지시사항의 두 가지 타입

### 1. 항상 적용되는 지시사항 (Always-on Instructions)

모든 채팅 요청에 자동으로 포함됩니다.

| 파일 | 용도 | 위치 |
|------|------|------|
| `.github/copilot-instructions.md` | 프로젝트 전체에 적용 | 워크스페이스 루트 |
| `AGENTS.md` | 여러 AI 에이전트에 적용 | 워크스페이스 루트 또는 서브폴더 |
| `CLAUDE.md` | Claude Code 호환성 | 워크스페이스 루트, `.claude` 폴더, 또는 홈 디렉토리 |
| 조직 레벨 지시사항 | 조직 전체 공유 | GitHub 조직 레벨 |

### 2. 파일 기반 지시사항 (File-based Instructions)

에이전트가 작업하는 파일이 특정 패턴과 일치할 때 조건부로 적용됩니다.

**파일 위치:**
- 워크스페이스: `.github/instructions` 폴더
- 사용자 프로필: `~/.copilot/instructions` 폴더

**예시 구조:**
```
.github/instructions/
  frontend/
    react.instructions.md
    accessibility.instructions.md
  backend/
    api-design.instructions.md
  testing/
    unit-tests.instructions.md
```

## `.github/copilot-instructions.md` 파일 사용

### 작성 가이드

프로젝트 전체에 적용되는 사항들을 작성하세요:
- 코딩 스타일 및 네이밍 규칙
- 기술 스택 선언 및 선호 라이브러리
- 따를 아키텍처 패턴
- 보안 요구사항 및 오류 처리 방식
- 문서 작성 표준

### 생성 방법

1. 워크스페이스 루트에 `.github` 디렉토리 생성
2. 그 안에 `copilot-instructions.md` 파일 생성
3. 마크다운 형식으로 지시사항 작성

### 예시

```markdown
# 프로젝트 코딩 가이드

## 코딩 스타일
- 타입스크립트 사용 (타입 힌트 필수)
- Prettier 사용 (라인 길이: 100)
- ESLint 권장 설정 준수

## 네이밍 규칙
- 변수: camelCase
- 상수: UPPER_SNAKE_CASE
- 클래스: PascalCase
- 컴포넌트: PascalCase

## 아키텍처 패턴
- 모듈식 구조 선호
- 강력한 타입 정의
- 에러 처리 필수
```

## `.instructions.md` 파일 사용

### 파일 포맷

YAML 프론트매터와 마크다운 본문으로 구성됩니다.

**YAML 필드:**
| 필드 | 필수 | 설명 |
|------|------|------|
| name | 선택 | UI에 표시되는 이름 (기본값: 파일명) |
| description | 선택 | 호버 시 표시되는 설명 |
| applyTo | 선택 | 글로브 패턴 (예: `**/*.py`) |

### 생성 방법

1. 챗 뷰에서 설정(기어) 아이콘 선택
2. 에이전트 커스터마이징 에디터 열기
3. 지시사항 탭에서 `New Instructions` 선택
4. 워크스페이스 또는 사용자 레벨 선택

또는 `/instructions` 명령으로 빠르게 메뉴 열기

### 예시

```markdown
---
name: 'Python 표준'
description: 'Python 파일의 코딩 규칙'
applyTo: '**/*.py'
---

# Python 코딩 표준

- PEP 8 스타일 가이드 준수
- 모든 함수 서명에 타입 힌트 사용
- 공개 함수에 docstring 작성
- 들여쓰기: 4 스페이스 사용
```

## `AGENTS.md` 파일 사용

### 특징

- VS Code에서 자동 감지됨
- 모든 채팅 요청에 적용됨
- 여러 AI 에이전트에서 인식 가능
- 모노레포의 서브폴더에 여러 파일 배치 가능 (실험적)

### 생성 방법

1. 워크스페이스 루트에 `AGENTS.md` 파일 생성
2. 설정에서 `chat.useAgentsMdFile: true` 확인

## `CLAUDE.md` 파일 사용

### 특징

- `AGENTS.md`처럼 항상 적용되는 지시사항
- Claude Code 및 기타 Claude 기반 도구와 호환
- 여러 도구에서 동일한 지시사항 사용 가능

### 위치 검색 순서

1. 워크스페이스 루트: `CLAUDE.md`
2. `.claude` 폴더: `.claude/CLAUDE.md`
3. 사용자 홈: `~/.claude/CLAUDE.md`
4. 로컬 변형: `CLAUDE.local.md` (버전 관리 제외)

## AI로 커스텀 지시사항 생성

### 자동 생성

1. 챗에 `/init` 입력 및 엔터
2. 또는 `/create-instructions` 후 설명 입력
3. 또는 에이전트 커스터마이징 에디터에서 `Generate Instructions` 선택

**생성 과정:**
- 기존 AI 규칙 발견 (copilot-instructions.md, AGENTS.md 등)
- 프로젝트 구조 및 코딩 패턴 분석
- 프로젝트에 맞춘 포괄적인 지시사항 생성

### 진행 중인 대화에서 추출

대화 중에 AI의 출력을 수정한 후, "이것으로부터 지시사항을 추출해"라고 요청하면 프로젝트 규칙으로 자동 캡처됩니다.

## 팀 전체로 지시사항 공유

### 조직 레벨 지시사항

GitHub 조직 레벨에서 정의하여 여러 저장소와 워크스페이스에 공유할 수 있습니다.

**활성화:**
- `github.copilot.chat.organizationInstructions.enabled: true` 설정

VS Code는 자동으로 접근 가능한 조직 지시사항을 발견합니다.

### 워크스페이스 레벨 공유

`.github/copilot-instructions.md` 또는 `AGENTS.md`를 버전 관리에 포함시켜 팀원과 공유합니다.

## 디바이스 간 동기화

Settings Sync를 사용하여 사용자 지시사항을 여러 디바이스 간에 동기화할 수 있습니다.

1. Settings Sync 활성화
2. 명령 팔레트에서 `Settings Sync: Configure` 실행
3. "Prompts and Instructions" 선택

## 효과적인 지시사항 작성 팁

### 1. 간결하고 명확하게
- 각 지시사항은 단일하고 단순한 진술
- 필요한 정보는 여러 지시사항으로 분리

### 2. 이유를 포함
- 규칙의 존재 이유를 설명하면 AI가 엣지 케이스에서 더 잘 결정함
- 예: "moment.js 대신 date-fns 사용 (deprecated, 번들 크기 증가)"

### 3. 구체적인 예시 제공
- 추상적 규칙보다 코드 예시가 효과적
- 선호하는 패턴과 피해야 할 패턴 모두 제시

### 4. 표준 도구가 이미 강제하는 규칙 생략
- Linter나 포매터로 자동 적용되는 규칙은 불필요

### 5. 다중 파일 지시사항 활용
- 주제별로 여러 `*.instructions.md` 파일 생성
- `applyTo` 프로퍼티로 선택적 적용

### 6. 프롬프트 파일과 커스텀 에이전트에서 참조
- 지시사항을 다시 작성하지 말고 Markdown 링크로 참조
- 깔끔하고 중복 없음

## 문제 해결

### 지시사항이 적용되지 않는 경우

**확인사항:**
1. 파일이 올바른 위치에 있는가?
   - `.github/copilot-instructions.md`는 워크스페이스 루트에
   - `*.instructions.md`는 `.github/instructions` 또는 사용자 프로필에

2. `applyTo` 글로브 패턴이 현재 파일과 일치하는가?
   - 패턴이 없으면 자동 적용되지 않음

3. 관련 설정이 활성화되어 있는가?
   - `chat.includeApplyingInstructions`
   - `chat.includeReferencedInstructions`
   - `chat.useAgentsMdFile`

**디버깅:**
- 챗 뷰의 우클릭 메뉴에서 `Diagnostics` 선택
- 또는 `Developer: Open Agent Debug Panel` 실행

### 지시사항의 출처 확인

- 명령 팔레트에서 `Chat: Configure Instructions` 실행
- 지시사항에 호버하면 출처 위치가 툴팁에 표시됨

## 우선순위 및 충돌 해결

여러 타입의 지시사항이 동일한 주제에 대해 상충할 때:

1. **개인 지시사항** (최우선)
2. **저장소 지시사항**
3. **조직 지시사항** (최하순)

더 우선순위가 높은 지시사항이 우선됩니다.
