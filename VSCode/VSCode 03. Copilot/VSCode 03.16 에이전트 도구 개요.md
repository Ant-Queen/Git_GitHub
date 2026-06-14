# VS Code Copilot 에이전트 도구 개요

## 개요

에이전트 도구는 VS Code에서 에이전트가 특정 작업을 수행하도록 확장하는 기능입니다. 검색, 코드 분석, 웹 요청, 터미널 명령 실행 등 다양한 도구를 에이전트와 함께 사용할 수 있습니다.

## 채팅에서 도구 활성화

- 채팅 뷰에서 도구를 사용하려면 먼저 도구를 활성화해야 합니다.
- 도구 선택기는 채팅 입력 필드에서 `Configure Tools` 버튼으로 열 수 있습니다.
- 도구를 요청별로 선택/해제하여 현재 작업에 필요한 도구만 사용하면 결과가 더 좋아집니다.
- 추가 도구는 MCP 서버나 확장 기능을 설치하여 가져올 수 있습니다.

## 프롬프트에서 도구 사용

- 에이전트는 활성화된 도구 중에서 작업에 필요한 도구를 자동으로 선택하고 호출합니다.
- 특정 도구를 사용하려면 프롬프트에 `#도구이름`을 명시적으로 입력할 수 있습니다.
- 예시:
  - `What is the latest version of Node.js #web`
  - `Fix the issues in #problems`
  - `Explain the authentication flow #codebase`
- 채팅에서 도구 호출 세부 정보는 기본적으로 접혀 있으므로 원하는 경우 펼쳐볼 수 있습니다.

## 권한 수준

- 에이전트의 자율성과 도구 호출 방식을 제어하는 옵션입니다.
- 권한 수준은 채팅 입력 영역의 권한 선택기에서 설정합니다.

### 주요 권한 수준

- Default Approvals
  - 설정된 승인 규칙을 따릅니다.
  - 민감한 도구는 실행 전에 확인 대화상자를 표시합니다.
- Bypass Approvals
  - 모든 도구 호출을 자동 승인합니다.
  - 오류 발생 시 자동 재시도합니다.
- Autopilot (Preview)
  - 모든 도구 호출을 자동 승인하고, 질문에 자동 응답하며 작업을 자율적으로 계속합니다.

> 주의: Bypass Approvals와 Autopilot은 파일 편집, 터미널 명령, 외부 도구 호출 등의 수동 승인 프롬프트를 우회합니다. 보안 영향을 이해한 후 사용하세요.

## 도구 승인

- 도구 호출 전 승인이 필요한 경우 확인 다이얼로그가 표시됩니다.
- 도구 세부 정보를 검토하고 한 번만, 현재 세션, 현재 워크스페이스, 또는 모든 이후 호출에 대해 승인할 수 있습니다.
- `Chat: Manage Tool Approval` 명령으로 도구 승인 상태를 중앙에서 관리할 수 있습니다.

### 자동 승인 구성(실험적)

- `chat.tools.eligibleForAutoApproval` 설정으로 특정 도구에 대해 자동 승인을 비활성화할 수 있습니다.
- 조직에서는 이 설정을 통해 특정 도구에 대해 항상 수동 승인을 요구할 수 있습니다.

## URL 승인

- `#web/fetch` 같은 도구가 URL에 접근하려 할 때 두 단계 승인 프로세스를 거칩니다.
- 사전 승인: URL 요청 자체를 허용할지 결정합니다.
- 사후 승인: 가져온 콘텐츠를 채팅에 추가하기 전에 검토하고 허용합니다.
- 많은 경우 `Trusted Domains` 설정에 있는 도메인은 사전 승인이 자동으로 허용됩니다.
- 그러나 사후 승인은 항상 수동으로 검토해야 합니다.
- URL 자동 승인 설정은 `chat.tools.urls.autoApprove`에서 도메인별 또는 URL별로 구성할 수 있습니다.

## 도구 매개변수 편집

- 도구 확인 대화상자에서 도구 입력 매개변수를 확장하여 실행 전에 수정할 수 있습니다.
- 수정 후 `Allow`를 선택하면 변경된 매개변수로 도구가 실행됩니다.

