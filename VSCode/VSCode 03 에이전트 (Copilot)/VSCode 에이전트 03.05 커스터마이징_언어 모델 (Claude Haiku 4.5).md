# VS Code 언어 모델 (Language Models)

## 개요

VS Code는 다양한 AI 모델에 접근할 수 있도록 해줍니다. 각 모델은 다양한 작업과 강점을 가지고 있으며, 모델을 선택하거나 자신의 API 키를 가져올 수 있습니다.

### 모델 선택 팁
- **빠른 작업**: 빠른 모델로 간단한 질문과 빠른 편집
- **복잡한 작업**: 추론 모델로 복잡한 리팩토링, 아키텍처 결정, 다단계 작업
- **에이전트 타입**: 사용 중인 에이전트 타입에 따라 사용 가능한 모델이 다를 수 있음

## 채팅용 모델 변경

### 방법 1: 모델 선택기 사용

1. 챗 입력 필드의 모델 선택기 열기
2. 원하는 모델 선택
3. 해당 대화에서 사용됨

### 방법 2: 모델 선택기 심화

원하는 모델이 보이지 않으면:
- "관리" 옵션으로 더 많은 모델 확인 가능
- AI 툴킷 확장으로 더 많은 모델 추가 가능

## 추론 노력 (Thinking Effort) 설정

### 개념

일부 모델은 "생각 노력"을 지원합니다. 이는 모델이 각 요청에 적용하는 추론량을 제어합니다.

### 기본 설정

- VS Code는 권장 노력 수준 설정
- 적응형 추론 활성화 (모델이 복잡도에 따라 동적 결정)
- 대부분의 경우 기본값이 적절

### 추론 노력 구성

1. 모델 선택기에서 추론 모델 선택
2. 모델명 옆의 `>` 화살표 클릭
3. "생각 노력" 서브메뉴에서 레벨 선택

### 노력 수준

| 레벨 | 설명 | 사용 시기 |
|------|------|---------|
| **None** | 추론 없음 | 빠른 답변 필요 |
| **Low** | 가벼운 추론 | 일반 작업 |
| **Medium** | 중간 정도 추론 | 복잡한 작업 |
| **High** | 심층 추론 | 매우 복잡한 작업 |

### 주의사항

높은 추론 노력은 더 많은 생각 토큰을 생성하여 **AI 크레딧 소비 증가**합니다. 필요한 경우에만 증가하세요.

## 자동 모델 선택 (Auto Model Selection)

### 개념

VS Code가 작업 복잡도와 실시간 모델 가용성을 평가하여 최적 모델로 라우팅합니다.

### 사용 방법

1. 모델 선택기에서 "Auto" 선택
2. 각 응답 위에 호버하면 사용된 모델 확인 가능

### 이점
- 수동 선택 불필요
- 항상 최적 모델 사용
- 비용 효율적

## 언어 모델 관리

### 언어 모델 에디터 열기

**방법 1: 모델 선택기**
- 모델 선택기의 기어 아이콘(관리) 클릭

**방법 2: 명령 팔레트**
```
Chat: Manage Language Models
```

### 에디터 기능

- 모든 사용 가능한 모델 표시
- 모델 기능, 컨텍스트 크기, 청구 정보 표시
- 모델 가시성 상태 변경
- 새 모델 추가

### 필터링 옵션

모델을 다음으로 필터링:
- 텍스트 검색
- `@provider:"OpenAI"` - 제공자별
- `@capability:tools` - 도구 지원
- `@capability:vision` - 이미지 지원
- `@capability:agent` - 에이전트 지원
- `@visible:true/false` - 가시성 상태

## 모델 선택기 커스터마이징

### 모델 가시성 변경

1. 언어 모델 에디터에서 모델에 호버
2. 눈 아이콘 클릭하여 표시/숨김 토글

### 선호 모델 고정 (Pin)

1. 모델 선택기에서 모델에 호버
2. 핀 아이콘 클릭
3. 고정된 모델은 목록 상단의 고정 섹션에 배치됨

**이점:**
- 자주 사용하는 모델을 쉽게 접근 가능
- 다른 모델 사용 시에도 위치 유지

