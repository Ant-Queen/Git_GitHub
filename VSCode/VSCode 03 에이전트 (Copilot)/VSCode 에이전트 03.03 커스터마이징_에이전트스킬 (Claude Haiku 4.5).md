# VS Code 에이전트 스킬 (Agent Skills)

## 개요

에이전트 스킬은 **오픈 표준**을 따르는 폴더로, 지시사항, 스크립트, 리소스를 패키징합니다. Copilot이 작업과 관련된 스킬을 자동으로 로드하거나 사용자가 수동으로 호출할 수 있습니다.

### 핵심 특징
- **재사용 가능**: VS Code, Copilot CLI, Copilot Cloud Agent에서 동작
- **효율적 로딩**: 관련 스킬만 컨텍스트에 로드됨
- **오픈 표준**: agentskills.io 기반
- **휴대 가능**: 여러 프로젝트와 도구에서 재사용 가능

## 에이전트 스킬 vs 커스텀 지시사항

| 구분 | 에이전트 스킬 | 커스텀 지시사항 |
|------|-------------|------------|
| **목적** | 특화된 기능과 워크플로우 제공 | 코딩 표준과 가이드라인 정의 |
| **휴대성** | 모든 AI 도구에서 작동 | VS Code와 GitHub.com만 |
| **콘텐츠** | 지시사항, 스크립트, 리소스 포함 | 지시사항만 포함 |
| **범위** | 작업별, 필요시 로드 | 항상 적용되거나 글로브 패턴 기반 |
| **표준** | 오픈 표준 (agentskills.io) | VS Code 고유 |

**스킬 사용 시기:**
- 재사용 가능한 기능을 다른 AI 도구에서도 쓰고 싶을 때
- 스크립트, 예시, 리소스를 포함해야 할 때
- AI 커뮤니티와 기능을 공유하고 싶을 때
- 테스트, 디버깅, 배포 같은 특화된 워크플로우를 정의하고 싶을 때

**지시사항 사용 시기:**
- 프로젝트 특정 코딩 표준을 정의할 때
- 언어나 프레임워크 규칙을 설정할 때
- 코드 리뷰나 커밋 메시지 가이드라인을 정할 때

## 스킬 생성하기

### 위치

스킬은 특정 폴더 구조로 저장됩니다:

| 타입 | 위치 |
|------|------|
| 프로젝트 스킬 | `.github/skills/`, `.claude/skills/`, `.agents/skills/` |
| 개인 스킬 | `~/.copilot/skills/`, `~/.claude/skills/`, `~/.agents/skills/` |

### 스킬 디렉토리 구조

```
my-skill/
  ├── SKILL.md              # 필수: 스킬 메타데이터와 지시사항
  ├── test-template.js      # 선택: 템플릿 파일
  ├── run-tests.sh          # 선택: 실행 스크립트
  └── examples/
      └── test-scenario.md  # 선택: 예시
```

### 생성 방법

#### 방법 1: 에이전트 커스터마이징 에디터
1. 챗 뷰에서 설정(기어) 아이콘 선택
2. 에이전트 커스터마이징 에디터 열기
3. 스킬 탭에서 `New Skill` 선택
4. 워크스페이스 또는 사용자 선택

#### 방법 2: AI로 생성
1. 챗에 `/create-skill` 입력
2. 원하는 스킬 설명 (예: "통합 테스트 실행 및 디버깅 스킬")
3. AI가 질문 후 `SKILL.md` 생성

#### 방법 3: 빠른 메뉴
- `/skills` 명령으로 커스터마이징 스킬 메뉴 열기

## SKILL.md 파일 포맷

### 헤더 (필수)

YAML 프론트매터:

```yaml
---
name: webapp-testing
description: 웹 애플리케이션 테스트 스킬. 테스트 자동화, 테스트 템플릿, 테스트 시나리오 예시 제공
argument-hint: [테스트 파일] [옵션]
user-invocable: true
disable-model-invocation: false
context: inline
---
```

### 필드 설명

| 필드 | 필수 | 설명 |
|------|------|------|
| **name** | 예 | 유니크한 식별자 (소문자, 숫자, 하이픈만 허용, 최대 64자) |
| **description** | 예 | 스킬 기능 설명 (최대 1024자) |
| **argument-hint** | 아니오 | 슬래시 명령 호출 시 표시되는 힌트 텍스트 |
| **user-invocable** | 아니오 | `/` 메뉴에 표시 여부 (기본값: true) |
| **disable-model-invocation** | 아니오 | 에이전트가 자동 로드 가능 여부 (기본값: false) |
| **context** | 아니오 | 스킬 로드 방식 (`inline` 또는 `fork`, 기본값: inline) |

### 본문 (필수)

마크다운 형식의 상세 지시사항:

- 스킬의 기능과 용도 설명
- 단계별 절차
- 입력/출력 예시
- 포함된 스크립트 또는 리소스 참조

**리소스 참조:**
```markdown
[테스트 템플릿](./test-template.js)
[예시 시나리오](./examples/test-scenario.md)
```

### 예시: 웹 애플리케이션 테스트 스킬

```markdown
---
name: webapp-testing
description: Playwright를 사용한 웹 애플리케이션 자동화 테스트
---

# 웹 애플리케이션 테스트

## 용도
이 스킬은 웹 애플리케이션의 기능 테스트를 자동화합니다.

## 사용 방법
1. 테스트 대상 URL 제공
2. [테스트 템플릿](./test-template.js)을 참조하여 테스트 작성
3. 테스트 실행

## 예시
/webapp-testing https://example.com
```

