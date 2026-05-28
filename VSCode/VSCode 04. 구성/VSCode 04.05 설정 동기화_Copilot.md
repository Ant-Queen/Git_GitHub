# VS Code Settings Sync 정리

Visual Studio Code의 Settings Sync 페이지(`https://code.visualstudio.com/docs/configure/settings-sync`)를 한국어로 요약한 문서입니다.

## 개요

Settings Sync는 사용자 설정, 키보드 단축키, 사용자 스니펫, 사용자 작업, UI 상태, 확장, 프로필 등을 여러 기기에서 동기화할 수 있는 기능입니다. 동기화는 백그라운드에서 자동으로 수행됩니다.

> 원격 창(SSH, 컨테이너, WSL)에서는 확장을 동기화하지 않습니다.

## Settings Sync 켜기

- `Manage` 기어 메뉴 또는 활동 표시줄의 `Accounts` 메뉴에서 `Backup and Sync Settings...`를 선택합니다.
- 동기화할 항목을 선택하고 로그인합니다.
- 로그인 방식:
  - Microsoft 계정 (Outlook, Azure 등)
  - GitHub 계정
- Microsoft 계정으로 로그인할 경우 GitHub 계정을 새로 연결하거나 기존 계정과 연결할 수 있습니다.
- 로그인 후 자동으로 동기화가 활성화됩니다.

## 병합(Merge) 또는 로컬 덮어쓰기(Replace)

다른 기기에서 이미 동기화된 상태에서 새 기기에서 설정 동기화를 켜면 다음 옵션이 표시됩니다.

- Merge: 로컬 설정과 클라우드 설정을 병합합니다.
- Replace Local: 원격(클라우드) 설정으로 로컬 설정을 덮어씁니다.
- Merge Manually...: 병합 뷰를 열어 항목별로 수동 병합할 수 있습니다.

## 동기화할 데이터 구성

- 기본적으로 `machine` 또는 `machine-overridable` 스코프를 가지는 머신별 설정은 동기화되지 않습니다.
- `settingsSync.ignoredSettings`를 통해 동기화에서 제외할 설정을 추가하거나 제거할 수 있습니다.
- 기본적으로 키보드 단축키는 플랫폼별로 동기화됩니다.
- 플랫폼에 영향받지 않는 단축키는 `settingsSync.keybindingsPerPlatform`을 비활성화하여 동기화할 수 있습니다.
- 설치된 확장은 글로벌 사용 상태와 함께 동기화됩니다.
- 특정 확장을 제외하려면 확장 보기 또는 `settingsSync.ignoredExtensions` 설정을 사용합니다.

### 동기화되는 UI 상태

- 표시 언어(Display Language)
- 활동 표시줄 항목(Activity Bar entries)
- 패널 항목(Panel entries)
- 보기 레이아웃과 가시성(Views layout and visibility)
- 최근 사용 명령(Recently used commands)
- 다시 표시하지 않기 알림(Do not show again notifications)

- 동기화 구성 변경 방법:
  - 명령 팔레트에서 `Settings Sync: Configure`
  - `Manage` 기어 메뉴에서 `Settings Sync is On` 선택 후 `Settings Sync: Configure`

## 충돌 처리

동기화 중 충돌이 발생하면 다음 옵션이 제공됩니다.

- Accept Local: 로컬 설정으로 클라우드 설정을 덮어씁니다.
- Accept Remote: 원격 설정으로 로컬 설정을 덮어씁니다.
- Show Conflicts: 로컬과 원격의 차이를 비교하는 diff 편집기를 열고 수동으로 해결합니다.

## 계정 전환

- 다른 계정으로 동기화하려면 Settings Sync를 끈 후 다른 계정으로 다시 켜면 됩니다.
- 동기화 끄기 명령: `Settings Sync: Turn off`

## Stable과 Insiders 동기화

- 기본적으로 Stable과 Insiders는 서로 다른 Settings Sync 서비스를 사용하므로 설정을 공유하지 않습니다.
- Insiders에서 Stable 동기화 서비스를 선택하면 두 빌드 간 동기화를 할 수 있습니다.
- 그러나 Insiders가 Stable보다 최신 버전이므로 버전 차이로 인해 데이터 호환성 문제가 생길 수 있습니다.
- 이 경우 Stable에서 동기화가 자동으로 비활성화되고, Stable이 새 버전으로 업데이트된 후 다시 켜야 합니다.

