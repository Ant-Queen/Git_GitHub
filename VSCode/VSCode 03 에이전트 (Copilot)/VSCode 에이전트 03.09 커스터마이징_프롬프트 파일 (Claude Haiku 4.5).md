# VS Code 프롬프트 파일 (Prompt Files)

## 개요

**프롬프트 파일** (슬래시 명령)은 일반적인 작업을 위한 **재사용 가능한 프롬프트**를 마크다운 파일로 인코딩합니다. 매번 같은 명령어를 입력할 필요 없이, 파일에 정의된 지침과 컨텍스트를 포함시킵니다.

### 핵심 특징

- **쉬운 호출**: `/프롬프트명` 입력으로 실행
- **재사용 가능**: 여러 대화에서 반복 사용
- **컨텍스트 포함**: 입력 변수와 도구 지정 가능
- **가벼움**: 단일 작업용 (지속적 페르소나 필요 없음)

## 프롬프트 파일 vs 다른 커스터마이징

| 구분 | 프롬프트 파일 | 커스텀 에이전트 | 에이전트 스킬 |
|------|-------------|-------------|------------|
| **용도** | 가벼운 단일 작업 | 지속적 페르소나 | 다단계 워크플로우 |
| **호출** | 수동 (`/명령`) | 항상 활성 또는 선택 | 자동 또는 수동 |
| **도구 제한** | 제한 가능 | 제한 가능 | 스킬에 포함 |
| **핸드오프** | 없음 | 지원 | 없음 |
| **구조** | 단순 Markdown | Markdown + 프론트매터 | Markdown + 리소스 |

## 프롬프트 파일 위치

| 범위 | 위치 |
|------|------|
| 워크스페이스 | `.github/prompts/` 폴더 |
| 사용자 프로필 | VS Code 프로필 데이터 디렉토리 |

### 위치 커스터마이징

`chat.promptFilesLocations` 설정으로 추가 위치 지정:

```json
{
  "chat.promptFilesLocations": {
    ".github/prompts": true,
    "custom/prompts": true,
    "~/my-prompts": true
  }
}
```

### 모노레포 지원

`chat.useCustomizationsInParentRepositories: true`로 부모 저장소의 프롬프트 발견 가능.

## 프롬프트 파일 포맷

### 파일 확장자

`.prompt.md` 확장자 사용

### YAML 프론트매터 (선택)

```yaml
---
name: react-component
description: React 컴포넌트 생성 프롬프트
agent: agent
model: "Claude Sonnet 4.5"
tools: ['createFiles', 'editFiles']
argument-hint: "[컴포넌트명] [스타일링]"
---
```

### 프론트매터 필드

| 필드 | 필수 | 설명 |
|------|------|------|
| **name** | 아니오 | 프롬프트 이름 (`/` 메뉴에 표시, 기본값: 파일명) |
| **description** | 아니오 | 프롬프트 설명 |
| **agent** | 아니오 | 실행 에이전트 (ask, agent, plan, 커스텀 에이전트명) |
| **model** | 아니오 | 사용 모델 (기본값: 현재 선택 모델) |
| **tools** | 아니오 | 사용 가능한 도구 목록 |
| **argument-hint** | 아니오 | 사용자 입력 가이드 텍스트 |

### Markdown 본문

프롬프트의 실제 지침과 가이드:

- 구체적인 작업 설명
- 입력 예시
- 출력 형식 요청사항
- 참고 사항

### 파일 참조

마크다운 링크로 다른 파일 참조:

```markdown
- [커스텀 지시사항 참조](../instructions/react-style.instructions.md)
- [API 문서](./api-reference.md)
```

상대 경로 사용, 프롬프트 파일 위치 기준.

### 도구 참조

본문에서 도구를 참조하려면:

```markdown
#tool:web/fetch를 사용하여 API 호출
#tool:editFiles로 파일 수정
#tool:browser로 브라우저 제어
```

## 프롬프트 파일 생성

### 방법 1: 에이전트 커스터마이징 에디터

1. 챗 뷰에서 설정(기어) 아이콘 선택
2. 에이전트 커스터마이징 에디터 열기
3. 프롬프트 탭에서 `New Prompt` 선택
4. 워크스페이스 또는 사용자 선택
5. 파일명 입력
6. 마크다운 작성

### 방법 2: 명령 팔레트

```
Chat: New Prompt File
또는
Chat: New Untitled Prompt File
```

### 방법 3: 빠른 메뉴

