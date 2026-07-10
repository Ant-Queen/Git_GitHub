# VSCode 에이전트 08.03 MCP 구성 참조

## 한줄 요약
MCP 구성은 VS Code 에이전트가 외부 도구나 서버와 연결되도록 설정하는 방식을 설명합니다.

## 핵심 개념
- MCP는 Model Context Protocol의 약자로, 에이전트가 외부 도구를 호출하게 해 줍니다.
- 설정 파일은 주로 mcp.json에 저장합니다.
- 서버에는 stdio, HTTP, SSE 방식이 있으며, 로컬 서버와 원격 서버를 모두 연결할 수 있습니다.
- 민감 정보는 input 변수로 분리해 안전하게 관리할 수 있습니다.
- 샌드박스를 사용하면 서버가 접근할 수 있는 파일/네트워크 범위를 제한할 수 있습니다.

## 실무 팁
- 로컬 개발용 서버는 stdio 방식이 가장 흔합니다.
- API 키 같은 민감값은 mcp.json에 직접 넣지 않고 input 변수로 관리하는 것이 좋습니다.
- 서버가 자주 바뀌면 MCP: Reset Cached Tools로 캐시를 초기화합니다.

## 핵심 정리
MCP는 에이전트의 능력을 “기본 VS Code 기능”에서 “외부 도구 연동”으로 확장하는 핵심 메커니즘입니다.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
