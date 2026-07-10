# VSCode 에이전트 06.11 에이전트 모니터링 가이드

## 한줄 요약
OpenTelemetry를 사용하면 VS Code에서 에이전트의 실행 흐름, 도구 호출, 토큰 사용량, 오류 상황을 추적할 수 있습니다.

## 핵심 개념
- 추적(trace), 메트릭(metric), 이벤트(event)를 수집할 수 있습니다.
- 주요 span: invoke_agent, chat, execute_tool, execute_hook
- OTel은 기본적으로 꺼져 있으며, 필요할 때 설정을 켜야 합니다.
- 민감한 내용은 기본적으로 수집되지 않고, captureContent 옵션을 켤 때만 세부 내용이 포함됩니다.
- 설정은 VS Code 설정, 환경 변수, 또는 조직 정책으로 관리할 수 있습니다.

## 실무 활용
- 에이전트가 어떤 도구를 호출했는지 확인할 수 있습니다.
- 토큰 사용량과 지연 시간을 분석해 비용과 성능을 개선할 수 있습니다.
- 백엔드로 OpenTelemetry를 연결해 대시보드에서 시각화할 수 있습니다.

## 핵심 정리
모니터링은 에이전트가 실제로 어떻게 동작하는지 확인하고, 성능과 안정성을 개선하는 데 필수입니다.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/agents/guides/monitoring-agents
