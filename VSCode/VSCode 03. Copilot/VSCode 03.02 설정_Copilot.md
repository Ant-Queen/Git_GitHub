# VS Code Copilot 설정 정리

## Copilot 시작하기

1. 상태 표시줄의 Copilot 아이콘 위에 마우스를 올리고 `Use AI Features`를 선택합니다.
2. 로그인 방법을 선택하고 안내에 따라 로그인합니다.
3. 설정이 완료되면 Copilot을 사용할 수 있습니다.

- 이미 Copilot 구독이 있는 계정은 해당 구독을 사용합니다.
- 구독이 없는 경우 Copilot Free 플랜에 가입되어 월간 인라인 제안 및 AI 크레딧을 받습니다.

> 2026년 4월 20일 이후, Copilot Pro/Pro+/Max/Student 플랜 신규 가입은 일시 중지될 수 있습니다.

## 프로젝트를 AI에 맞추기

- 채팅 세션에서 `/init`을 입력하면 코드베이스를 분석하고 AI가 코드 관행을 이해하도록 커스텀 인스트럭션을 생성합니다.

## Copilot과 텔레메트리

- 무료 Copilot 버전에서는 텔레메트리가 기본적으로 활성화되어 있습니다.
- VS Code 설정에서 `telemetry.telemetryLevel`을 `off`로 설정하면 텔레메트리 수집을 비활성화할 수 있습니다.
- Copilot 설정에서 텔레메트리와 코드 제안 옵션을 조정할 수도 있습니다.

## GHE 계정으로 Copilot 사용하기

GitHub Enterprise(GHE) 계정으로 Copilot 구독을 사용하는 경우 다음 절차를 따릅니다.

1. 상태 표시줄의 Copilot 아이콘 위에 마우스를 올리고 `Use AI Features`를 선택합니다.
2. 로그인 창에서 `Continue with GHE.com`을 선택합니다.
3. GHE 인스턴스 URL과 자격 증명을 입력합니다.

## 다른 GitHub 계정으로 Copilot 사용하기

다른 GitHub 계정으로 Copilot에 로그인하려면 다음 방법 중 하나를 사용합니다.

1. 활동 표시줄의 계정 메뉴에서 현재 로그인된 계정 옆의 `Sign out`을 선택합니다.
2. Copilot 메뉴에서 `Sign in to use Copilot`을 선택합니다.
3. 활동 표시줄의 계정 메뉴에서 `Sign in with GitHub`를 선택합니다.
4. 명령 팔레트(`Ctrl+Shift+P`)에서 `GitHub Copilot: Sign in` 명령을 실행합니다.

## 워크스페이스 또는 프로필별로 다른 GitHub 계정 사용

워크스페이스 또는 프로필마다 서로 다른 GitHub 계정으로 Copilot을 사용할 수 있습니다.

### GitHub.com 계정의 경우

1. 활동 표시줄의 계정 메뉴에서 `Manage Extension Account Preferences`를 선택합니다.
2. 목록에서 `GitHub Copilot Chat`을 찾습니다.
3. 현재 워크스페이스와 프로필에서 사용할 GitHub 계정을 선택합니다.

### GHE 계정의 경우

1. 명령 팔레트(`Ctrl+Shift+P`)에서 `Preferences: Open User Settings (JSON)` 또는 `Preferences: Open Workspace Settings (JSON)`을 엽니다.
2. 다음 설정을 추가하여 Copilot 인증 공급자를 GitHub Enterprise로 지정합니다.
```json
"github.copilot.advanced": {
    "authProvider": "github-enterprise"
}
```
3. 아직 로그인하지 않은 경우 GitHub Enterprise 계정으로 다시 로그인합니다.

## VS Code에서 AI 기능 제거하기

- `chat.disableAIFeatures` 설정을 사용하면 VS Code에서 기본 제공 AI 기능을 비활성화하고 숨길 수 있습니다.
- 이 설정은 워크스페이스 또는 사용자 수준에서 구성할 수 있습니다.
- Chat 메뉴의 `Learn How to Hide AI Features`를 선택하면 해당 설정으로 빠르게 이동할 수 있습니다.

> 이전에 AI 기능을 비활성화한 경우 VS Code 업데이트 후에도 해당 선택은 유지됩니다.

## 특정 워크스페이스에서 AI 기능 비활성화

- 워크스페이스 설정(`settings.json`)에서 `chat.disableAIFeatures`를 `true`로 설정합니다.
- 설정 편집기(`Ctrl+,`)에서도 이 옵션을 검색하여 비활성화할 수 있습니다.

## 다음 단계

- 기본 AI 사용법을 알아보려면 [Copilot Quickstart](https://code.visualstudio.com/docs/copilot/getting-started)를 참고합니다.
