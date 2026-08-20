# VSCode 에디터 04.04 태스크 부록 (Tasks Appendix)

## 한줄 요약
태스크 구성에서 자주 사용하는 예제, 문제 해결 팁, 고급 옵션을 정리한 부록입니다.

## 핵심 개념
- `tasks.json`은 작업(빌드, 테스트, 스크립트 실행 등)을 정의하는 파일로, `version`과 `tasks` 배열로 구성됩니다.
- 태스크는 `label`, `type`, `command`, `args`, `group`, `presentation` 등의 속성을 가집니다.
- 문제 매칭(`problemMatcher`)을 설정해 빌드 오류를 문제 패널로 연결할 수 있습니다.

## 주요 예제
- 간단한 npm 스크립트 실행 태스크
- 병렬/순차 실행을 위한 `dependsOn` 설정
- 터미널 동작 제어를 위한 `presentation` 옵션(ex: `reveal`, `panel`) 적용

## 실무 팁
- 공통 명령은 템플릿화해 여러 태스크에서 재사용하세요.
- `problemMatcher`를 잘 구성하면 컴파일 오류를 클릭해 해당 파일로 바로 이동할 수 있어 디버깅이 쉬워집니다.
- CI 환경과 로컬 환경의 설정 차이는 `isBackground`, `watching` 등의 옵션으로 처리하세요.

## 핵심 정리
`tasks.json`을 잘 구성하면 개발 워크플로를 자동화하고 오류 탐지·수정 속도를 높일 수 있습니다. 부록의 예제를 참고해 표준 태스크를 만들어 보세요.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/reference/tasks-appendix