## 터미널 명령

- 에이전트는 터미널 명령을 실행할 수 있습니다.
- 채팅 대화에서 명령 실행 결과를 `Show Output`으로 바로 볼 수 있고, `Show Terminal`로 통합 터미널에서 전체 출력을 확인할 수 있습니다.
- 장기 실행 명령은 `Continue in Background` 버튼으로 백그라운드 실행할 수 있습니다.
- 타임아웃이 설정된 경우 에이전트는 시간 초과 시점까지 수집된 출력을 반환합니다.
- 터미널 출력을 채팅에 유지하거나 통합 터미널에서 확인할 수 있습니다.

### 터미널 명령 자동 승인

- `chat.tools.terminal.autoApprove` 설정으로 특정 터미널 명령을 자동 승인하거나 거부할 수 있습니다.
- 명령 배열 또는 정규식 패턴을 사용해 허용/차단 규칙을 정의할 수 있습니다.
- 예시:
  - `mkdir`: 자동 승인
  - `/^git (status|show\b.*)$/`: `git status`와 `git show` 계열 명령 자동 승인
  - `del`: 거부
  - `/dangerous/`: 위험한 명령어 거부
- 기본적으로 각 서브커맨드가 개별적으로 매칭됩니다. 자동 승인을 위해서는 모든 서브커맨드가 `true` 규칙과 일치하고 `false` 규칙과 일치하지 않아야 합니다.
- 전체 명령줄을 기준으로 매칭하려면 `matchCommandLine` 속성을 사용하세요.

#### 관련 설정

- `chat.tools.terminal.enableAutoApprove`: 조직 관리형 설정으로 자동 승인 기능을 완전히 비활성화할 수 있습니다.
- `chat.tools.terminal.blockDetectedFileWrites` (실험적): `outsideWorkspace`로 설정하면 워크스페이스 외부 파일 쓰기 명령에 대해서는 수동 승인을 요구합니다.
- `chat.tools.terminal.ignoreDefaultAutoApproveRules` (실험적): 기본 자동 승인 규칙을 모두 무시합니다.

> 주의: 터미널 명령 자동 승인은 완전한 보안을 보장하지 않습니다. 프롬프트 인젝션 가능성이 있는 경우 에이전트 샌드박싱 또는 컨테이너 내 실행을 고려하세요.

## 샌드박스 에이전트 명령

- 샌드박싱은 에이전트 명령의 파일 시스템 및 네트워크 액세스를 제한합니다.
- `chat.agent.sandbox.enabled` 설정을 사용해 샌드박싱을 켤 수 있습니다.
- `on`: 전체 샌드박싱(파일 시스템 + 네트워크 격리)
- `allowNetwork`: 파일 시스템 격리만 적용하고 네트워크는 자유롭게 허용
- `off`: 샌드박싱 비활성화

### 파일 시스템 액세스 구성

- `chat.agent.sandbox.FileSystem.linux` 또는 `chat.agent.sandbox.FileSystem.mac` 설정에서 접근 규칙을 정의합니다.
- `allowRead`, `allowWrite`, `denyRead`, `denyWrite` 규칙을 통해 특정 경로를 허용 또는 차단합니다.
- `deny` 규칙이 `allow` 규칙보다 우선합니다.
- 작업 공간 폴더와 샌드박스 임시 폴더는 자동으로 허용됩니다.
- 명령 실행 시 필요한 경로는 자동으로 허용 목록에 추가됩니다.

### 네트워크 액세스 구성

- `chat.agent.networkFilter`를 활성화하면 도메인 필터링이 작동합니다.
- `chat.agent.allowedNetworkDomains`와 `chat.agent.deniedNetworkDomains`로 도메인별 허용/차단을 정의합니다.
- 빈 목록인 경우 기본적으로 모든 도메인이 차단됩니다.
- `deny` 도메인은 `allow` 도메인보다 우선합니다.
- 와일드카드 패턴(`*.example.com`)을 사용할 수 있습니다.
- `allowNetwork` 모드에서는 네트워크 필터링 설정이 무시되고 모든 아웃바운드 연결이 허용됩니다.

