# VSCode 에디터 02.12 멀티 루트 워크스페이스

## 한줄 요약
여러 폴더를 한 워크스페이스에 묶어 동시에 작업할 수 있는 기능으로, 서로 다른 프로젝트를 한 창에서 관리하기 좋습니다.

## 핵심 개념
- `.code-workspace` 파일에 루트 폴더 배열을 정의해 사용합니다.
- 각 루트 폴더는 독립적인 `.vscode` 설정을 가질 수 있으며, 워크스페이스 전역 설정도 지정 가능합니다.
- UI나 검색 결과에 폴더명이 함께 표시되어 파일 충돌을 구분하기 쉽습니다.

## 주요 기능
- 폴더 추가/제거: `File > Add Folder to Workspace` 또는 드래그 앤 드롭
- 워크스페이스 파일 저장: `Save Workspace As...`로 `.code-workspace` 생성
- Workspace-scoped settings, launch, tasks 지원
- Source Control Providers 섹션에 여러 리포지토리 표시

## 실무 팁
- 클라이언트/서버 등 관련 프로젝트들을 묶어 개발 컨텍스트를 한 번에 열면 편리합니다.
- 워크스페이스 레벨에 공통 설정(예: window.zoomLevel)을 넣어 일관된 환경을 유지하세요.
- 일부 확장(또는 설정)은 멀티 루트에서 제한되거나 작동 방식이 달라질 수 있으니 문서를 확인하세요.

## 핵심 정리
멀티 루트 워크스페이스는 관련 프로젝트를 함께 보며 작업할 때 강력한 생산성 도구가 됩니다.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/editing/workspaces/multi-root-workspaces
