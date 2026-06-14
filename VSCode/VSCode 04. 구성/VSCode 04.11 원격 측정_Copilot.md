# VS Code 텔레메트리 정리

## 개요

Visual Studio Code는 제품 개선을 위해 텔레메트리 데이터를 수집합니다. 텔레메트리는 VS Code의 문제 해결, 성능 개선, 기능 우선순위 결정, 실험 기능 롤아웃 등에 사용됩니다.

## 텔레메트리 데이터 종류

- Crash Reports: VS Code가 충돌할 때 수집되는 진단 정보
- Error Telemetry: 애플리케이션이 충돌하지는 않았지만 예기치 않은 오류 정보
- Usage Data: 기능 사용 방식과 성능에 대한 정보

## 텔레메트리 비활성화

- `telemetry.telemetryLevel` 설정으로 전송할 텔레메트리 레벨을 제어합니다.
- 가능 값
  - `all` : 충돌, 오류, 사용 데이터 모두 전송
  - `error` : 충돌과 오류만 전송
  - `crash` : 충돌만 전송
  - `off` : 전송하지 않음
- 모든 텔레메트리를 끄려면 `settings.json`에 다음을 추가합니다.
```json
"telemetry.telemetryLevel": "off"
```
- A/B 실험 및 새로운 기능 얼리 액세스에 참여하려면 `telemetry.telemetryLevel`을 `all`로 설정해야 합니다.

## 기능 제공과 텔레메트리

- VS Code는 A/B 실험 시스템을 통해 새 기능을 일부 사용자에게 먼저 배포합니다.
- 이 시스템은 사용 데이터 텔레메트리를 사용하여 사용자 그룹을 결정하고 기능 사용을 검증합니다.
- `telemetry.telemetryLevel`을 `error`, `crash`, `off`로 설정하면 사용 데이터가 비활성화되어 실험 기능 대상에서 제외될 수 있습니다.

## 확장과 텔레메트리

- Microsoft 및 서드파티 확장은 자체 텔레메트리를 수집할 수 있습니다.
- 확장 텔레메트리는 `telemetry.telemetryLevel` 설정에 의해 제어되지 않습니다.
- 확장별 문서를 확인하여 해당 확장의 텔레메트리 보고 여부와 비활성화 방법을 확인하십시오.
- 확장 작성자는 확장 텔레메트리 구현을 위한 모범 사례 문서를 참고할 수 있습니다.

## 텔레메트리 이벤트 출력 채널

- 명령 팔레트에서 `Developer: Show Telemetry`를 실행하면 텔레메트리 출력 채널이 열립니다.
- 텔레메트리 이벤트가 전송될 때마다 세부 정보가 출력 패널에 표시됩니다.
- 추적 중인 이벤트는 로컬 `telemetry.log` 파일에도 기록됩니다.
- `Developer: Open Log...` 명령에서 `Telemetry`를 선택하여 로그 파일을 열 수 있습니다.
- 텔레메트리 추적을 종료하려면 `Developer: Reload Window` 명령으로 창을 다시 로드합니다.

## 모든 텔레메트리 이벤트 보기

- CLI에서 `code --telemetry` 옵션을 사용하면 가능한 모든 텔레메트리 이벤트를 JSON 보고서로 생성할 수 있습니다.
- 예시:
```bash
code --telemetry > telemetry.json && code telemetry.json
```
- 생성된 보고서는 빌드별로 만들어지며 확장 텔레메트리는 확장이 `telemetry.json` 파일을 제공하는 경우에만 포함됩니다.

### 이벤트 분류

- `classification` 필드는 데이터 유형을 설명합니다.
  - `SystemMetaData` : 개인 식별 불가능한 VS Code 생성 값
  - `CallstackOrException` : 스택 추적이 포함된 오류
  - `PublicNonPersonalData` : 공개 가능한 사용자 생성 데이터
  - `EndUserPseudonymizedInformation` : 사용자 고유 식별이 불가능한 해시값

### 이벤트 목적

- `purpose` 필드는 데이터 수집 목적을 설명합니다.
  - `PerformanceAndHealth` : 제품과 서비스의 안정성과 속도 보장
  - `FeatureInsight` : 기능 사용 이해와 개발 방향 결정
  - `BusinessInsight` : VS Code, Microsoft, GitHub의 비즈니스 결정 지원