## 자신의 언어 모델 키 가져오기 (BYOK)

### 개념

자신의 API 키로 모든 호환 모델 제공자에 연결할 수 있습니다. GitHub 계정이나 Copilot 계획 없이도 가능합니다.

### BYOK 지원 범위

✅ **지원:**
- 채팅 경험
- 유틸리티 작업 (제목 생성, 커밋 메시지 등)
- 오프라인 모드 (로컬 모델)

❌ **미지원:**
- 의미론적 검색 (semantic search)
- 인라인 제안 (코드 완성)
- 임베딩 기반 기능

### 모델 추가 옵션

#### 1. 내장 제공자
```
Azure, Anthropic, Gemini, OpenAI 등
```

#### 2. 확장 제공자
```
Visual Studio Marketplace에서 설치 가능
예: AI Toolkit for local models
```

#### 3. 커스텀 엔드포인트 (미리보기)
```
자체 호스팅, 엔터프라이즈, 기타 엔드포인트
```

### 내장 제공자에서 모델 추가

1. 언어 모델 에디터 열기
2. "모델 추가" 선택
3. 제공자 선택 (Azure, OpenAI, Anthropic 등)
4. 그룹명 입력 (모델 선택기에 표시됨)
5. 제공자 별 세부 정보 입력 (API 키 등)
6. `chatLanguageModels.json` 파일에서 모델 설정 완료

### 모델 제공자 확장 설치

1. 언어 모델 에디터 열기
2. "모델 제공자 설치" 선택
3. 확장 마켓플레이스에서 찾기
4. 설치 후 확장 설정 지시사항 따르기

### 커스텀 엔드포인트 모델 추가

1. 언어 모델 에디터 열기
2. "모델 추가" → "커스텀 엔드포인트" 선택
3. 그룹명 입력
4. 표시명과 API 키 입력
5. API 타입 선택:
   - Chat Completions
   - Responses
   - Messages
6. `chatLanguageModels.json`에서 세부 설정

### Anthropic 엔드포인트 예시

```json
[
  {
    "name": "Anthropic",
    "vendor": "customendpoint",
    "apiKey": "YOUR_API_KEY",
    "apiType": "messages",
    "models": [
      {
        "id": "claude-sonnet-4-6",
        "name": "Claude Sonnet 4.6",
        "url": "https://api.anthropic.com/v1/messages",
        "toolCalling": true,
        "vision": true,
        "maxInputTokens": 200000,
        "maxOutputTokens": 64000
      }
    ]
  }
]
```

## 모델 제공자 세부 정보 업데이트

이전에 구성한 모델 제공자의 설정 변경:

1. 언어 모델 에디터 열기
2. 제공자명 옆의 기어 아이콘 선택
3. API 키나 엔드포인트 URL 등 업데이트

## 다른 기능용 모델 설정

### 인라인 채팅 모델 변경

인라인 채팅에만 다른 모델 사용:

1. 인라인 채팅 세션 중에 모델 선택기 사용
2. 또는 설정에서 `inlineChat.defaultModel` 구성

### 인라인 제안 모델 변경

코드 완성 모델 변경:

1. 챗 메뉴에서 "인라인 제안 구성..." 선택
2. "완성 모델 변경..." 선택
3. 목록에서 모델 선택

**주의:**
- 사용 가능한 모델은 제한적일 수 있음
- Copilot Business/Enterprise 사용자는 관리자 승인 필요

### 유틸리티 작업용 모델 변경

제목 생성, 커밋 메시지 등 백그라운드 작업용 모델:

```json
{
  "chat.utilityModel": "Default",
  "chat.utilitySmallModel": "Default"
}
```

