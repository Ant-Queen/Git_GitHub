# VS Code AI 언어 모델(Language Models)

## 개요
VS Code는 여러 AI 언어 모델 중에서 대화에 적합한 모델을 선택할 수 있게 합니다. 기본 모델 외에도 자체 API 키로 모델을 추가하여 BYOK(Bring Your Own Key) 환경을 구성할 수 있습니다.

## 채팅 모델 변경

- 채팅 입력 필드의 모델 선택기로 모델을 변경합니다.
- 모델마다 속도, 비용, 추론 능력, 툴 호출 지원 여부가 다릅니다.
- 태스크가 복잡할수록 추론 모델을 사용하고, 단순 질의에는 빠른 모델이 적합합니다.

## 생각 노력(Thinking Effort) 구성

- 일부 모델은 `thinking effort`를 지원합니다.
- 선택 가능한 수준은 `None`, `Low`, `Medium`, `High` 등입니다.
- 더 높은 노력은 더 많은 토큰을 사용하므로 비용이 증가합니다.
- 모델 선택기에서 모델 이름 옆의 화살표를 눌러 노력 수준을 조절합니다.

## 자동 모델 선택

- Auto 모드를 사용하면 VS Code가 요청 복잡도와 모델 가용성을 기반으로 최적 모델을 선택합니다.
- 응답 위에 마우스를 올리면 실제로 사용된 모델을 확인할 수 있습니다.

## 언어 모델 관리

- 모델 선택기에서 `Manage Language Models`를 선택합니다.
- 모델을 숨기거나 표시할 수 있습니다.
- 좋아하는 모델은 핀으로 고정하여 상단에 유지할 수 있습니다.
- 검색과 필터링으로 모델을 찾습니다.

## 자체 모델 키(BYOK) 연결

### 빌트인 제공자 모델 추가

- Language Models 편집기에서 `Add Models`를 선택하고 제공자를 선택합니다.
- API 키, 엔드포인트 URL 등 제공자별 구성 정보를 입력합니다.
- Azure OpenAI, OpenAI, Anthropic 등 주요 제공자를 지원합니다.

### 확장 기능으로 모델 제공자 추가

- 마켓플레이스에서 `@tag:language-models` 확장 기능을 설치합니다.
- 확장 기능이 제공하는 모델이 Language Models 편집기에 추가됩니다.
- 예를 들어 Foundry Toolkit 확장을 설치하면 로컬 및 클라우드 모델을 사용할 수 있습니다.

### 사용자 지정 엔드포인트 모델 추가

- `Custom Endpoint` 제공자를 사용하여 Chat Completions, Responses, Messages API를 연결할 수 있습니다.
- 모델이 해당 API 유형을 지원해야 합니다.
- `chatLanguageModels.json` 파일을 사용하여 모델 구성 정보를 저장합니다.

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

## 다른 기능을 위한 모델 구성

- **인라인 채팅**: `inlineChat.defaultModel` 설정으로 인라인 채팅 기본 모델을 지정합니다.
- **인라인 제안**: 에디터 코드 완성 시 사용할 모델을 선택할 수 있습니다.
- **유틸리티 작업**: 제목 생성, 커밋 메시지 생성, 의도 감지 등에 사용할 모델을 `chat.utilityModel`과 `chat.utilitySmallModel`로 구성합니다.

> BYOK 모델을 사용할 때 GitHub 서비스에 의존하는 몇몇 기능(semantic search, inline suggestions 등)은 사용할 수 없을 수 있습니다.

## 모델 구성 참조

`chatLanguageModels.json` 파일의 주요 속성:

- `vendor`: 모델 제공자(예: `azure`, `openai`, `customendpoint`)
- `name`: UI에 표시될 제공자 이름
- `models`: 모델 목록
- `id`: API에 전송할 모델 식별자
- `name`: 모델 표시 이름
- `url`: 모델 엔드포인트
- `apiType`: `chat-completions`, `responses`, `messages`
- `toolCalling`: 도구 호출 지원 여부
- `vision`: 이미지 입력 지원 여부
- `maxInputTokens`: 최대 입력 토큰 수
- `maxOutputTokens`: 최대 출력 토큰 수
- `editTools`: 지원하는 편집 도구 목록
- `thinking`: 추론 기능 지원 여부
- `streaming`: 스트리밍 응답 지원 여부
- `zeroDataRetentionEnabled`: ZDR 사용 여부
- `supportsReasoningEffort`: 지원하는 노력 수준 목록
- `reasoningEffortFormat`: 노력 정보 전달 형식
- `requestHeaders`: 추가 HTTP 요청 헤더

## FAQ

### Copilot Business/Enterprise에서 BYOK를 사용하려면?

관리자가 GitHub Copilot 정책에서 Bring Your Own Language Model Key를 활성화해야 합니다.

### 로컬 모델을 사용할 수 있나?

예. 로컬 모델 제공자를 설치하거나 확장 기능을 사용하여 로컬 모델을 연결할 수 있습니다. 로컬 모델은 인터넷 및 Copilot 플랜 없이도 사용할 수 있습니다.

### 인터넷 없이 로컬 모델만 사용할 수 있나?

예. 적절한 로컬 모델 제공자를 추가하면 완전 오프라인으로 사용할 수 있습니다. 다만 GitHub 서비스에 의존하는 일부 기능은 이용할 수 없습니다.

### Copilot 플랜 없이도 가능한가?

예. BYOK 모델은 GitHub 계정이나 Copilot 플랜 없이도 사용할 수 있습니다. 그러나 일부 Copilot 전용 기능은 제한됩니다.

## 요약

VS Code에서 언어 모델은 단순한 선택지를 넘어서, 자체 모델과 외부 제공자를 연결하여 채팅 및 도구 호출 경험을 확장하는 핵심 요소입니다. 모델 선택기, 관리 화면, 설정 파일을 활용하여 필요한 워크플로우에 맞는 모델을 구성하세요.
