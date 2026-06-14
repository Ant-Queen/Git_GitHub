# VS Code 명령줄 정리

## 개요

Visual Studio Code는 `code` CLI를 통해 파일, 폴더, 확장, 프로필, 채팅 등 다양한 기능을 명령줄에서 제어할 수 있습니다.

## 명령줄 도움말

- 터미널 또는 명령 프롬프트에서 `code --help`를 입력하면 사용 가능한 옵션 목록과 간단한 사용 예시를 볼 수 있습니다.

## 명령줄에서 VS Code 실행하기

- 현재 폴더에서 VS Code를 열려면:
  - `code .`
- 지정한 파일이나 폴더를 열 수 있습니다.
- 파일 또는 폴더가 존재하지 않으면 새로 만들거나 멀티 루트 작업 영역을 생성합니다.
- macOS에서는 먼저 `Shell Command: Install 'code' command in PATH`를 실행하여 `code` 명령을 PATH에 추가해야 합니다.
- Windows와 Linux는 일반적으로 설치 시 `PATH`에 VS Code 이진 위치를 자동으로 추가합니다.
- Insiders 빌드를 사용하는 경우 명령은 `code-insiders`입니다.

## 핵심 CLI 옵션

- `-h`, `--help` : 도움말 출력
- `-v`, `--version` : VS Code 버전, GitHub 커밋 ID, 아키텍처 출력
- `-n`, `--new-window` : 새 창으로 열기
- `-r`, `--reuse-window` : 마지막 활성 창에서 열기
- `-g`, `--goto` : `파일:행[:열]` 형식으로 특정 위치에서 파일 열기
- `-d`, `--diff <file1> <file2>` : 두 파일의 차이 비교 열기
- `-m`, `--merge <path1> <path2> <base> <result>` : 3방향 병합 수행
- `-w`, `--wait` : 파일이 닫힐 때까지 대기
- `--locale <locale>` : 표시 언어(locale) 설정

## 파일과 폴더 열기

- 파일을 여러 개 지정하면 VS Code는 단일 인스턴스에서 모두 엽니다.
- 폴더를 여러 개 지정하면 멀티 루트 작업 영역을 생성합니다.
- 경로는 절대 또는 현재 디렉터리에 대한 상대 경로로 지정할 수 있습니다.
- 예시:
  - `code index.html style.css documentation\readme.md`
- 주요 인수
  - `file` : 열 파일 경로, 없으면 새 파일 생성
  - `file:line[:character]` : 특정 행/열에서 열기
  - `folder` : 열 폴더 경로
  - `--skip-add-to-recently-opened` : 최근 파일/폴더 목록에 추가하지 않기

## 프로필 선택

- `--profile` 옵션을 사용하여 특정 프로필로 VS Code를 실행할 수 있습니다.
- 예시:
  - `code ~/projects/web-sample --profile "Web Development"`
- 지정한 프로필이 없으면 동일한 이름의 새 빈 프로필이 만들어집니다.

## 확장 관련 명령

- `--install-extension <extension-id> | <extension-vsix-path>` : 확장 설치 또는 업데이트
  - 예: `ms-python.python`
  - 특정 버전을 설치하려면 `@{version}`을 추가
- `--uninstall-extension <extension-id>` : 확장 제거
- `--disable-extensions` : 모든 확장 비활성화
- `--list-extensions` : 설치된 확장 목록 출력
- `--show-versions` : 확장 버전 정보 포함하여 출력
- `--enable-proposed-api <ext>` : 확장의 제안 API 활성화
- `--update-extensions` : 설치된 확장 업데이트 후 종료
- `--profile`을 함께 사용하면 특정 프로필의 확장에 대해 명령 실행 가능

## 명령줄에서 채팅 시작하기

- `code chat <prompt>` 형식으로 현재 디렉터리에서 채팅을 시작할 수 있습니다.
- 예시:
  - `code chat Find and fix all untyped variables`
- `chat` 하위 명령 옵션
  - `-m`, `--mode <mode>` : `ask`, `edit`, `agent` 또는 사용자 지정 에이전트 지정
  - `-a`, `--add-file <path>` : 채팅 세션에 파일 컨텍스트 추가
  - `--maximize` : 채팅 세션 창 최대화
  - `-r`, `--reuse-window` : 마지막 활성 창 사용
  - `-n`, `--new-window` : 새 창에서 열기
