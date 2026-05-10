# VS Code Extension Runtime Security 정리

Visual Studio Code 확장 런타임 보안 페이지(`https://code.visualstudio.com/docs/configure/extensions/extension-runtime-security`)를 한국어로 요약한 문서입니다.

## 개요

VS Code 확장은 확장 호스트에서 실행되며, 확장 호스트는 VS Code와 동일한 권한을 갖습니다. 즉, 확장은 파일 읽기/쓰기, 네트워크 요청, 외부 프로세스 실행, 워크스페이스 설정 변경 같은 작업을 수행할 수 있습니다.

이 문서에서는 확장의 런타임 권한과 안전한 확장 선택을 위한 보호 메커니즘을 설명합니다.

## 확장 런타임 권한

- 확장 호스트는 VS Code 자체가 할 수 있는 모든 작업을 수행할 수 있습니다.
- 확장은 로컬 파일 시스템에 접근하고, 네트워크에 연결하며, 외부 도구를 실행할 수 있습니다.
- 따라서 설치 전에 확장의 신뢰성과 동작을 반드시 확인해야 합니다.

## 확장 게시자 신뢰

- VS Code 1.97부터 서드파티 게시자의 확장을 처음 설치할 때 게시자를 신뢰하는지 확인하는 대화상자가 표시됩니다.
- 확장 팩이나 종속 확장이 있는 확장을 설치할 때는 해당 종속 확장 게시자도 함께 신뢰하게 됩니다.
- 이전에 설치한 확장의 게시자는 자동으로 신뢰된 게시자로 간주됩니다.
- `Extensions: Manage Trusted Extensions Publishers` 명령으로 신뢰된 게시자 목록을 관리할 수 있습니다.

> 중요: 커맨드 라인(`code --install-extension`)으로 설치한 확장은 게시자가 자동으로 신뢰되지 않습니다.

## 확장 신뢰성 판단 방법

설치를 결정하기 전에 다음 정보를 확인합니다.

- 평점 및 리뷰: 다른 사용자의 평가와 의견 확인
- Q&A: 게시자의 응답성과 문제 해결 태도 확인
- 이슈, 저장소, 라이선스: 게시자가 제공했는지 확인
- Verified Publisher: 게시자 이름 옆 파란 체크 마크 여부 확인
  - 도메인 소유권이 검증된 게시자
  - 도메인이 존재하고 Marketplace에서 6개월 이상 신뢰 상태임

확장의 신뢰도를 높이려면 공식 문서와 저장소, 문제 추적 상태를 검토하세요.

## Marketplace 보호 기능

Visual Studio Marketplace는 악성 확장으로부터 사용자를 보호하기 위해 여러 보안 기능을 제공합니다.

- 악성코드 검사: 각 확장 패키지에 대해 여러 안티바이러스 엔진으로 검사
- 동적 탐지: 샌드박스 환경에서 확장 런타임 동작을 검증
- Verified Publisher: 게시자의 도메인 소유권과 Marketplace 상태 검증
- 이상 사용 모니터링: 다운로드 및 사용 패턴 감시
- 이름 도용 방지: Microsoft, RedHat 등 공식 게시자 이름과 인기 확장 이름의 도용 차단
- 차단 목록: 악성 확장이나 취약 확장 종속성은 Marketplace에서 제거되고, 설치된 경우 VS Code가 자동으로 제거
- 확장 서명 검증: 게시된 확장을 서명하고 설치 시 무결성과 출처를 확인
- 비밀 스캔: 새로 게시된 확장에서 API 키, 자격 증명 등 비밀 정보 탐지 후 게시 차단
  - `vsce`는 `.env` 파일 검사 및 비밀이 발견되면 게시 차단

더 자세한 내용은 Marketplace 보안 및 신뢰 관련 블로그를 참고하세요.

## 의심스러운 확장 신고

의심스러운 확장을 발견하면 Marketplace 팀에 신고할 수 있습니다.

신고 방법:
1. Visual Studio Marketplace에서 확장 페이지를 엽니다.
2. `More Info` 섹션 하단의 `Report a concern` 링크를 선택합니다.

Marketplace 팀은 일반적으로 영업일 기준 하루 이내에 초기 응답을 제공합니다.

## 관련 자료

- 확장 설치 및 관리: `https://code.visualstudio.com/docs/configure/extensions/extension-marketplace`
- 워크스페이스 트러스트: `https://code.visualstudio.com/docs/editing/workspaces/workspace-trust`
- 조직용 허용 확장 구성: `https://code.visualstudio.com/docs/enterprise/extensions#_configure-allowed-extensions`

## 도움 및 지원

- 페이지 하단의 `Ask the community`, `Request features`, `Report issues` 링크로 추가 지원을 받을 수 있습니다.
