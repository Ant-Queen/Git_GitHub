# VS Code 에이전트 커스터마이징 - Agent Plugins

원문: https://code.visualstudio.com/docs/agent-customization/agent-plugins

---

## 1. 한 줄 요약

Agent Plugins는 에이전트 커스터마이징을 묶어서 배포하고 설치할 수 있게 해 주는 확장형 기능입니다.

---

## 2. 무엇을 묶을 수 있나?

플러그인 안에는 다음 요소를 포함할 수 있습니다.

- Slash commands
- Agent Skills
- Custom Agents
- Hooks
- MCP Servers

즉, 하나의 패키지로 여러 커스터마이징 기능을 한 번에 제공할 수 있습니다.

---

## 3. 왜 쓰나?

- 팀 공통 워크플로를 손쉽게 배포하고 싶을 때
- 특정 개발 도구 세트를 한 번에 설정하고 싶을 때
- 커뮤니티에서 검증된 설정을 가져오고 싶을 때

---

## 4. 플러그인 구조

플러그인은 보통 다음 파일로 구성됩니다.

- `plugin.json`: 플러그인 메타데이터
- `skills/`: Skill 디렉터리
- `agents/`: Custom Agent 파일
- `hooks/` 또는 `hooks.json`: Hook 설정
- `.mcp.json`: MCP 서버 설정

---

## 5. 설치 방식

- Extensions 뷰에서 Agent Plugins를 찾아 설치할 수 있습니다.
- Git 저장소 URL로 직접 설치할 수도 있습니다.
- GitHub Copilot CLI로 설치한 플러그인도 VS Code에서 사용할 수 있습니다.

---

## 6. 보안 주의사항

플러그인은 hooks나 MCP 서버를 포함할 수 있으므로, 설치 전에는 출처와 내용을 확인하는 것이 중요합니다.

특히 다음을 확인해야 합니다.

- 신뢰할 수 있는 출처인지
- 실행할 코드가 안전한지
- 필요한 권한만 포함하는지

---

## 7. 핵심 정리

Agent Plugins는 “에이전트 커스터마이징을 묶어 배포하는 패키지”입니다. 여러 설정을 한 번에 공유하고 재사용할 때 매우 유용합니다.

---

> 이 문서는 VS Code 공식 Agent plugins 페이지를 기반으로 한국어로 요약 정리한 내용입니다.
