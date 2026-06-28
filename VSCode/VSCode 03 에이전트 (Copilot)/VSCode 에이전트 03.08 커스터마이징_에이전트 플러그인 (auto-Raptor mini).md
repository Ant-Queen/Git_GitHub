# VS Code 에이전트 플러그인(Agent Plugins)

## 개요
Agent Plugins는 여러 에이전트 커스터마이제이션을 하나의 설치 가능한 패키지로 묶은 것입니다. 플러그인은 Skills, Agents, Hooks, MCP Servers, Slash Commands 등을 함께 제공할 수 있습니다.

## 제공 항목
플러그인은 다음과 같은 항목을 포함할 수 있습니다.
- 슬래시 명령
- Agent Skills
- Custom Agents
- Hooks
- MCP Servers

예시 파일 구조:
```
my-testing-plugin/
  plugin.json
  skills/
    test-runner/
      SKILL.md
      run-tests.sh
  agents/
    test-reviewer.agent.md
  hooks/
    hooks.json
  scripts/
    validate-tests.sh
  .mcp.json
```

## plugin.json 메타데이터
필수 필드:
- `name`: 플러그인 이름(소문자, 숫자, 하이픈만 허용)

선택 필드:
- `description`
- `version`
- `author`
- `skills`
- `agents`
- `hooks`
- `mcpServers`

예시:
```json
{
  "name": "my-dev-tools",
  "description": "React development utilities",
  "version": "1.2.0",
  "author": { "name": "Jane Doe" },
  "skills": "skills/",
  "agents": "agents/",
  "hooks": "hooks.json",
  "mcpServers": ".mcp.json"
}
```

## 플러그인 형식
자동 감지 순서:
- Claude: `.claude-plugin/plugin.json`
- OpenPlugin: `.plugin/plugin.json`
- Copilot 기본: `plugin.json` 또는 다른 형식 탐지

### 플러그인 경로 토큰
- Claude: `${CLAUDE_PLUGIN_ROOT}`
- Copilot: 없음
- OpenPlugin: `${PLUGIN_ROOT}`

## 플러그인의 Hooks
플러그인도 훅을 포함할 수 있습니다.
- Claude 형식: `hooks/hooks.json`
- Copilot 형식: `hooks.json` (플러그인 루트)

예시:
```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "${CLAUDE_PLUGIN_ROOT}/scripts/format.sh"
      }
    ]
  }
}
```

## 플러그인의 MCP 서버
플러그인은 MCP 서버를 번들로 제공할 수 있습니다.
- 파일: `.mcp.json`
- 구성: `mcpServers` 최상위 객체

예시:
```json
{
  "mcpServers": {
    "plugin-database": {
      "command": "${CLAUDE_PLUGIN_ROOT}/servers/db-server",
      "args": ["--config", "${CLAUDE_PLUGIN_ROOT}/config.json"],
      "env": { "DB_PATH": "${CLAUDE_PLUGIN_ROOT}/data" }
    }
  }
}
```

## 플러그인 설치
- Extensions 뷰에서 `@agentPlugins` 검색
- Git 리포지토리 URL로 설치
- GitHub Copilot CLI로 설치된 플러그인도 VS Code에서 자동 검색

## 플러그인 관리
- 설치/비활성화/제거: Extensions 뷰 또는 Agent Customizations editor
- Enable/Disable: 플러그인이 비활성화되면 제공 항목 전체가 숨겨집니다.
- 업데이트: Extensions 뷰에서 업데이트 버튼 클릭

## 플러그인 시장 구성
- `chat.plugins.marketplaces` 설정으로 추가 마켓플레이스 등록
- `owner/repo`, HTTPS git URL, SSH URL, file URI 지원

## 로컬 플러그인 사용
- `chat.pluginLocations` 설정으로 로컬 디렉토리 등록
- `true`로 설정하면 활성화, `false`로 등록만

## 호환성
- VS Code, Copilot CLI, Claude Code 간 공용 플러그인 형식
- 자동 감지는 `.plugin/plugin.json`, `plugin.json`, `.github/plugin/plugin.json`, `.claude-plugin/plugin.json`
- Claude와 Copilot 간 경로 토큰 및 훅 위치 차이 존재

## 문제 해결
- 플러그인이 보이지 않을 때: `plugin.json`의 `name` 규칙 확인
- 스킬이 로드되지 않을 때: `SKILL.md`의 `name` 필드가 디렉토리 이름과 일치하는지 확인
- 업데이트가 반영되지 않을 때: `version`을 올리고 업데이트 확인
- 설치 실패: 캐시된 플러그인 디렉토리 삭제 후 재시도

## 요약
Agent Plugins는 여러 커스터마이제이션을 패키징하여 쉽게 설치하고 공유할 수 있게 해줍니다. 플러그인 메타데이터, 훅, MCP 서버, 스킬, 에이전트 구성을 활용해 자신만의 AI 확장팩을 만들 수 있습니다.
