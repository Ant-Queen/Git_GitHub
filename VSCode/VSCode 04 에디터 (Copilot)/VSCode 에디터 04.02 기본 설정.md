# VSCode 에디터 04.02 기본 설정 (Default Settings)

## 한줄 요약
VS Code의 모든 기본 설정 목록과 기본값, 설정 키의 형식 및 우선순위를 설명합니다.

## 핵심 개념
- 기본 설정은 VS Code가 제공하는 `Default` 값으로, 사용자/워크스페이스 설정이 없을 때 사용됩니다.
- 설정은 `settings.json`에서 사용자 또는 워크스페이스 수준으로 오버라이드할 수 있습니다.
- 각 설정 항목은 설명, 타입, 기본값을 가지며 공식 문서에서 키 이름과 의미를 확인할 수 있습니다.

## 주요 내용
- 기본 설정 목록은 문서에서 검색 가능하며, JSON 경로(예: `editor.tabSize`)로 참조합니다.
- 설정의 범위(scope): `application`(전체), `window`, `resource`(파일/폴더 단위) 등으로 분류됩니다.
- 설정 변경은 Settings UI 또는 `settings.json`에서 수행 가능.

## 실무 팁
- 프로젝트 규칙(탭 길이, 포맷터 설정 등)은 워크스페이스 설정에 넣어 팀원 간 일관성을 유지하세요.
- 민감 정보는 설정에 직접 넣지 말고 환경 변수나 시크릿 스토어 사용을 권장합니다.
- 기본값을 확인하려면 Settings UI의 설명 또는 default settings JSON을 참고하세요.

## 핵심 정리
기본 설정 문서는 가능한 설정 키와 기본 동작을 이해하는 데 필수적입니다. 변경 전 기본값과 적용 범위를 확인하세요.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/reference/default-settings
