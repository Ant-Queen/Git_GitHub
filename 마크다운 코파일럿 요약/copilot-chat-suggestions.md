# VS Code의 채팅 및 제안 기능

원문:
- Inline Chat: https://code.visualstudio.com/docs/copilot/chat/inline-chat
- Inline Suggestions: https://code.visualstudio.com/docs/copilot/ai-powered-suggestions
- Smart Actions: https://code.visualstudio.com/docs/copilot/copilot-smart-actions

## 인라인 채팅 (Inline Chat)

### 에디터 인라인 채팅

인라인 채팅을 사용하면 편집기나 통합 터미널에서 직접 쉘 명령어에 대한 도움을 받을 수 있습니다.

#### 편집기 인라인 채팅 사용

1. 편집기에서 파일 열기
2. Ctrl+I 단축키 또는 Chat 메뉴에서 "Open Inline Chat" 선택
3. Chat 입력 필드에 프롬프트 입력
4. VS Code가 diff를 표시하고 인라인 제안 표시
5. "Keep" 또는 "Undo"로 변경사항 수락/거부

**팁**: 특정 코드 블록을 선택한 후 Ctrl+I를 누르면 프롬프트가 해당 코드로 범위가 지정됩니다.

**예제**:
```python
# 선택된 코드:
def calculate_factorial(n):
    result = 1
    for i in range(1, n + 1):
        result *= i
    return result

# Ctrl+I로 인라인 채팅 열고:
# "Add input validation to prevent negative numbers"
```

#### 활성 편집 세션에서의 인라인 채팅

파일이 활성 chat 편집 세션에 속하면, Ctrl+I는 Chat 뷰에서 "Ask in Chat"을 열어 기존 세션 컨텍스트를 사용할 수 있습니다.

`inlineChat.askInChat` 설정을 `false`로 설정하여 항상 일반 인라인 채팅 사용 가능.

#### 텍스트 선택 시 시각적 힌트 (실험)

텍스트를 선택했을 때 VS Code가 인라인 채팅 시작을 돕는 시각적 힌트를 표시할 수 있습니다.

`inlineChat.affordance` 설정:
- `off`: 힌트 없음
- `gutter`: 행 번호 영역에 힌트 표시
- `editor`: 커서 위치에 힌트 표시 (라이트벌브와 통합)

### 터미널 인라인 채팅

통합 터미널에서 쉘 명령어에 대한 도움을 받습니다.