```
/prompts
```

에이전트 커스터마이징 메뉴 열기

### 방법 4: AI로 생성

```
/create-prompt
```

프롬프트 작업 설명 (예: "단위 테스트 생성 프롬프트")
- AI가 질문 후 `.prompt.md` 생성

진행 중인 대화에서:
```
"이를 재사용 가능한 프롬프트로 만들어줘"
또는
"이 워크플로우를 프롬프트로 저장해"
```

## 프롬프트 파일 실행

### 방법 1: 슬래시 명령

채팅에서:
```
/프롬프트명
```

추가 정보도 포함 가능:
```
/create-react-form formName=MyForm
/create-api "고객 목록 API"
```

### 방법 2: 명령 팔레트

```
Chat: Run Prompt
```

목록에서 프롬프트 선택

### 방법 3: 에디터 버튼

프롬프트 파일을 에디터에서 열면:
- 제목 영역의 재생 버튼 클릭
- 현재 대화 또는 새 대화에서 실행 선택

**장점:** 프롬프트 수정 후 빠르게 테스트 가능

### 프롬프트 권장 표시

`chat.promptFilesRecommendations: true`로 설정:

신규 채팅 시 관련 프롬프트가 추천 액션으로 나타남.

## 도구 목록 우선순위

프롬프트 파일과 커스텀 에이전트 모두 `tools`를 지정할 때:

**우선순위 (높음 → 낮음):**

1. **프롬프트 파일의 도구** (있으면)
2. **프롬프트가 참조하는 커스텀 에이전트의 도구** (있으면)
3. **선택된 에이전트의 기본 도구**

프롬프트 파일의 도구가 가장 높은 우선순위.

## 입력 변수

### 기본 변수

프롬프트 본문에서 사용 가능:

| 변수 | 의미 |
|------|------|
| **${selection}** | 에디터의 현재 선택 텍스트 |
| **${input:변수명}** | 사용자 입력 요청 |
| **${input:변수명:플레이스홀더}** | 플레이스홀더 포함 입력 |

### 예시

```markdown
---
name: refactor
description: 코드 리팩토링
---

# 코드 리팩토링

현재 선택한 코드:
${selection}

# 요청
${input:refactorGoal:예: 가독성 개선, 성능 최적화}

이 코드를 다음 목표에 맞게 리팩토링하세요: ${refactorGoal}
```

대부분의 언어 모델이 이 문법을 이해하고 입력 요청을 처리합니다.

## Settings Sync로 프롬프트 동기화

### 프롬프트 파일 동기화

여러 디바이스 간 동기화:

1. Settings Sync 활성화
2. `Settings Sync: Configure` 실행
3. **"Prompts and Instructions"** 선택

사용자 프롬프트 파일이 모든 디바이스에서 사용 가능해집니다.

## 효과적인 프롬프트 작성 팁

### 1. 명확한 설명

프롬프트가 수행할 작업과 예상 출력을 명확히:

```markdown
---
name: unit-tests
description: 함수에 대한 단위 테스트 작성
---

# 단위 테스트 생성

주어진 함수에 대해 포괄적인 단위 테스트 작성.
- 정상 케이스
- 엣지 케이스
- 에러 처리
```

### 2. 예시 제공

입력과 출력 예시로 명확히:

```markdown
## 입력 예시
function add(a, b) {
  return a + b;
}

## 출력 예시
describe('add', () => {
  test('두 양수 더하기', () => {
    expect(add(2, 3)).toBe(5);
  });
});
```

### 3. 지시사항 링크

중복을 피하고 지시사항 참조:

```markdown
[프로젝트 테스트 표준](../instructions/test-standards.md) 참조
```

### 4. 유연한 입력 변수

프롬프트를 다양하게 사용할 수 있게:

```markdown
${input:targetLanguage:예: Python, JavaScript}
${input:testFramework:예: Jest, pytest}
```

### 5. 도구 명시

프롬프트에 필요한 도구 명시:

```yaml
tools: ['createFiles', 'editFiles']
```

### 6. 에디터 플레이 버튼 활용

파일을 에디터에서 열어 테스트:
- 프롬프트 수정 후 빠른 검증
- 반복 개선 가능

## 실제 예제

### 예제 1: React 폼 생성

