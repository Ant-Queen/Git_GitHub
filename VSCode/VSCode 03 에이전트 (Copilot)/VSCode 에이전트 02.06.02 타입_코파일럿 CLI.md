# Copilot CLI 세션

Visual Studio Code는 GitHub Copilot CLI를 사용해 백그라운드에서 에이전트 세션을 실행할 수 있습니다. VS Code의 통합 채팅 보기에서 Copilot CLI 세션을 시작, 모니터링, 관리할 수 있으며, 에이전트는 로컬 머신에서 자율적으로 실행되어 사용자가 다른 작업을 계속할 수 있습니다.

## Copilot CLI 세션이란?

- Copilot CLI 세션은 로컬 머신에서 백그라운드로 독립 실행됩니다.
- VS Code는 Copilot SDK를 사용하여 세션을 시작, 중지, 진행 상태를 모니터링합니다.
- Copilot CLI는 자동으로 설치 및 구성됩니다.
- 로컬 에이전트와 달리 VS Code 창을 닫아도 세션이 계속 실행됩니다.
- 통합 채팅 보기에서 세션과 상호 작용하며, 입력 요청이나 권한 승인이 필요한 경우 채팅을 통해 처리할 수 있습니다.
- 백그라운드 실행에 적합한 작업: 계획된 구현, 프로토타입 여러 버전 생성, 명확하게 정의된 수정 또는 기능 구현.

## 주요 기능

- `/` 명령어 지원: 재사용 가능한 프롬프트, 에이전트 스킬, 훅, `/compact`, `/research`, `/yolo`, `/autoApprove` 등
- 작업 중간에 계속 입력을 보내거나 권한 승인을 처리할 수 있음
- 여러 Copilot CLI 세션을 병렬로 실행 가능

## 분리 모드(Isolation Modes)

### 워크트리 격리(Worktree isolation)

- Copilot CLI 세션은 Git 워크트리를 별도 폴더에 생성합니다.
- 에이전트가 만든 변경사항은 워크트리에 적용되어 현재 작업 중인 워크스페이스와 분리됩니다.
- 변경사항을 검토하고 적용할 준비가 되었을 때만 병합할 수 있습니다.
- Git 워크트리와 워크트리 격리를 사용하려면 워크스페이스가 Git 저장소여야 합니다.
- 워크트리 격리를 사용하는 세션은 자동으로 `Bypass Approvals` 권한 레벨이 설정되고 변경할 수 없습니다.

### 워크스페이스 격리(Workspace isolation)

- 에이전트가 현재 워크스페이스에서 직접 실행되고 변경사항이 즉시 적용됩니다.
- 로컬 에이전트 세션과 동일하게 `Default Approvals`, `Bypass Approvals`, `Autopilot` 권한 레벨을 선택할 수 있습니다.

## 권한 및 승인

- 워크트리 격리: 모든 도구 호출이 자동 승인되므로 승인 대화상자가 나타나지 않습니다.
- 워크스페이스 격리: 채팅 입력 영역의 권한 선택기에서 세 가지 권한 레벨 중 하나를 선택할 수 있습니다.

## Copilot CLI 세션 생성 방법

1. 채팅 보기(`Ctrl+Alt+I`)를 열고 `Session Target` 드롭다운에서 `Copilot CLI`를 선택합니다.
2. 상단의 새 채팅 아이콘을 선택하고 `New Copilot CLI Session`을 선택합니다.
3. 명령 팔레트(`Ctrl+Shift+P`)에서 `Chat: New Copilot CLI` 명령을 실행합니다.
4. 워크스페이스 또는 워크트리 격리 모드를 선택합니다.
5. 프롬프트를 제출하여 에이전트를 시작합니다.
6. 세션 진행 상태를 채팅 보기에서 확인합니다.

Tip: 워크트리 격리를 사용하는 경우 세션이 끝날 때마다 변경사항을 워크트리에 커밋하여 세션 기록과 커밋 기록을 일치시킵니다.

## 로컬 세션을 Copilot CLI로 넘기기

- 처음에 VS Code 로컬 에이전트로 요구사항을 정리한 뒤 Copilot CLI로 작업을 넘기는 방법이 유용합니다.
- 계획 에이전트(`Plan agent`)로 계획을 만든 후 구현을 Copilot CLI로 계속 실행할 수 있습니다.
- 로컬 에이전트 대화를 Copilot CLI로 넘기면 전체 대화 기록과 컨텍스트가 백그라운드 세션으로 전달됩니다.

### 넘기기 방법

1. 채팅 보기(`Ctrl+Alt+I`)를 엽니다.
2. 로컬 에이전트와 상호작용하여 작업 준비를 완료합니다.
3. `Session Target` 드롭다운에서 `Copilot CLI`를 선택합니다.
4. 계획 에이전트를 사용 중이면 `Start Implementation` 드롭다운에서 `Continue in Copilot CLI`를 선택합니다.

## Copilot CLI 세션 원격 제어

