# VSCode 에이전트 07.03 AI 문제해결 가이드

## 한줄 요약
VS Code에서는 로그 확인, 네트워크 진단, 채팅 디버그, MCP 서버 점검을 통해 AI 관련 문제를 체계적으로 해결할 수 있습니다.

## 핵심 개념
- GitHub Copilot 확장 로그를 Trace 수준으로 확인할 수 있습니다.
- GitHub Copilot: Collect Diagnostics로 네트워크 문제를 진단할 수 있습니다.
- /troubleshoot 명령, Agent Debug Log panel, Cache Explorer, Chat Debug view를 활용할 수 있습니다.
- MCP 서버가 동작하지 않으면 서버 로그와 재시작으로 확인할 수 있습니다.

## 실무 흐름
1. 로그 확인
2. 네트워크 진단
3. Agent Debug Log 또는 Chat Debug view로 원인 분석
4. MCP 서버/커스텀 설정 점검
5. 필요 시 피드백 또는 이슈 리포트 제출

## 핵심 정리
문제를 해결할 때는 “결과 자체”보다 로그와 디버그 흐름을 먼저 보는 것이 가장 효율적입니다.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/agents/agent-troubleshooting/troubleshooting
