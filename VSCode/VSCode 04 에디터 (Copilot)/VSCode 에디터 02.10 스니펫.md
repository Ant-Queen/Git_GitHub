# VSCode 에디터 02.10 스니펫

## 한줄 요약
스니펫은 자주 쓰는 코드 패턴을 템플릿으로 저장해 빠르게 삽입할 수 있는 도구입니다.

## 핵심 개념
- 스니펫은 JSON 형식으로 정의되며, 변수, 자리표시자, 선택 옵션 등을 지원합니다.
- 스니펫은 언어별 파일, 글로벌 `.code-snippets` 파일, 또는 프로젝트별 `.vscode` 스니펫으로 만들 수 있습니다.
- 탭 순서(`$1`, `$2`, `$0`)와 변수(`TM_FILENAME`, `CURRENT_YEAR` 등)를 이용해 동적 템플릿을 만들 수 있습니다.

## 생성 방법
1. `File > Preferences > Configure User Snippets`에서 언어를 선택하거나 새 글로벌 스니펫 파일 생성
2. JSON 구조로 `prefix`, `body`, `description`을 작성
3. 저장 후 IntelliSense 또는 `Insert Snippet` 명령으로 삽입

## 실무 팁
- 프로젝트 공통 스니펫은 `.vscode` 폴더에 저장해 팀과 공유하세요.
- 복잡한 자리표시자와 변수 변환을 활용하면 반복작업을 크게 줄일 수 있습니다.
- 스니펫 단축어가 너무 일반적이면 다른 제안과 충돌하니 주의하세요.

## 핵심 정리
스니펫은 생산성 향상에 직결되는 기능으로, 반복 코드를 줄이고 일관된 스타일을 유지하는 데 유용합니다.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/editing/userdefinedsnippets