- `-`를 전달하면 표준 입력(stdin)을 채팅 프롬프트로 사용합니다.
  - 예: `python app.py | code chat why does it fail -`

## 고급 CLI 옵션

- `--extensions-dir <dir>` : 확장 루트 폴더 설정
- `--user-data-dir <dir>` : 사용자 데이터 디렉터리 지정
- `-s`, `--status` : 프로세스 사용량 및 진단 정보 출력
- `-p`, `--performance` : 시작 성능 명령 활성화
- `--disable-gpu` : GPU 하드웨어 가속 비활성화
- `--verbose` : 자세한 출력(기본적으로 `--wait` 포함)
- `--prof-startup` : 시작 시 CPU 프로파일러 실행
- `--upload-logs` : 현재 세션 로그 업로드
- `--remote <authority>` : 원격 개발 환경 연결
- `--add <dir>` : 멀티 루트 작업 영역에 폴더 추가
- `--remove <dir>` : 멀티 루트 작업 영역에서 폴더 제거

## VS Code 인스턴스 분리 실행

- `--user-data-dir` 옵션을 사용하여 서로 다른 사용자 데이터 디렉터리를 지정하면 독립된 환경에서 VS Code를 실행할 수 있습니다.
- 예시:
  - `code ~/project1 --user-data-dir ~/vscode-data-project1`
  - `code ~/project2 --user-data-dir ~/vscode-data-project2`
- 각 인스턴스는 별도 환경 변수, 설정, 확장, UI 상태를 유지합니다.
- 주의: 각 사용자 데이터 디렉터리에 확장을 다시 설치해야 합니다.

## 원격 터널 생성

- `code tunnel` 명령으로 원격 머신에서 터널을 생성할 수 있습니다.
- 이 기능은 Remote - Tunnels 확장과 연계되어 보안 터널을 사용해 원격 시스템에 연결합니다.
- `code tunnel -help`로 터널 관련 추가 명령을 확인할 수 있습니다.

## URL로 VS Code 열기

- 플랫폼 URL 핸들링을 사용하여 다음과 같이 VS Code를 열 수 있습니다.
  - 프로젝트 열기: `vscode://file/{full path to project}/`
  - 파일 열기: `vscode://file/{full path to file}`
  - 파일 특정 위치 열기: `vscode://file/{full path to file}:line:column`
  - 설정 편집기 열기: `vscode://settings/setting.name`
- Windows에서 `start vscode://...` 형태로 사용할 수 있습니다.
- Insiders 빌드는 `vscode-insiders://` URL 접두사를 사용합니다.

## 자주 묻는 질문

### 'code' 명령을 찾을 수 없을 때

- OS가 `code` 바이너리를 PATH에서 찾을 수 없음
- Windows/Linux에서는 설치 시 PATH에 추가되어야 함
- macOS에서는 `Shell Command: Install 'code' command in PATH`를 실행해야 함
- 문제가 계속되면 플랫폼별 설치 가이드를 참조합니다.

### VS Code 내에서 명령줄(터미널)에 접근하는 방법

- VS Code에는 내장 터미널(Integrated Terminal)이 있어 에디터 내부에서 커맨드를 실행할 수 있습니다.

### 포터블 버전에서 설정 위치 지정이 가능한가요?

- 명령줄로 직접 지정할 수는 없지만, VS Code 포터블 모드를 사용하면 설정과 데이터를 설치 폴더에 함께 저장할 수 있습니다.

### 쉘이 VS Code로부터 실행되었는지 감지하는 방법

- VS Code가 초기 셸을 실행할 때 `VSCODE_RESOLVING_ENVIRONMENT=1` 환경 변수를 설정합니다.
- 이 값을 확인하면 셸이 VS Code 환경을 위해 실행된 것인지 알 수 있습니다.

## 다음 단계

- 통합 터미널: `https://code.visualstudio.com/docs/terminal/basics`
- 기본 편집: `https://code.visualstudio.com/docs/editing/codebasics`
- 코드 탐색: `https://code.visualstudio.com/docs/editing/editingevolved`