## 데이터 복원

- VS Code는 동기화 중에 로컬 및 원격 백업을 보관합니다.
- 복원 뷰를 열려면 명령 팔레트에서 `Settings Sync: Show Synced Data`를 실행합니다.
- 로컬 Sync 활동 뷰는 기본적으로 숨겨져 있으며, Settings Sync 뷰 오버플로우 메뉴에서 활성화할 수 있습니다.
- 로컬 백업 폴더 열기 명령: `Settings Sync: Open Local Backups Folder`
- 백업 폴더는 preference 타입별로 정리되며, 각 JSON 파일은 타임스탬프가 붙은 이름으로 저장됩니다.

> 로컬 백업은 30일 후 자동 삭제됩니다.
> 원격 백업은 각 리소스별로 최신 20개 버전을 유지합니다.

## 동기화된 기기

- VS Code는 동기화를 수행하는 기기를 추적합니다.
- 각 기기는 기본적으로 빌드 유형(Stable/Insiders)과 플랫폼 기반 이름을 가집니다.
- 기기 이름은 편집할 수 있으며, Settings Sync 뷰에서 다른 기기의 동기화를 끌 수 있습니다.
- 기기 정보는 `Settings Sync: Show Synced Data` 명령으로 확인합니다.

## 확장 기능 개발자를 위한 안내

- 확장 기능은 Settings Sync가 켜졌을 때 적절히 동작해야 합니다.
- 동일한 알림을 여러 기기에 중복으로 표시하거나 환영 페이지를 반복해서 보이지 않도록 주의해야 합니다.
- 확장이 사용자 상태를 동기화해야 한다면 `vscode.ExtensionContext.globalState.setKeysForSync`를 사용해야 합니다.
- `setKeysForSync` 사용 예제는 VS Code 확장 기능 문서의 Extension Capabilities 항목에 나와 있습니다.

## 문제 신고

- Settings Sync 문제는 `Log (Settings Sync)` 출력 뷰에서 확인할 수 있습니다.
- 인증 문제가 있는 경우 `Account` 출력 뷰 로그도 함께 첨부하여 이슈를 생성합니다.

## 데이터 삭제

- 서버에 저장된 모든 데이터를 삭제하려면 Settings Sync를 끄고 클라우드 데이터 삭제 체크박스를 선택합니다.
- 다시 활성화하면 처음 로그인하는 것과 동일한 상태로 설정됩니다.

## FAQ

### VS Code Settings Sync는 Shan Khan의 Settings Sync 확장과 같은 것인가요?

- 아니요. VS Code 내장 Settings Sync는 별도의 기능이며, Shan Khan의 `Settings Sync` 확장은 GitHub Gist를 사용하는 서드파티 확장입니다.

### 어떤 계정으로 로그인할 수 있나요?

- Microsoft 계정 (Outlook 또는 Azure)
- GitHub 계정
- GitHub Enterprise 계정은 지원되지 않습니다.
- Microsoft Sovereign Cloud 계정도 현재 지원되지 않습니다.

### 다른 백엔드 또는 서비스를 사용할 수 있나요?

- 현재 Settings Sync는 전용 서비스를 사용합니다.
- 향후 사용자 지정 백엔드를 지원하는 API가 제공될 가능성이 있습니다.

### Stable과 Insiders 간에 설정을 공유할 수 있나요?

- 예. Stable과 Insiders는 기본적으로 다른 서비스에 동기화되지만, Insiders에서 Stable 동기화 서비스를 선택하면 공유할 수 있습니다.
- 단, 버전 차이로 호환성 문제가 발생할 수 있으며, Stable에서 동기화가 자동으로 비활성화될 수 있습니다.

## 다음 단계

- 사용자 및 워크스페이스 설정에 대한 자세한 내용은 `https://code.visualstudio.com/docs/configure/settings` 문서를 참고하세요.
