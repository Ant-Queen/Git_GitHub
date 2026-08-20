# VSCode 에디터 03.10 명령행 (Command-line)

## 한줄 요약
VS Code의 명령줄 인터페이스(`code` 명령)를 사용하면 편집기 실행, 파일/폴더 열기, 확장 관리 등을 터미널에서 빠르게 제어할 수 있습니다.

## 핵심 개념
- `code` 명령은 OS에 따라 PATH에 추가해야 터미널에서 사용 가능합니다(`Install 'code' command in PATH` 또는 VS Code 내 메뉴 사용).
- 주로 사용하는 옵션: 새 창(`-n`), 폴더에서 열기(`.`), 특정 위치로 이동(`--goto`), diff 보기(`--diff`), 대기 모드(`--wait`) 등입니다.

## 주요 명령 예시
- `code .` — 현재 폴더를 VS Code에서 엽니다.
- `code -n file.txt` — 새 창에서 `file.txt`를 엽니다.
- `code --goto file:line:column` — 지정한 파일의 위치로 바로 이동합니다.
- `code --diff file1 file2` — 두 파일의 차이를 비교합니다.
- `code --install-extension ms-python.python` — 확장 설치
- `code --list-extensions` — 설치된 확장 목록 출력
- `code --disable-extensions` — 확장을 비활성화하고 실행

## 실무 팁
- 원격 서버에서 GUI가 없는 환경의 경우 `code --folder-uri` 또는 SSH 포워딩과 함께 사용해 편리하게 작업하세요.
- 스크립트나 CI에서 특정 버전의 VS Code를 사용할 필요가 있으면 `--user-data-dir`/`--extensions-dir`를 지정해 독립 환경을 만드세요.
- `--wait` 옵션은 Git이나 다른 툴에서 에디터가 닫힐 때까지 기다려야 하는 훅에 유용합니다.

## 핵심 정리
명령행 인터페이스는 반복 작업 자동화와 빠른 파일 접근에 강력하며, 여러 옵션으로 작업 흐름을 터미널 기반으로 통합할 수 있습니다.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/configure/command-line