## 포크 컨텍스트에서 스킬 실행 (실험적)

기본적으로 스킬의 지시사항은 부모 에이전트의 컨텍스트 윈도우에 추가됩니다.

**포크 컨텍스트 사용:**
큰 스킬이나 중간 추론이 메인 대화에 필요 없는 경우, `context: fork`로 설정하면:
- 스킬이 독립적인 서브에이전트에서 실행됨
- 최종 결과만 부모 에이전트에 반환됨
- 메인 대화의 컨텍스트가 깔끔함

**활성화:**
- `github.copilot.chat.skillTool.enabled: true` 설정 필요

**사용 시기:**
- 많은 파일을 읽거나 긴 조사가 필요할 때
- 요약이나 리포트 같은 집중된 결과를 생성할 때
- 최종 출력만 부모 에이전트가 필요할 때

## 스킬을 슬래시 명령으로 사용

스킬은 채팅에서 슬래시 명령으로 사용 가능합니다.

### 기본 사용법
```
/webapp-testing
/github-actions-debugging PR #42
```

### 접근 제어

| 설정 | user-invocable | disable-model-invocation | 용도 |
|------|-------------|------------------|------|
| 기본값 | true | false | 일반 스킬 |
| 백그라운드만 | false | false | 백그라운드 지식 (AI가 필요시 로드) |
| 수동 호출만 | true | true | 필요할 때만 사용 |
| 비활성화 | false | true | 비활성화된 스킬 |

## Copilot이 스킬을 사용하는 방식

### 3단계 로딩 시스템

1. **발견 (Discovery)**
   - Copilot이 SKILL.md의 name과 description 읽음
   - "로그인 페이지 테스트 도와줘" → webapp-testing 스킬 매칭

2. **지시사항 로드 (Instructions Loading)**
   - SKILL.md 본문 전체를 컨텍스트에 로드
   - 상세 테스트 절차와 가이드라인 제공
   - 또는 `/webapp-testing` 직접 입력으로 로드

3. **리소스 접근 (Resource Access)**
   - Copilot이 필요할 때만 리소스 파일 로드
   - test-template.js나 예시 시나리오 액세스

이 3단계 로딩은 많은 스킬을 설치해도 컨텍스트 효율적입니다.

## 공유 스킬 사용

### 커뮤니티 스킬

- **awesome-copilot**: https://github.com/github/awesome-copilot
- **anthropic-skills**: https://github.com/anthropics/skills

### 플러그인 기반 스킬

에이전트 플러그인에 번들된 스킬:
1. 플러그인 설치
2. 설정 스킬 메뉴에서 표시됨
3. 로컬 스킬과 함께 나타남

### 공유 스킬 사용 방법

1. 저장소에서 스킬 디렉토리 확인
2. `.github/skills/` 폴더로 복사
3. `SKILL.md` 파일 검토 및 커스터마이징
4. 필요시 리소스 수정

## 확장에서 스킬 제공

### 필수 폴더 구조

```
extension-root/
└── skills/
    └── my-skill/
        └── SKILL.md
```

### package.json에서 등록

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

### 주의사항

- `SKILL.md`의 `name` 필드는 부모 디렉토리명과 일치해야 함
- 예: 디렉토리 `skills/my-skill/` → name: `my-skill`
- 네임스페이스 프리픽스 사용 금지 (예: `myorg/my-skill` ✗)

## 에이전트 스킬 표준

Agent Skills는 **agentskills.io**에서 정의한 오픈 표준입니다.

**호환 도구:**
- GitHub Copilot in VS Code
- GitHub Copilot CLI
- GitHub Copilot Cloud Agent

이를 통해 한 번 작성한 스킬을 여러 도구에서 재사용할 수 있습니다.

## 효과적인 스킬 작성 팁

1. **명확한 이름과 설명**
   - 스킬의 용도를 명확하게 설명
   - AI가 언제 사용할지 결정 가능하도록

2. **단계별 절차**
   - 복잡한 워크플로우는 단계별로 분해
   - 각 단계의 목표와 산출물 명확히

3. **구체적인 예시**
   - 입력과 출력의 예시 제공
   - 실제 상황 기반 예시 선호

4. **리소스 참조**
   - SKILL.md에서 스크립트/템플릿 참조
   - 상대 경로 사용 (예: `./script.sh`)

5. **문서화**
   - 리소스 목적 명확하게 설명
   - 커스터마이징 지점 표시

## 보안 고려사항

### 공유 스킬 검토
- 공유 스킬 사용 전 항상 검토
- 출처와 권한자 확인
- VS Code의 터미널 도구로 자동 승인 설정 검토

### 리소스 경로 검증
- 스킬의 스크립트 경로 확인
- 의도하지 않은 파일 접근 방지

## 문제 해결

### 스킬이 로드되지 않음

**확인사항:**
1. `SKILL.md`가 스킬 디렉토리에 있는가?
2. 디렉토리명과 `name` 필드가 일치하는가?
3. `name` 필드가 유효한가? (소문자, 숫자, 하이픈만)
4. 플러그인의 스킬인 경우, 플러그인이 활성화되어 있는가?

### AI가 스킬을 자동 로드하지 않음

**확인사항:**
1. `disable-model-invocation: true`가 아닌가?
2. `description`이 명확하고 충분한가?
3. 작업 설명이 스킬 설명과 일치하는가?