1. 터미널 열기 (Ctrl+`)
2. Ctrl+I 또는 Command Palette에서 "Terminal Inline Chat" 실행
3. Chat 입력 필드에 프롬프트 입력

**예제**:
```bash
# 프롬프트: "list the top 5 largest files in the src dir"
# 결과: 쉘 명령어 제안 받음
```

4. "Run" (Ctrl+Enter)으로 터미널에서 명령어 실행
5. 또는 "Insert" (Alt+Enter)로 터미널에 명령어 삽입 후 수정 후 실행

### Quick Chat

가벼운 Chat 패널을 편집기 상단에 열어 빠른 질문과 짧은 상호작용을 위해 사용합니다.

Ctrl+Shift+Alt+L로 Quick Chat 열기 또는 Chat 메뉴에서 "Quick Chat" 선택.

Quick Chat도 Chat 뷰와 동일한 `#`-mentions 및 `@`-mentions 지원.

### 인라인 채팅 모델 변경

`inlineChat.defaultModel` 설정으로 인라인 채팅에 사용할 언어 모델 구성.

더 자세한 내용: https://code.visualstudio.com/docs/copilot/chat/inline-chat

## 인라인 제안 (Inline Suggestions)

### 고스트 텍스트 제안

Copilot은 입력하면서 희미한 고스트 텍스트 제안을 제공합니다(행 완성부터 전체 코드 블록까지).

#### 첫 제안 받기

1. 프로그래밍 언어 파일 열기
2. 입력 시작 - Copilot이 자동으로 제안 표시
3. Tab으로 제안 수락
4. 부분 수락: Ctrl+Right로 단어 또는 줄 단위로 수락

#### 다양한 제안 탐색

호버하여 다양한 제안 확인 가능.

Alt+] 또는 Alt+[로 제안 순환 탐색.

#### 코드 주석으로 제안 생성

코드 주석으로 기대하는 코드에 대한 힌트 제공:

```typescript
// Student 클래스를 만드는 데 주석 사용
// - properties: name (string), age (number), studentId (string)
// - methods: getStudentInfo(), updateAge()
class Student {
    // Copilot이 주석 기반으로 클래스 구현 제안
}
```

### 다음 편집 제안 (Copilot NES)

현재 편집에 따라 다음 코드 편집을 예측합니다.

가터의 화살표가 다음 편집 제안 가능 위치를 표시. Tab으로 제안으로 이동 후 다시 Tab으로 수락.

#### 편집 제안 감소시키기

`editor.inlineSuggest.edits.showCollapsed` 설정으로 코드 변경사항을 접힌 상태로 표시. Tab을 눌러 제안으로 이동하거나 가터 화살표 위에 마우스를 올릴 때까지만 표시.

#### 다음 편집 제안 사용 사례

**실수 잡기 및 수정**:
- 오타 수정 ('const x = 5'를 'conts x = 5'에서 수정)
- 논리 오류 수정 (반전된 삼항 표현식, ||를 &&로 변경)

**의도 변경**:
- Point 클래스를 Point3D로 변경하면 z 변수 추가 제안
- 함수 이름 변경 후 모든 호출 위치에서 업데이트 제안

**리팩토링**:
- 변수명 한 번 변경 후 파일 전체에서 업데이트 제안
- 코드 스타일 자동 일치

#### 다음 편집 제안 활성화

`github.copilot.nextEditSuggestions.enabled` 설정 활성화 필요 (조직 수준에서 관리).

#### 관련 설정

- `github.copilot.nextEditSuggestions.enabled`: 활성화
- `editor.inlineSuggest.edits.allowCodeShifting`: 코드 이동 허용
- `editor.inlineSuggest.edits.renderSideBySide`: 나란히 표시 또는 아래에 표시
- `github.copilot.nextEditSuggestions.fixes`: 진단 기반 제안(누락된 import 등)
- `editor.inlineSuggest.minShowDelay`: 제안 표시 전 대기 시간 (기본값 0ms)

### 인라인 제안 활성화/비활성화

상태 표시줄의 Copilot 메뉴에서 특정 언어별로 인라인 제안 활성화/비활성화 가능.

또는 `github.copilot.enable` 설정을 수정하여 언어별로 설정:

```json
"github.copilot.enable": {
  "*": true,        // 모든 언어 활성화
  "python": false,  // Python에서만 비활성화
  "javascript": true
}
```

일시적 비활성화: 상태 표시줄의 Copilot 메뉴에서 "Snooze" 버튼으로 5분 단위 일시중지.

### 제안용 AI 모델 변경

Command Palette (F1)에서 "GitHub Copilot: Change Completions Model" 실행 후 모델 선택.

### 팁

**컨텍스트**: 관련 파일을 VS Code에서 열어두면 Copilot이 프로젝트의 더 큰 그림을 파악하여 더 적절한 제안을 제공합니다.

**설정**:
- `github.copilot.enable`: 특정 언어 활성화/비활성화
- `editor.inlineSuggest.fontFamily`: 인라인 제안 폰트
- `editor.inlineSuggest.showToolbar`: 도구모음 표시/숨기기
- `editor.inlineSuggest.syntaxHighlightingEnabled`: 문법 강조 표시

더 자세한 내용: https://code.visualstudio.com/docs/copilot/ai-powered-suggestions

## 스마트 액션 (Smart Actions)

### 커밋 메시지 및 PR 정보 생성

코드 변경사항을 기반으로 커밋 메시지 및 PR 제목/설명 생성.

Source Control 뷰의 아이콘이나 GitHub PR 확장에서 스파클 아이콘을 사용하여 커밋 메시지 생성.

AI가 다음을 고려합니다:
- 변경된 파일
- 변경사항의 성격(기능 추가, 버그 수정, 리팩토링)
- 수정 범위 및 영향

생성된 메시지가 마음에 들지 않으면 스파클 아이콘을 다시 클릭하여 다른 스타일의 메시지 생성.

### Git 병합 충돌 AI로 해결 (실험)

편집기에서 "Resolve Merge Conflict with AI" 버튼 선택. Chat 뷰가 열리고 각 브랜치의 변경사항 컨텍스트를 제공하는 에이전트 플로우 시작.

### TODO 주석 구현

GitHub Pull Requests 확장이 설치되어 있다면 AI로 `TODO` 주석을 구현할 수 있습니다.

1. 코드에 `TODO` 주석 추가
2. 주석 옆에 나타나는 code action(라이트벌브) 클릭
3. "Delegate to coding agent" 선택 후 Copilot 클라우드 에이전트가 구현 시작

### 기호 이름 바꾸기

코드에서 기호를 이름 변경할 때 컨텍스트와 코드베이스를 기반으로 AI가 새로운 이름에 대한 제안 제공.

### Markdown에서 이미지 alt 텍스트 생성

1. Markdown 파일 열기
2. 이미지 링크 위에 커서 놓기
3. Code Action(라이트벌브) 클릭 > "Generate alt text" 선택
4. 이미 alt 텍스트가 있으면 "Refine alt text" 선택

### 문서 생성

선택한 코드 블록에 대한 설명 받기:

1. 응용 프로그램 코드 파일 열기
2. 선택사항: 문서화할 코드 선택
3. 우클릭 > "Generate Code" > "Generate Docs"

여러 언어에 대한 코드 문서 생성 지원.

### 테스트 생성

프롬프트를 작성하지 않고 에디터 스마트 액션으로 테스트 생성:

1. 응용 프로그램 코드 파일 열기
2. 선택사항: 테스트할 코드 선택
3. 우클릭 > "Generate Code" > "Generate Tests"

VS Code가 기존 테스트 파일에 테스트 생성 또는 새 테스트 파일 생성.

선택사항으로 Inline Chat 프롬프트에서 추가 컨텍스트 제공하여 생성된 테스트 개선.

### 코드 설명

선택한 코드 블록에 대한 설명 받기:

1. 코드 파일 열기
2. 설명할 코드 선택
3. 우클릭 > "Explain"

### 코딩 오류 수정

1. 코드 파일 열기
2. 수정할 코드 선택
3. 우클릭 > "Generate Code" > "Fix"

또는 컴파일/린팅 문제가 있으면 편집기에 code action 표시됨.

추가 컨텍스트로 Chat 프롬프트에서 생성된 코드 개선 가능.

### 테스트 오류 수정

Test Explorer에서 실패한 테스트를 마우스 올리고 "Fix Test Failure" 버튼(스파클 아이콘) 클릭.

또는 Chat 뷰에서 `/fixTestFailure` 명령 사용.

Copilot의 수정 제안 팔로우.

**팁**: 에이전트 사용 시 테스트 실행을 모니터링하고 실패한 테스트 자동 수정 및 다시 실행 시도.

### 터미널 오류 수정

터미널에서 명령이 실패하면 에디터 거터에 스파클 아이콘 표시. Quick Fix를 선택하여 무슨 일이 일어났는지 설명받음.

### 코드 검토

편집기에서 코드 블록 검토:

1. 코드 파일 열기
2. 검토할 코드 선택
3. 우클릭 > "Generate Code" > "Review"

Comments 패널과 편집기에 검토 주석 표시.

또는 GitHub PR 확장으로 풀 요청 전체 검토:

1. GitHub PR 확장으로 풀 요청 생성
2. Files Changed 뷰에서 "Code Review" 버튼 클릭
3. Comments 패널과 편집기에 검토 주석 표시

### 의미론적 검색 결과 (Preview)

VS Code의 Search 뷰에서 텍스트 정확 일치가 아닌 의미론적으로 관련된 결과 찾기.

`search.searchView.semanticSearchBehavior` 설정으로 의미론적 검색 구성:
- 자동 실행 또는 명시적 요청 시에만 실행

`search.searchView.keywordSuggestions` 설정으로 검색 관련 대체 용어 AI 제안 활성화.

### AI로 설정 검색

정확한 설정 이름을 모를 때 자연어로 검색 가능.

`workbench.settings.showAISearchToggle` 활성화.

"increase text size"라고 검색하면 에디터 폰트 크기 관련 설정 제안됨.

더 자세한 내용: https://code.visualstudio.com/docs/copilot/copilot-smart-actions

---

**최종 업데이트**: 2026년 5월 6일