**두 가지 설정:**
- `chat.utilityModel`: 일반 유틸리티 작업 (제목, 요약 등)
- `chat.utilitySmallModel**: 빠른 경량 작업 (커밋 메시지, 이름 생성 등)

**BYOK 모드 주의:**
- GitHub 계정 없이 BYOK만 사용 중이면 유틸리티 모델 설정 필수

## 모델 구성 참고

BYOK 모델 추가 시 `chatLanguageModels.json`에서 설정 가능한 속성:

### 제공자 레벨 속성

| 속성 | 설명 |
|------|------|
| **vendor** | 제공자 (azure, openai, customendpoint 등) |
| **name** | 표시명 |
| **models** | 모델 배열 (선택) |

### 모델 레벨 속성

| 속성 | 필수 | 설명 |
|------|------|------|
| **id** | 예 | API에 전송되는 모델 식별자 |
| **name** | 예 | 모델 선택기에 표시되는 이름 |
| **url** | 예 | 모델 엔드포인트 전체 URL |
| **apiType** | 아니오 | API 타입 재정의 (chat-completions, responses, messages) |
| **toolCalling** | 아니오 | 도구 호출 지원 여부 (기본값: false) |
| **vision** | 아니오 | 이미지 입력 지원 여부 (기본값: false) |
| **maxInputTokens** | 아니오 | 최대 입력 토큰 |
| **maxOutputTokens** | 아니오 | 최대 출력 토큰 |
| **editTools** | 아니오 | 지원하는 편집 도구 배열 |
| **thinking** | 아니오 | 생각 기능 지원 여부 (기본값: false) |
| **streaming** | 아니오 | 스트리밍 응답 지원 (기본값: true) |
| **supportsReasoningEffort** | 아니오 | 지원 추론 노력 레벨 배열 |
| **requestHeaders** | 아니오 | 추가 HTTP 헤더 |

### 주의사항

- `maxInputTokens + maxOutputTokens` ≤ 모델의 실제 컨텍스트 윈도우
- VS Code는 이 합을 모델의 총 컨텍스트로 사용
- 제공자 문서에서 컨텍스트 윈도우 크기 확인

## 로컬 모델 사용

### 로컬 모델로 실행

1. Ollama 등 로컬 모델 제공자 설치
2. 언어 모델 관리자에서 추가
3. 오프라인에서도 사용 가능

### 유틸리티 기능 활성화

로컬 모델만 사용할 경우:
```json
{
  "chat.utilityModel": "local-model-name",
  "chat.utilitySmallModel": "local-model-name"
}
```

### 제한사항

로컬 모델로는 **지원되지 않음**:
- 의미론적 검색
- 인라인 제안
- 임베딩 기반 기능

이들은 GitHub Copilot 서비스가 필요합니다.

## Copilot Business/Enterprise용 BYOK

Copilot Business 또는 Enterprise 사용자:

1. 관리자가 "VS Code에서 자신의 언어 모델 키 가져오기" 정책 활성화
2. GitHub의 Copilot 정책 설정에서 활성화
3. 개인 계정처럼 모델 추가 가능

자세한 내용: [GitHub 문서](https://docs.github.com/en/copilot/how-tos/administer-copilot/manage-for-enterprise/use-your-own-api-keys)

## 자주 묻는 질문

### Q: GitHub 계정 없이 로컬 모델 사용 가능?

**A:** 예. BYOK 모델은 GitHub 계정이나 Copilot 계획 없이도 작동합니다.

### Q: 여러 모델 제공자 동시 사용 가능?

**A:** 예. 여러 제공자에서 모델을 추가하고 필요에 따라 전환할 수 있습니다.

### Q: 인터넷 없이 사용 가능?

**A:** 로컬 모델의 경우 완전 오프라인 사용 가능합니다. 클라우드 모델은 인터넷 필요합니다.

### Q: 모델이 모델 선택기에 나타나지 않음

**A:**
1. 모델이 도구 호출 지원하는가? (에이전트 사용 시 필수)
2. 모델 구성이 올바른가? `chatLanguageModels.json` 확인
3. VS Code 재시작 필요

### Q: API 비용 절감 방법?

**A:**
- 빠른 작업에는 저가 모델 사용
- 복잡한 작업에만 프리미엄 모델 사용
- 로컬 모델 활용

## 모델 관리 팁

1. **자주 사용하는 모델 고정**: 모델 선택기에서 빠른 접근
2. **불필요한 모델 숨기기**: 깔끔한 목록 유지
3. **기본값 설정**: 각 작업 타입별 기본 모델 지정
4. **성능 모니터링**: 모델별 응답 시간과 비용 추적