### 이벤트 엔드포인트

- `endpoint` 필드는 데이터 처리기를 나타냅니다.
  - `GoogleAnalyticsId` : 웹사이트용 Google Analytics 및 페이지 뷰 추적
  - `MacAddressHash` : 클라이언트 측 해시된 MAC 주소를 사용하여 사용자 식별
  - `none` : 특별 처리 불필요

## OpenTelemetry 지원 (에이전트 상호작용)

- Copilot Chat은 OpenTelemetry(OTel)를 통해 에이전트 상호작용, LLM 호출, 도구 실행, 토큰 사용량 등의 추적, 메트릭, 이벤트를 내보낼 수 있습니다.
- OTel 호환 백엔드로 데이터를 전송하여 실시간 모니터링이 가능합니다.

## GDPR과 VS Code

- VS Code 팀은 GDPR을 준수하며 개인정보 보호를 매우 중요하게 다룹니다.
- 주요 대응 내용
  - 기존 및 신규 사용자에게 텔레메트리 옵트아웃 기능 제공
  - 수집 텔레메트리 검토 및 분류
  - 유효한 데이터 보존 정책 마련
- 고유 사용자 식별을 위해 로그인 기반 방식은 사용하지 않습니다.
- 데스크톱에서는 네트워크 어댑터 NIC 해시를, 웹에서는 UUID를 사용해 사용자 대략 정보를 구별합니다.
- 이 방식은 문제 해결에는 충분하지만 정확한 사용자 식별에는 적합하지 않습니다.
- 프라이버시가 걱정되면 텔레메트리를 비활성화할 수 있습니다.
- 더 많은 정보는 Visual Studio Family GDPR 데이터 주체 요청 페이지를 참고하십시오.

## 온라인 서비스 관리

- VS Code는 텔레메트리 외에도 다음과 같은 온라인 서비스를 사용합니다.
  - 제품 업데이트 다운로드
  - 확장 찾기, 설치, 업데이트
  - Settings Sync
  - Settings 편집기 내 자연어 검색
- `@tag:usesOnlineServices` 태그로 관련 설정을 검색하여 개별적으로 켜거나 끌 수 있습니다.
- 이 설정을 끈다고 해서 완전 오프라인 모드가 되는 것은 아닙니다. 예를 들어 확장 검색은 여전히 온라인 마켓플레이스를 사용합니다.
- 확장도 자체 온라인 서비스를 사용할 수 있으며, 해당 확장의 문서를 확인해야 합니다.

### 비-Microsoft 온라인 서비스

- 확장 설치 기능이 `https://registry.npmjs.org`, `https://registry.bower.io`에 요청을 보냄
- TypeScript/JavaScript 언어 기능 확장은 `@types` 도메인(예: `https://registry.npmjs.org`)에 질의함
- 개발자 도구 또는 웹뷰 개발자 도구를 열면 Google 서버와 통신할 수 있음

## 확장 추천

- VS Code는 확장 추천을 위해 다음 정보를 수집합니다.
  - 파일 형식별 활성화된 확장
  - 작업 영역/폴더 정보
- 특정 폴더는 Git 원격 해시를 사용해 식별합니다.
- 사전 계산된 추천은 이후 조건에 맞춰 익명으로 확장 추천을 제공합니다.
- 동적 추천은 VS Code가 파일 형식에 대한 추천을 마켓플레이스에 질의하여 결과를 가져옵니다.
- 추천 이유는 확장 상세 페이지의 헤더에서 확인할 수 있습니다.

## 확장 작성자를 위한 안내

- 텔레메트리를 구현하려는 확장 작성자는 VS Code 확장 가이드의 텔레메트리 문서를 참고해야 합니다.

## 관련 자료

- 조직에서 텔레메트리 로그 수준 중앙 관리: `https://code.visualstudio.com/docs/enterprise/telemetry#_configure-telemetry-level`
- VS Code FAQ: `https://code.visualstudio.com/docs/supporting/faq`
- 사용자 및 작업 영역 설정: `https://code.visualstudio.com/docs/configure/settings`

## 도움말 및 지원

- VS Code 커뮤니티, 기능 요청, 이슈 보고를 통해 추가 지원을 받을 수 있습니다.
