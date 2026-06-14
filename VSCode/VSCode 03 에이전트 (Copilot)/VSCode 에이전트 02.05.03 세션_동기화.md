# VS Code 에이전트 세션 동기화

VS Code는 Copilot 채팅 세션을 GitHub 계정과 동기화하여 여러 장치에서 세션 기록에 접근할 수 있도록 합니다. 동기화된 세션은 기본적으로 사용자 개인에게만 공개됩니다.

## 1. 세션 동기화 끄기

세션 데이터를 로컬에만 보관하려면 `chat.sessionSync.enabled` 설정을 `false`로 변경합니다. 이 설정은 조직 수준에서 관리되므로 관리자에게 문의해야 할 수 있습니다.

- 끄면 세션 데이터는 내 기기에만 저장됩니다.
- 클라우드로 업로드되지 않습니다.

## 2. 동기화에서 리포지토리 제외

`chat.sessionSync.excludeRepositories` 설정을 사용하면 특정 리포지토리를 동기화에서 제외할 수 있습니다.

예시:
```json
"chat.sessionSync.excludeRepositories": [
    "my-org/private-repo",
    "my-org/secret-*"
]
```

- 일치하는 리포지토리에 속한 세션은 로컬에만 저장됩니다.

## 3. Enterprise 정책

Copilot Business 및 Copilot Enterprise 사용자에게는 두 가지 정책이 세션 동기화를 제어합니다.

- GitHub.com 기업 정책: "Store local sessions in the Cloud"로 클라우드 동기화 사용 또는 비활성화
- VS Code 그룹 정책(`CopilotSessionSync`): 비활성화되면 `chat.sessionSync.enabled` 설정이 `false`로 강제 적용되어 세션이 로컬에만 저장

중요:
- 정책이 활성화되었다고 해서 관리자가 세션 데이터에 접근할 수 있는 것은 아닙니다.
- 동기화된 세션은 기본적으로 개인 계정에 연결되며, 별도로 공유하지 않으면 다른 사용자가 볼 수 없습니다.
- 정책이 비활성화되면 상태 표시가 `Disabled by policy`로 나타나며 사용자가 변경할 수 없습니다.

## 4. 세션 공유

세션은 기본적으로 공유되지 않습니다. GitHub.com에서 동기화된 세션을 보기 전용으로 공유할 수 있습니다.

1. GitHub.com의 Agents 탭 열기
2. 세션 선택 후 `...` 메뉴에서 `Sharing settings` 선택
3. 공유 활성화하여 저장소 협업자가 보기 전용으로 접근할 수 있게 설정

- 공유 대상자는 프롬프트, 응답, 파일 변경 내용을 볼 수 있음
- 세션을 조작하거나 수정할 수는 없음
- 공유된 세션은 다른 사용자의 세션 검색 인덱스에 포함되지 않음

## 5. 세션 동기화 상태

Copilot 상태 표시줄의 세션 동기화 상태는 다음과 같습니다.

- `Not enabled`: 세션 동기화가 꺼져 있음. 데이터는 로컬에만 저장
- `Enabled`: 세션 동기화가 켜져 있음
- `N sessions synced`: 몇 개의 세션이 업로드되었는지 표시. 선택하면 GitHub.com에서 세션 보기
- `Syncing N sessions`: 업로드 진행 중
- `Disabled by policy`: 조직 정책으로 동기화가 금지됨
- `Sync error`: 마지막 동기화에서 오류 발생. 나중에 다시 시도

## 6. 개인 정보 및 데이터 제어

- 동기화된 세션은 기본적으로 본인만 볼 수 있음
- 세션 데이터는 개인 GitHub 계정에 연결됨
- 토큰, API 키, 자격 증명 등 비밀 정보는 클라우드로 전송되기 전에 자동으로 제거됨
- 언제든지 `chat.sessionSync.enabled`를 `false`로 설정하여 동기화를 중단할 수 있음
- 이미 동기화된 세션은 GitHub.com에서 삭제할 때까지 남아 있음

## 7. 동기화된 세션 삭제

동기화된 세션 데이터를 삭제하려면 명령 팔레트에서 `Delete Session Sync Data`(`github.copilot.sessionSync.deleteSessions`)를 실행합니다.

삭제 시 선택 가능한 범위:

- `Delete from local and cloud`: 로컬과 GitHub.com 모두에서 제거. 되돌릴 수 없음
- `Delete from cloud only`: GitHub.com에서만 삭제하고 로컬 데이터는 유지

또는 GitHub.com의 Agents 탭에서 개별 동기화 세션을 숨기거나 삭제할 수 있습니다.

- 숨기면 세션 인덱스에서 보이지 않게 되고 검색 결과에 나타나지 않음

## 8. 설정 참조

- `github.copilot.chat.localIndex.enabled` (기본값: `true`): 로컬 세션 추적 활성화(동기화 전제 조건)
- `chat.sessionSync.enabled`: 세션을 GitHub 계정으로 동기화
- `chat.sessionSync.excludeRepositories`: 동기화에서 제외할 리포지토리 패턴

## 9. 관련 콘텐츠

- 세션 인사이트
- 채팅 세션 관리
- 보안

---

> 이 문서는 VS Code 공식 `Session sync` 페이지를 바탕으로 한국어로 요약 정리한 내용입니다.
