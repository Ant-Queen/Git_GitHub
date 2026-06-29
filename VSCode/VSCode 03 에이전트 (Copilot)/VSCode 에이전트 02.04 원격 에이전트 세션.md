# VS Code 원격 에이전트 세션 정리

원문: https://code.visualstudio.com/docs/agents/remote-agent-sessions

---

## 1. 한 줄 요약

원격 에이전트 세션은 SSH 또는 Dev Tunnel을 통해 다른 머신에서 에이전트를 실행하고, 브라우저 기반 Agents 창으로도 세션을 관리할 수 있는 기능입니다.

---

## 2. 왜 원격 에이전트 세션을 쓰나?

- 로컬 머신 대신 원격 서버의 리소스를 활용할 수 있습니다.
- 다른 장치에서 작업하거나 이동 중에 세션을 확인할 수 있습니다.
- 원격 머신에서 실행 중인 세션을 브라우저에서 관리할 수 있습니다.

---

## 3. SSH로 연결하기

### 필요한 조건

- 원격 머신에 SSH로 접속할 수 있어야 함
- 원격 머신에 별도 에이전트 설치 불필요

### 시작 방법

1. `New` 또는 `Ctrl+N`으로 새 에이전트 세션을 시작합니다.
2. 워크스페이스 드롭다운에서 `Remote` 탭을 선택하고 `SSH`를 선택합니다.
3. SSH 연결 문자열(`user@hostname`)을 입력합니다.
4. 원격 머신에서 사용할 폴더를 선택합니다.
5. 프롬프트를 입력하고 Enter를 눌러 세션을 시작합니다.

---

## 4. Dev Tunnel로 연결하기

### 필요한 조건

- 원격 머신에서 Dev Tunnel이 이미 실행 중이어야 합니다.
- 터널은 GitHub 또는 Microsoft 인증을 요구하도록 설정하는 것이 안전합니다.

### 시작 방법

1. `New` 또는 `Ctrl+N`으로 새 에이전트 세션을 시작합니다.
2. 워크스페이스 드롭다운에서 `Remote` 탭을 선택하고 `Tunnels`를 선택합니다.
3. 활성 Dev Tunnel을 선택합니다.
4. 원격 머신에서 사용할 폴더를 선택합니다.
5. 프롬프트를 입력하고 Enter를 눌러 세션을 시작합니다.

### 보안 주의

- 익명 접근 가능 상태로 터널을 열면 누구나 URL을 통해 접속할 수 있습니다.
- 자동 승인 모드가 활성화된 경우, 승인 없이 명령 실행이 발생할 수 있으므로 더욱 위험합니다.
- 항상 인증이 필요한 상태로 터널을 구성하세요.

---

## 5. 브라우저에서 Agents 창 사용하기

브라우저 기반 Agents 창(`https://insiders.vscode.dev/agents`)을 사용하면 어떤 기기에서든 브라우저로 원격 에이전트 세션을 관리할 수 있습니다.

### 준비

원격 호스트에서 Dev Tunnel을 실행합니다.

```bash
code-insiders tunnel
```

- 정식 버전에서는 `code tunnel`을 사용합니다.
- 최초 실행 시 GitHub 또는 Microsoft 계정으로 인증해야 합니다.

### 연결 방법

1. 브라우저에서 `https://insiders.vscode.dev/agents`를 엽니다.
2. GitHub로 로그인합니다.
3. 상단의 호스트 바에서 연결할 터널 호스트를 선택합니다.
4. 원격 폴더를 선택하고 에이전트를 선택한 다음 세션을 시작합니다.

### 호스트 상태

- Online: 터널이 실행 중이며 연결 가능
- Offline: 터널이 실행되지 않음

호스트가 오프라인인 상태에서 활성 세션이 있으면 연결이 끊어지고, 다시 온라인이 되면 자동으로 재연결됩니다.

---

## 6. 주요 기능

- SSH 또는 Dev Tunnel로 원격 머신에 연결할 수 있습니다.
- 브라우저에서 Agents 창을 열어 세션을 확인하고 관리할 수 있습니다.
- 원격 세션은 에이전트 채팅, 변경 검토, 작업 실행 등 기본 기능을 지원합니다.

---

## 7. 관련 문서

- [Agents 창 사용](https://code.visualstudio.com/docs/agents/agents-window)
- [Agents 개요](https://code.visualstudio.com/docs/agents/overview)
- [원격 터널 사용](https://code.visualstudio.com/docs/remote/tunnels)
- [보안](https://code.visualstudio.com/docs/agents/security)

---

> 이 문서는 VS Code 공식 `Remote agent sessions` 페이지를 기반으로 한국어로 요약 정리한 내용입니다.