> 참고: 샌드박싱은 터미널 명령에만 적용되며, 내장 파일 도구에는 VS Code 자체 권한 시스템이 사용됩니다.

## 도구 세트 그룹화

### 도구 세트 생성

- `Chat: Configure Tool Sets` 명령에서 새 도구 세트 파일을 생성할 수 있습니다.
- JSONC 파일에 도구 그룹을 정의합니다.
- 예:
  ```jsonc
  {
    "reader": {
      "tools": ["search/changes", "search/codebase", "read/problems", "search/usages"],
      "description": "Tools for reading and gathering context",
      "icon": "book"
    }
  }
  ```
- `tools`에 빌트인 도구, MCP 도구, 확장 도구를 지정할 수 있습니다.
- `description`은 도구 선택기에서 표시되는 설명입니다.
- `icon`은 도구 세트 아이콘입니다.

### 도구 세트 사용

- 프롬프트에서 `#도구세트이름`으로 도구 세트를 참조할 수 있습니다.
- 예:
  - `Analyze the codebase for security issues #reader`
  - `Where is the DB connection string defined? #search`
- 도구 선택기에서 도구 세트는 관련 도구 그룹으로 표시되어 쉽게 선택할 수 있습니다.
- 빌트인 도구 중 일부는 이미 `#edit`, `#search`처럼 도구 세트에 포함되어 있습니다.

## 자주 묻는 질문

### 어떤 도구가 사용 가능한지 어떻게 알 수 있나요?

- 채팅 입력창에 `#`를 입력하면 사용 가능한 도구 목록이 표시됩니다.
- 도구 선택기에서도 활성 도구 목록을 볼 수 있습니다.

### 요청당 도구 수가 128개를 초과하면 어떻게 하나요?

- 도구 선택기에서 일부 도구 또는 전체 MCP 서버를 선택 해제하세요.
- `github.copilot.chat.virtualTools.threshold` 설정을 사용해 대규모 도구 집합을 관리할 수도 있습니다.

### 에이전트가 내 설정한 기본 터미널 셸을 사용하지 않는 이유는?

- Windows에서는 `cmd`, macOS/Linux에서는 `sh`는 셸 통합을 완전히 지원하지 않기 때문입니다.
- PowerShell(Windows) 또는 `bash`/`zsh`(macOS/Linux)를 사용하는 것이 더 나은 경험을 제공합니다.
- 필요한 경우 `chat.tools.terminal.terminalProfile.windows`, `chat.tools.terminal.terminalProfile.osx`, `chat.tools.terminal.terminalProfile.linux` 설정으로 셸을 재정의할 수 있습니다.

### 모든 도구와 터미널 명령을 자동 승인할 수 있나요?

- 세션 권한 수준에서 `Bypass Approvals` 또는 `Autopilot`을 선택할 수 있습니다.
- `chat.tools.global.autoApprove`를 활성화하면 모든 워크스페이스에 걸쳐 도구 자동 승인을 적용할 수 있습니다.
- `/yolo` 또는 `/autoApprove` 명령으로 채팅에서 직접 활성화할 수 있습니다.
- 그러나 이러한 옵션은 보안 위험이 커지므로 주의해서 사용해야 합니다.

### 도구와 채팅 참가자의 차이는 무엇인가요?

- 채팅 참가자는 도메인별 전문 도우미 역할을 합니다.
- 도구는 에이전트 흐름의 일부로 호출되어 특정 작업을 수행합니다.
- 하나의 채팅 요청에는 여러 도구를 포함할 수 있지만, 채팅 참가자는 한 번에 하나만 활성화됩니다.

### 나만의 도구를 만들 수 있나요?

- 예, VS Code 확장 기능으로 `Language Model Tools API`를 사용해 도구를 만들 수 있습니다.
- 또는 MCP 서버를 작성하여 도구를 제공할 수 있습니다.

## 관련 리소스

- Chat tools reference: https://code.visualstudio.com/docs/copilot/reference/copilot-vscode-features#_chat-tools
- 에이전트 후크: https://code.visualstudio.com/docs/copilot/customization/hooks
- AI 사용 보안 고려 사항: https://code.visualstudio.com/docs/copilot/security