- `/remote on` 명령으로 GitHub.com 또는 GitHub Mobile 앱에서 Copilot CLI 세션을 원격 제어할 수 있습니다.
- 원격 제어를 활성화하면 GitHub 작업 페이지에 세션 기록, 도구 활동, 상태 업데이트가 실시간으로 스트리밍됩니다.
- 세션에서 권한 승인이나 입력이 필요한 경우 GitHub과 VS Code 양쪽에서 처리할 수 있습니다.
- `/remote` 명령은 현재 원격 제어 상태를 표시합니다.
- `/remote off` 명령으로 GitHub 미러링을 중지합니다.
- `github.copilot.chat.cli.remote.enabled` 설정을 비활성화하면 원격 제어 지원을 끌 수 있습니다.

> 원격 제어는 GitHub 인증과 GitHub 리포지토리 매핑이 필요하며, 필요한 추가 권한이 있으면 VS Code가 요청합니다.

## 터미널에서 Copilot CLI 사용하기

### Copilot CLI 터미널 열기

- 터미널 패널에서 `+` 버튼 옆 드롭다운을 클릭하고 `GitHub Copilot CLI`를 선택합니다.
- 명령 팔레트(`Ctrl+Shift+P`)에서 `Chat: New Copilot CLI Session`을 실행하거나 `Chat: New CLI Session to the Side`를 실행합니다.
- `Terminal: Create New Terminal (With Profile)` 명령을 실행하고 `GitHub Copilot CLI`를 선택합니다.
- VS Code 통합 터미널에서 `copilot`을 입력하여 Copilot CLI를 직접 시작할 수 있습니다.

### 지원 셸

- macOS, Linux: bash, zsh
- Windows: PowerShell, 명령 프롬프트(Command Prompt)

### 세션 시작 및 재개

- Copilot CLI 터미널에서 새 세션을 시작하면 VS Code가 세션을 자동으로 감지하여 채팅 보기 세션 목록에 표시합니다.
- 세션을 재개하려면 세션 목록에서 해당 세션을 마우스 오른쪽 클릭하고 `Resume in Terminal`을 선택합니다.
- Copilot CLI 터미널은 인증을 자동으로 처리하므로 별도 로그인은 필요하지 않습니다.

## 다중 리포지토리 워크스페이스

- 워크스페이스에 여러 Git 저장소가 있는 경우, Copilot CLI 세션을 시작할 때 채팅 입력에 리포지토리 선택기가 표시됩니다.
- 세션이 생성되면 선택한 저장소에 워크트리가 생성되며, 소스 제어 보기의 Worktrees 노드에서 확인할 수 있습니다.
- `scm.repositories.explorer` 설정을 활성화하면 워크스페이스의 모든 저장소를 확인할 수 있습니다.

## Copilot CLI에서 커스텀 에이전트 사용하기

- 커스텀 에이전트는 에이전트의 역할이나 페르소나를 정의합니다.
- Copilot CLI 세션 생성 시 커스텀 에이전트를 선택할 수 있습니다.

### 사용 방법

1. `github.copilot.chat.cli.customAgents.enabled` 설정을 활성화합니다.
2. 명령 팔레트(`Ctrl+Shift+P`)에서 `Chat: New Custom Agent`를 사용해 워크스페이스에 커스텀 에이전트를 만듭니다.
3. 새 Copilot CLI 세션을 만들고 `Agents` 드롭다운에서 커스텀 에이전트를 선택합니다.

> 현재 Copilot CLI 세션에서 사용할 수 있는 커스텀 에이전트는 워크스페이스에 정의된 에이전트만 가능합니다.

## 리서치 에이전트로 심층 조사 실행

- 리서치 에이전트는 현재 미리보기 기능이며, Insiders의 Copilot CLI(로컬) 세션에서만 사용할 수 있습니다.
- 코드베이스, 관련 GitHub 리포지토리, 웹에서 정보를 모아 깊이 있는 Markdown 보고서를 작성합니다.
- 읽기 전용 접근 방식으로 동작하며 코드 변경 없이 조사 결과를 제공합니다.
- `/research` 명령어를 사용하여 주제를 조사합니다.

예: `/research How does the authentication flow work in this codebase?`

## Copilot CLI 세션의 제한 사항

- 모든 VS Code 기본 제공 도구에 액세스할 수 있는 것은 아닙니다.
- 확장 제공 도구에는 액세스할 수 없으며, CLI 도구에서 사용 가능한 모델로 제한됩니다.
- 현재 인증이 필요한 로컬 MCP 서버에만 접근할 수 없습니다.

## 관련 자료

- [에이전트 개요](https://code.visualstudio.com/docs/agents/overview)
- [커스텀 에이전트](https://code.visualstudio.com/docs/agent-customization/custom-agents)
- [GitHub Copilot CLI 리서치 문서](https://docs.github.com/en/copilot/concepts/agents/copilot-cli/research)
- [GitHub Copilot CLI 참조 문서](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference)
