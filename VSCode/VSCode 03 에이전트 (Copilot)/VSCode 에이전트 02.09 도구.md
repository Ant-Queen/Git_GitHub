# VS Code 에이전트 도구 사용하기

VS Code의 에이전트는 검색, 명령 실행, 웹 가져오기, API 호출 등 특정 작업을 수행하기 위해 도구를 사용할 수 있습니다. 도구는 세 가지 유형으로 나뉩니다: 내장 도구, MCP 도구, 확장 도구.

도구 유형과 에이전트 루프에서 도구가 어떻게 작동하는지 자세히 보려면 [Tools concepts](https://code.visualstudio.com/docs/agents/concepts/tools)를 참조하세요.

이 문서는 채팅에서 도구를 활성화하고, 프롬프트에서 도구를 사용하는 방법, 도구 호출 승인 및 터미널 명령 관리 방법을 설명합니다.

## 채팅에서 도구 활성화하기

도구를 사용하려면 먼저 채팅 보기에서 활성화해야 합니다. 요청별로 도구 선택기를 사용하여 도구를 활성화하거나 비활성화할 수 있습니다. 추가 도구는 [MCP 서버](https://code.visualstudio.com/docs/agent-customization/mcp-servers) 또는 도구를 제공하는 [확장](https://code.visualstudio.com/docs/configure/extensions/extensions)을 설치하여 추가할 수 있습니다.

> Tip: 프롬프트와 관련된 도구만 선택하면 결과가 더 좋아집니다.

도구 선택기 사용 방법:

1. 채팅 보기를 열고 에이전트 선택기에서 `Agent`를 선택합니다.
2. 채팅 입력 필드에서 `Configure Tools` 버튼을 선택합니다.
3. 현재 요청에 사용할 도구를 선택하거나 선택 해제합니다.

검색 상자를 사용해 도구 목록을 필터링할 수 있습니다.


## 프롬프트에서 도구 사용하기

에이전트를 사용할 때 에이전트는 프롬프트와 요청 컨텍스트를 기반으로 활성화된 도구 중에서 적절한 도구를 자동으로 선택합니다.

특정 도구를 반드시 사용하도록 하려면 프롬프트에 `#` 뒤에 도구 이름을 명시적으로 입력할 수 있습니다. 예를 들어:

- `What is the latest version of Node.js #web`
- `How does routing work in Next.js? #web`
- `Fix the issues in #problems`
- `Explain the authentication flow #codebase`

`#`를 입력하면 사용 가능한 도구 목록이 표시됩니다. 여기에는 내장 도구, 설치된 MCP 서버의 도구, 확장 도구, 도구 집합이 포함됩니다.

> Tip: 기본적으로 채팅에서 도구 호출 세부 정보는 접혀 있습니다. 채팅에서 도구 요약 줄을 선택하여 펼치거나, `chat.agent.thinking.collapsedTools` 설정으로 기본 동작을 변경할 수 있습니다(실험적).


## 권한 수준

채팅 보기의 권한 선택기는 세션 중 에이전트가 얼마나 자율적으로 행동할지를 제어합니다. 권한 수준은 도구 호출 및 승인 처리 방식에 영향을 줍니다.

- `Default Approvals`: 구성된 승인 설정을 사용합니다. 승인이 필요한 도구는 실행 전에 확인 대화 상자를 표시합니다. 필요한 경우 에이전트가 명확화 질문을 할 수 있습니다.
- `Bypass Approvals`: 모든 도구 호출을 자동으로 승인하고 오류가 발생하면 자동으로 재시도합니다. 필요한 경우 명확화 질문이 있을 수 있습니다.
- `Autopilot (Preview)`: 모든 도구 호출을 자동으로 승인하고 명확화 질문에 자동 응답합니다. 에이전트는 작업이 완료될 때까지 자율적으로 계속 작업합니다.

> 주의: `Bypass Approvals`와 `Autopilot`은 파일 편집, 터미널 명령, 외부 도구 호출과 같은 잠재적으로 파괴적인 작업에 대한 수동 승인 프롬프트를 우회합니다. 첫 사용 시 경고 대화 상자가 표시됩니다. 보안 영향을 이해한 후 사용하세요.

현재 채팅 세션에만 권한 수준이 적용됩니다. 세션 중 언제든지 권한 선택기에서 다른 수준을 선택하여 변경할 수 있습니다. 에이전트를 중지하려면 중지 버튼을 선택하세요.

기본적으로 새 채팅 세션은 `Default Approvals` 수준으로 시작합니다. 선호하는 권한 수준을 세션 간에 유지하려면 `chat.permissions.default` 설정을 구성하세요.


## 도구 승인

일부 도구는 실행 전에 사용자의 승인을 필요로 합니다. 도구가 파일을 수정하거나 환경을 변경하거나 악의적 도구 출력으로 프롬프트 주입 공격을 시도할 수 있기 때문입니다.

도구 승인을 관리하려면 명령 팔레트(`Ctrl+Shift+P`)에서 `Chat: Manage Tool Approval`을 실행합니다. 퀵 픽에는 MCP 서버 또는 확장 출처별로 그룹된 모든 도구가 표시됩니다.

각 도구에 대해 다음 두 가지 승인 유형을 구성할 수 있습니다:

- 사전 승인(`without approval`): 도구가 실행되기 전에 확인 대화 상자를 건너뜁니다.
- 사후 승인(`without reviewing result`): 외부 데이터를 반환하는 도구의 결과를 채팅 컨텍스트에 추가하기 전에 검토를 건너뜁니다.

출처를 확장하여 개별 도구 승인을 구성하거나 특정 MCP 서버 또는 확장에 대한 모든 도구를 한 번에 신뢰하도록 최상위 확인란을 선택할 수 있습니다.


### 도구 자동 승인(실험적) 사용 또는 해제

기본적으로 자동 승인을 선택할 수 있습니다. 특정 도구에 대해 자동 승인을 방지하려면 조직 수준에서 관리되는 `chat.tools.eligibleForAutoApproval` 설정을 `false`로 설정합니다. 관리자는 이 설정을 변경할 수 있습니다.

조직 문서에서 자세한 내용을 확인하세요: [Enterprise documentation](https://code.visualstudio.com/docs/enterprise/ai-settings).


### URL 승인

도구가 `#web/fetch`와 같은 URL에 액세스하려고 할 때는 악의적이거나 예상치 못한 콘텐츠로부터 보호하기 위해 2단계 승인 프로세스가 사용됩니다. VS Code는 URL 세부 정보가 포함된 확인 대화 상자를 표시합니다.

승인 옵션:

- 일회성 승인
- 특정 URL 또는 도메인에 대한 향후 자동 승인

자동 승인을 선택해도 결과 검토 필요성에는 영향을 주지 않습니다. `Allow requests to`를 선택하면 URL 또는 도메인에 대해 사전 승인과 사후 승인을 모두 구성할 수 있습니다.

> 참고: 이 사전 승인 단계는 `Trusted Domains` 기능을 준수합니다. 신뢰할 수 있는 도메인이 나열된 경우 해당 도메인에 대한 요청은 자동으로 승인되고 응답 검토 단계는 연기됩니다.

사후 승인:

- URL에서 가져온 콘텐츠를 채팅이나 다른 도구로 전달하기 전에 검토합니다.
- 사용자 생성 콘텐츠가 포함된 사이트에서 요청을 승인할 때 발생할 수 있는 프롬프트 주입 위험을 줄입니다.

사후 승인 단계는 `Trusted Domains` 기능과 연결되어 있지 않으며 항상 검토가 필요합니다.

`chat.tools.urls.autoApprove` 설정은 자동 승인 URL 패턴을 저장하는 데 사용됩니다. 값은 요청 및 응답 모두에 대한 자동 승인을 활성화하거나 비활성화하는 부울이거나, `approveRequest`, `approveResponse` 속성을 포함하는 객체일 수 있습니다.

URL 자동 승인 예시:

```jsonc
{
  "chat.tools.urls.autoApprove": {
    "https://www.example.com": false,
    "https://*.contoso.com/*": true,
    "https://example.com/api/*": {
      "approveRequest": true,
      "approveResponse": false
    }
  }
}
```


### 도구 확인 초기화

저장된 모든 도구 승인을 지우려면 명령 팔레트에서 `Chat: Reset Tool Confirmations`를 실행합니다.

개별 도구 승인을 선택적으로 검토하고 변경하려면 `Chat: Manage Tool Approval` 명령을 사용하세요.


## 도구 매개변수 편집

도구가 실행되기 전에 입력 매개변수를 검토하고 편집할 수 있습니다.

1. 도구 확인 대화 상자가 나타나면 도구 이름 옆의 화살표를 선택하여 세부 정보를 확장합니다.
2. 필요한 경우 도구 입력 매개변수를 편집합니다.
3. `Allow`를 선택하여 수정된 매개변수로 도구를 실행합니다.


## 터미널 명령

에이전트는 작업을 수행하는 과정에서 빌트인 터미널 도구를 사용해 통합 터미널에서 명령을 실행할 수 있습니다. 채팅 대화에서 실행한 명령을 표시하며, 명령 옆의 `Show Output (>)`을 선택하면 채팅에서 출력 내용을 볼 수 있습니다. `Show Terminal`을 선택하면 통합 터미널에서 전체 출력을 확인할 수 있습니다.

`chat.tools.terminal.outputLocation` 실험적 설정을 사용하여 터미널 명령 출력이 채팅 내에 표시될지 통합 터미널에 표시될지 구성할 수 있습니다.

터미널 창에서는 채팅 세션에서 에이전트가 사용한 터미널 목록을 확인할 수 있습니다. 에이전트 터미널은 터미널 목록에서 채팅 아이콘으로 구분됩니다.


### 백그라운드에서 터미널 명령 계속 실행

에이전트가 개발 서버 시작 또는 감시 모드 빌드와 같이 장시간 실행되는 터미널 명령을 실행할 때, 명령을 백그라운드로 보내 계속 실행하도록 할 수 있습니다. 이렇게 하면 에이전트가 명령이 끝날 때까지 기다리지 않고 다른 작업을 계속할 수 있습니다.

명령이 실행되는 동안 채팅 대화에 `Continue in Background` 버튼이 나타납니다. 이 버튼을 선택하면 명령이 백그라운드에서 계속 실행됩니다. 에이전트는 이후 출력 내용을 확인하거나 다른 작업을 위해 터미널을 사용할 수 있습니다.

에이전트는 터미널 명령 실행 시 타임아웃을 지정할 수도 있습니다. 타임아웃이 도달하면 에이전트는 명령 대기 상태를 중단하고 그때까지 수집된 출력을 반환합니다. `chat.tools.terminal.enforceTimeoutFromModel` 설정을 사용하여 모델이 지정한 타임아웃 값을 강제할지 제어할 수 있습니다.

백그라운드에서 표시되지 않은 터미널은 명령이 완료되면 자동으로 정리되어 장기간 세션 중에 터미널이 누적되는 것을 방지합니다. 명령이 완료된 후에도 터미널을 표시하고 유지하려면 도구 호출 헤더의 `Show` 링크를 선택하세요.


### 터미널 명령 자동 승인

`chat.tools.terminal.autoApprove` 설정을 사용하여 자동으로 승인할 터미널 명령을 구성할 수 있습니다. 승인할 명령과 거부할 명령을 지정할 수 있습니다:

- `true`로 설정하면 자동 승인
- `false`로 설정하면 항상 승인을 요구
- `/.../`로 감싼 정규식 사용 가능

예시:

```jsonc
{
  "mkdir": true,
  "/^git (status|show\b.*)$/": true,
  "del": false,
  "/dangerous/": false
}
```

기본적으로 패턴은 개별 하위 명령과 비교합니다. 명령이 자동 승인되려면 모든 하위 명령이 `true` 항목과 일치해야 하고 `false` 항목과 일치하지 않아야 합니다.

고급 시나리오에서는 `matchCommandLine` 속성을 사용해 전체 명령줄과 비교할 수 있습니다.

관련 설정:

- `chat.tools.terminal.enableAutoApprove`: 조직 수준에서 관리되는 설정으로 자동 승인 기능을 영구적으로 비활성화합니다.
- `chat.tools.terminal.blockDetectedFileWrites`(실험적): `outsideWorkspace`(기본값)로 설정하면 워크스페이스 외부에 파일을 쓰는 터미널 명령에 대해 승인을 요구합니다. OS 임시 폴더(`%TEMP%` 등)는 세션 수준 명령 승인 활성 시 예외입니다.
- `chat.tools.terminal.ignoreDefaultAutoApproveRules`(실험적): 모든 기본 규칙(허용 및 차단)을 비활성화하여 규칙을 완전히 제어합니다.

> 주의: 터미널 명령 자동 승인은 최선의 보호를 제공합니다. 에이전트가 악의적으로 동작하지 않는다는 전제하에 동작하므로 프롬프트 주입 위험이 있는 경우 주의해야 합니다.

자동 승인에는 탐지가 실패할 수 있는 한계가 있으며, 다음과 같은 경우 명령이 감지되지 않을 수 있습니다:

- PowerShell 및 bash 트리시터 문법이 하위 명령을 감지하지 못하는 경우
- zsh 또는 fish 문법이 없어서 bash 문법을 사용하는 경우
- 파일 쓰기 감지가 최소한으로 구현되어 있어 터미널로 파일을 쓰는 동작을 완전히 탐지하지 못할 수 있는 경우
- 인용부호 연결 등의 기법으로 자동 승인을 우회하는 경우

프롬프트 주입이 가능하거나 고위험 환경에 있는 경우 에이전트 샌드박싱을 활성화하거나 컨테이너 내에서 VS Code를 실행하는 것을 고려하세요.


## 에이전트 샌드박싱 명령

### 파일 시스템 액세스 구성

`chat.agent.sandbox.FileSystem.linux` 또는 `chat.agent.sandbox.FileSystem.mac` 설정을 사용하여 파일 시스템 액세스를 제어할 수 있습니다. 읽기 및 쓰기 허용 규칙과 거부 규칙을 지정할 수 있으며, glob 패턴은 지원되지 않습니다. `denyWrite` 및 `denyRead` 규칙은 `allowWrite` 및 `allowRead`보다 우선합니다.

작업공간 폴더, 샌드박스 런타임 임시 폴더 및 VS Code가 자동으로 추가하는 명령별 읽기 경로는 자동으로 허용됩니다. 따라서 일반적으로 워크스페이스 외부의 도구 구성이나 데이터를 허용하려면 `allowRead`만 추가하면 됩니다.

예시:

```jsonc
{
  "chat.agent.sandbox.FileSystem.mac": {
    "allowWrite": ["."],
    "allowRead": ["/Users/me/.config/myapp"],
    "denyWrite": ["./secrets/"],
    "denyRead": ["/etc/passwd"]
  }
}
```


### 네트워크 액세스 구성

에이전트 도구(`fetch` 도구, 통합 브라우저 등)가 액세스할 수 있는 도메인을 제한하려면 조직 수준에서 관리되는 `chat.agent.networkFilter` 설정을 활성화합니다. 또한 `chat.agent.allowedNetworkDomains` 및 `chat.agent.deniedNetworkDomains` 설정을 사용하여 허용/거부 도메인을 구성할 수 있습니다. 두 목록이 모두 비어 있으면 모든 도메인이 차단됩니다.

거부 도메인은 항상 허용 도메인보다 우선합니다. 두 설정 모두 `*.example.com`과 같은 와일드카드를 지원합니다.

샌드박싱이 활성화되고 `chat.agent.sandbox.retryWithAllowNetworkRequests`가 기본값으로 설정된 경우, 네트워크 제한으로 차단된 명령은 제한되지 않은 네트워크 액세스와 함께 다시 시도할지 확인합니다. 이 설정을 비활성화하면 명령을 샌드박스 외부에서 실행하는 확인으로 대체합니다. 이 동작은 `chat.agent.sandbox.allowUnsandboxedCommands` 설정으로 제어됩니다.

예시:

```jsonc
{
  "chat.agent.networkFilter": true,
  "chat.agent.allowedNetworkDomains": [
    "api.github.com"
  ],
  "chat.agent.deniedNetworkDomains": [
    "example.com"]
}
```


### 에이전트 샌드박싱 개요

에이전트 샌드박싱은 현재 미리보기 상태이며 향후 변경될 수 있습니다.

자세한 내용은 [Agent sandboxing](https://code.visualstudio.com/docs/agents/concepts/trust-and-safety#_agent-sandboxing)를 참조하세요.

에이전트 샌드박싱은 명령 실행 시 파일 시스템과 네트워크 액세스를 제한합니다. 샌드박싱이 활성화된 경우 터미널 명령은 제어된 환경에서 실행되므로 추가 사용자 확인 없이 자동 승인됩니다.

- `off`(기본): 샌드박싱 비활성화
- `on`: 파일 시스템 및 네트워크 격리 포함 전체 샌드박싱. 명시적으로 허용된 도메인 외에는 모든 아웃바운드 네트워크 액세스 차단
- `allowNetwork`: 파일 시스템 격리만 적용. 네트워크는 제한되지 않음

샌드박싱이 `on` 또는 `allowNetwork`인 경우:

- 파일 시스템 액세스 제한 시:
  - 워크스페이스 폴더, 샌드박스 런타임 임시 폴더 및 VS Code가 자동으로 추가한 경로는 읽기 허용
  - 홈 디렉터리(`$HOME`)에서의 읽기 기본 거부
  - 현재 작업 디렉터리와 하위 디렉터리에 대한 쓰기 허용
  - 명령은 사용자 확인 없이 실행
- 네트워크 액세스 제한 시:
  - 명시적으로 허용된 도메인 외엔 모든 아웃바운드 네트워크 액세스 차단

필수 OS 종속성이 설치되지 않은 경우 VS Code는 필요한 구성 요소 설치를 제안합니다. 설치를 선택하지 않으면 샌드박싱이 활성화되지 않습니다.


## 도구 세트로 도구 그룹화하기

도구 세트를 사용하면 관련 도구를 하나의 단위로 묶어 프롬프트에서 참조하기 쉽습니다.

### 도구 세트 생성

도구 세트를 생성하려면:

1. 명령 팔레트에서 `Chat: Configure Tool Sets` 명령을 실행하고 `Create new tool sets file`을 선택합니다.
   - 또는 채팅 보기의 줄임표(`...`) 메뉴에서 `Tool Sets`를 선택한 후 `Create new tool sets file`을 선택합니다.
2. 열리는 `.jsonc` 파일에 도구 세트를 정의합니다.

도구 세트 예시:

```jsonc
{
  "reader": {
    "tools": ["search/changes", "search/codebase", "read/problems", "search/usages"],
    "description": "Tools for reading and gathering context",
    "icon": "book"
  }
}
```

도구 세트 속성:

- `tools`: 도구 이름 배열(내장 도구, MCP 도구, 확장 도구)
- `description`: 도구 선택기에 표시되는 간단한 설명
- `icon`: 도구 세트 아이콘([Product Icon Reference](https://code.visualstudio.com/api/references/icons-in-labels))


### 도구 세트 사용하기

프롬프트에서 도구 세트를 참조하려면 `#` 뒤에 도구 세트 이름을 입력합니다. 예:

- `Analyze the codebase for security issues #reader`
- `Where is the DB connection string defined? #search`

도구 선택기에서 도구 세트는 관련 도구의 접이식 그룹으로 표시됩니다. 전체 도구 세트를 한 번에 선택하거나 해제할 수 있습니다.

도구 세트는 프롬프트 파일, 맞춤 채팅 에이전트, 채팅 프롬프트에서 모두 사용할 수 있습니다. 내장 도구 중 일부는 `#edit`, `#search`와 같은 미리 정의된 도구 세트의 일부입니다.


## 자주 묻는 질문

### 어떤 도구를 사용할 수 있는지 어떻게 알 수 있나요?

채팅 입력 필드에 `#`를 입력하면 사용 가능한 도구 목록이 표시됩니다. 채팅에서 도구 선택기를 사용하여 활성 도구 목록을 확인하고 관리할 수도 있습니다.

### "Cannot have more than 128 tools per request." 오류가 발생하는 이유는?

한 채팅 요청에 최대 128개의 도구를 활성화할 수 있습니다. 이 오류가 발생하면 채팅 보기의 도구 선택기에서 일부 도구 또는 전체 MCP 서버를 선택 해제하여 도구 수를 줄이세요.

또는 `github.copilot.chat.virtualTools.threshold` 설정을 사용해 큰 도구 세트를 자동으로 관리하도록 설정할 수 있습니다.

### 에이전트가 구성된 터미널 셸을 사용하지 않는 이유는 무엇인가요?

에이전트는 터미널에 대해 기본으로 구성된 셸을 사용하지만, Windows의 `cmd`와 macOS/Linux의 `sh`는 쉘 통합을 지원하지 않기 때문에 예외입니다. 이러한 셸은 터미널에서 명령이 실행 중인지 또는 완료되었는지를 직접 감지할 수 없는 경우가 많아, 에이전트 경험이 느리고 불안정해질 수 있습니다.

PowerShell(Windows) 또는 bash/zsh(macOS/Linux)을 사용하는 것이 더 나은 환경입니다. 그래도 `chat.tools.terminal.terminalProfile.windows`, `chat.tools.terminal.terminalProfile.osx`, `chat.tools.terminal.terminalProfile.linux` 설정을 사용하여 셸을 재정의할 수 있습니다.

### 모든 도구와 터미널 명령을 자동 승인할 수 있나요?

예, 여러 옵션이 있습니다:

- 권한 수준: 현재 세션에서 `Bypass Approvals` 또는 `Autopilot` 권한 수준을 선택하여 모든 도구를 자동 승인합니다.
- 전역 설정: 조직 수준에서 관리되는 `chat.tools.global.autoApprove`를 활성화하여 모든 워크스페이스에서 모든 도구를 자동 승인합니다.

이 옵션을 처음 활성화하면 경고 대화 상자가 표시됩니다.

> 주의: 수동 승인 프롬프트를 비활성화하면 잠재적으로 파괴적인 동작에 대한 보안 보호가 사라집니다. 위험을 이해하는 경우에만 사용하세요.

`chat.tools.global.autoApprove` 설정은 모든 워크스페이스에 전역적으로 적용됩니다. 현재 세션에만 자동 승인을 적용하려면 세션 범위 권한 수준을 사용하세요.

### 도구와 채팅 참여자(chat participants)의 차이는 무엇인가요?

채팅 참여자는 도메인별 질문에 답하는 전문 보조자와 같습니다. 하나의 채팅 요청에서 여러 도구를 포함할 수 있지만, 한 번에 활성화할 수 있는 채팅 참여자는 하나뿐입니다.

도구는 에이전트 흐름의 일부로 호출되어 특정 작업을 수행합니다.

### 나만의 도구를 만들 수 있나요?

네. 도구는 다음 두 가지 방법으로 만들 수 있습니다:

- [Language Model Tools API](https://code.visualstudio.com/api/extension-guides/ai/tools)를 사용하여 도구를 제공하는 VS Code 확장을 개발
- 도구를 제공하는 MCP 서버를 생성. [MCP 개발자 가이드](https://code.visualstudio.com/docs/agents/guides/mcp-developer-guide)를 참조하세요.


## 관련 자료

- [Chat tools reference](https://code.visualstudio.com/docs/agents/reference/copilot-vscode-features#_chat-tools)
- [Agent hooks](https://code.visualstudio.com/docs/agent-customization/hooks) - 도구 수명 주기 이벤트에서 사용자 지정 명령 실행
- [Security considerations for using AI in VS Code](https://code.visualstudio.com/docs/agents/security)

## 도움말 및 지원

- 커뮤니티에 질문하기: https://stackoverflow.com/questions/tagged/vscode
- 기능 요청: https://go.microsoft.com/fwlink/?LinkID=533482
- 문제 보고: https://www.github.com/Microsoft/vscode/issues