```markdown
---
name: create-react-form
description: React 함수형 컴포넌트로 폼 생성
tools: ['createFiles']
argument-hint: "[폼명] [필드들]"
---

# React 폼 생성

주어진 요구사항에 맞는 React 폼 컴포넌트를 생성하세요.

## 요구사항
- 폼명: ${input:formName}
- 필드: ${input:fields}
- 유효성 검사: 기본 유효성 검사 포함

## 출력
- React 17+ 호환
- 함수형 컴포넌트 (hooks 사용)
- Tailwind CSS로 스타일링
```

### 예제 2: REST API 보안 검토

```markdown
---
name: security-review-api
description: REST API의 보안 취약점 검토
tools: ['search', 'codeBaseSearch']
---

# REST API 보안 검토

이 API의 보안을 다음 관점에서 검토하세요:

1. **인증/인가**
   - JWT 검증 적절한가?
   - 권한 확인 있는가?

2. **입력 검증**
   - 모든 입력 검증되는가?
   - SQL 인젝션 방지?

3. **데이터 보안**
   - 민감 정보 암호화?
   - HTTPS 사용?

각 문제에 대해:
- 심각도 표시
- 구체적 설명
- 수정 방안 제시
```

### 예제 3: 커밋 메시지 생성

```markdown
---
name: generate-commit-message
description: 변경 사항에 기반한 커밋 메시지 생성
tools: ['search']
---

# 커밋 메시지 생성

현재 변경 사항을 기반으로 명확하고 설명적인 커밋 메시지 생성.

## 포맷

```
[타입](범위): 주제

본문 (선택)
```

## 타입
- feat: 새 기능
- fix: 버그 수정
- refactor: 코드 구조 개선
- test: 테스트 추가

## 요구사항
- 주제: 50자 이내
- 명확하고 구체적
- 현재형 사용 ("added" ✗, "add" ✓)
```

## 프롬프트 권장 지정

워크스페이스 설정에서 특정 프롬프트를 권장으로 표시:

```json
{
  "chat.promptFilesRecommendations": true
}
```

관련 프롬프트가 신규 채팅에서 추천 액션으로 나타남.

## 커뮤니티 프롬프트

### 오픈 소스 리소스

- **awesome-copilot**: https://github.com/github/awesome-copilot/
  - 커뮤니티 기여 프롬프트
  - 에이전트, 스킬도 포함

### 공유 방법

1. 프롬프트 파일 작성
2. GitHub 저장소에 커밋
3. awesome-copilot에 PR 제출
4. 다른 사용자와 공유

## 프롬프트 파일 검색

### UI에서 찾기

1. `@agentPlugins` (플러그인 포함)
2. 또는 명령 팔레트: `Chat: Configure Prompt Files`
3. 프롬프트 목록에서 소스 확인

### 출처 확인

```
Chat: Configure Prompt Files
```

프롬프트에 호버하면 출처 표시:
- 내장
- 사용자 정의 (프로필)
- 워크스페이스
- 확장 기여

## 문제 해결

### 프롬프트가 나타나지 않음

**확인:**
1. 파일이 `.prompt.md` 확장자인가?
2. 올바른 위치에 있는가? (`.github/prompts/` 또는 설정 위치)
3. 마크다운 문법이 올바른가?
4. VS Code 재시작 필요?

### 입력 변수가 작동하지 않음

- `${input:변수명}` 문법 확인
- 변수명에 공백이 없는가?
- 모델이 문법을 이해하는가? (대부분의 최신 모델 지원)

### 도구가 사용 불가능

**확인:**
1. 도구명이 정확한가?
2. 도구가 환경에서 사용 가능한가?
3. MCP 서버가 실행 중인가? (MCP 도구의 경우)
4. 에이전트가 도구 사용 지원하는가?

## 고급 팁

1. **템플릿화**: 유사 작업의 기본 템플릿 생성
2. **버전 관리**: 프롬프트를 저장소에 커밋
3. **테스트**: 에디터 플레이 버튼으로 프롬프트 검증
4. **문서화**: 프롬프트 설명 명확하게
5. **재사용**: 여러 프롬프트에서 지시사항 파일 참조
6. **조합**: 프롬프트 → 커스텀 에이전트 → 핸드오프로 복잡한 워크플로우 구성

## 프롬프트 파일 체크리스트

새 프롬프트 생성 시:

- [ ] 파일명이 설명적인가?
- [ ] 명확한 `description` 작성?
- [ ] 예시 입력/출력 포함?
- [ ] 필요한 `tools` 명시?
- [ ] 참고 자료 링크 추가?
- [ ] 에디터에서 테스트?
- [ ] 팀과 공유?
