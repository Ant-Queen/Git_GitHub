# VS Code 에이전트 플러그인 (Agent Plugins) (미리보기)

## 개요

**에이전트 플러그인**은 커스터마이징들을 하나의 설치 가능한 패키지로 번들링합니다. 슬래시 명령, 스킬, 에이전트, 훅, MCP 서버를 모두 포함할 수 있습니다.

### 핵심 특징

- **다용도**: 여러 커스터마이징 타입 번들 가능
- **설치 용이**: 마켓플레이스에서 한 번에 설치
- **공유 가능**: 팀, 커뮤니티와 공유
- **크로스 플랫폼**: VS Code, GitHub Copilot CLI, Claude Code에서 작동

## 플러그인 제공 기능

### 가능한 포함 항목

1. **슬래시 명령** - `/` 입력 시 사용 가능한 명령
2. **스킬** - 에이전트가 자동 또는 수동 로드 가능
3. **에이전트** - 특화된 AI 페르소나
4. **훅** - 라이프사이클 자동화
5. **MCP 서버** - 외부 도구 연결

### 예: 테스팅 플러그인

```
my-testing-plugin/
├── plugin.json           # 플러그인 메타데이터
├── skills/
│   └── test-runner/
│       ├── SKILL.md
│       └── run-tests.sh
├── agents/
│   └── test-reviewer.agent.md
├── hooks/
│   └── hooks.json
├── scripts/
│   └── validate-tests.sh
└── .mcp.json
```

## 플러그인 메타데이터 (plugin.json)

### 필수 필드

```json
{
  "name": "my-dev-tools"
}
```

| 필드 | 필수 | 설명 |
|------|------|------|
| **name** | 예 | 케밥 케이스 플러그인명 (소문자, 숫자, 하이픈만, 최대 64자) |

### 선택 필드

```json
{
  "name": "my-dev-tools",
  "description": "React 개발 유틸리티",
  "version": "1.2.0",
  "author": {
    "name": "Jane Doe",
    "email": "jane@example.com",
    "url": "https://example.com"
  },
  "skills": "skills/",
  "agents": "agents/",
  "hooks": "hooks.json",
  "mcpServers": ".mcp.json"
}
```

| 필드 | 타입 | 설명 |
|------|------|------|
| **description** | string | 플러그인 설명 (최대 1024자) |
| **version** | string | 의미론적 버전 (예: 1.0.0) |
| **author** | object | 작성자 정보 (name 필수, email/url 선택) |
| **skills** | string/array | 스킬 폴더 경로 (기본값: skills/) |
| **agents** | string/array | 에이전트 폴더 경로 (기본값: agents/) |
| **hooks** | string/object | 훅 구성 파일 경로 또는 인라인 객체 |
| **mcpServers** | string/object | MCP 구성 파일 경로 또는 인라인 객체 |

### plugin.json 예시

```json
{
  "name": "my-dev-tools",
  "description": "React 개발 유틸리티",
  "version": "1.2.0",
  "author": {
    "name": "Jane Doe"
  },
  "skills": "skills/",
  "agents": "agents/",
  "hooks": "hooks.json",
  "mcpServers": ".mcp.json"
}
```

## 플러그인 형식 감지

VS Code는 다음 위치를 확인하여 형식을 자동 감지합니다:

| 형식 | 마크 | 우선순위 |
|------|------|---------|
| OpenPlugin | `.plugin/plugin.json` | 1순위 |
| 기본 (Copilot) | `plugin.json` | 2순위 |
| GitHub | `.github/plugin/plugin.json` | 3순위 |
| Claude | `.claude-plugin/plugin.json` | 4순위 |

### 플러그인 환경 변수

형식별 루트 토큰:

| 형식 | 토큰 | 사용 예 |
|------|------|--------|
| Claude | `${CLAUDE_PLUGIN_ROOT}` | `${CLAUDE_PLUGIN_ROOT}/scripts/format.sh` |
| Copilot | (미정의) | N/A |
| OpenPlugin | `${PLUGIN_ROOT}` | `${PLUGIN_ROOT}/config.json` |

## 플러그인의 훅

### 파일 위치

| 형식 | 위치 |
|------|------|
| Claude | `hooks/hooks.json` |
| Copilot | `hooks.json` (플러그인 루트) |

### 구성 포맷

플러그인 훅은 워크스페이스 훅과 동일한 기본 포맷을 사용합니다:

**플랫 포맷:**
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

**매처 포맷 (Claude 호환성):**
```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "${CLAUDE_PLUGIN_ROOT}/scripts/format.sh"
          }
        ]
      }
    ]
  }
}
```

### 플러그인 경로 참조

Claude 형식 플러그인의 `${CLAUDE_PLUGIN_ROOT}` 토큰 사용:

- 훅 명령에서 플러그인 디렉토리 내 파일 참조
- VS Code가 런타임에 절대 경로로 확장
- 스크립트에서 `$CLAUDE_PLUGIN_ROOT` (또는 Windows에서 `%CLAUDE_PLUGIN_ROOT%`) 환경 변수로 접근

## 플러그인의 MCP 서버

### MCP 구성 파일

플러그인 루트의 `.mcp.json`에서 정의:

```json
{
  "mcpServers": {
    "plugin-database": {
      "command": "${CLAUDE_PLUGIN_ROOT}/servers/db-server",
      "args": ["--config", "${CLAUDE_PLUGIN_ROOT}/config.json"],
      "env": {
        "DB_PATH": "${CLAUDE_PLUGIN_ROOT}/data"
      }
    },
    "plugin-api": {
      "command": "npx",
      "args": ["@company/mcp-server", "--plugin-mode"],
      "cwd": "${CLAUDE_PLUGIN_ROOT}"
    }
  }
}
```

**주의:** 최상위 키는 `mcpServers` (워크스페이스 `mcp.json`의 `servers` 아님)

### MCP 경로 참조

`${CLAUDE_PLUGIN_ROOT}` 토큰을 다음 필드에서 사용 가능:

- `command`: 실행 파일 경로
- `args`: 명령어 인수
- `cwd`: 작업 디렉토리
- `env`: 환경 변수 값
- `envFile`: 환경 파일 경로
- `url`: HTTP MCP 서버 URL
- `headers`: HTTP 헤더 값

VS Code는 `CLAUDE_PLUGIN_ROOT` 환경 변수를 서버 프로세스에 주입합니다.

## 플러그인 발견 및 설치

### 플러그인 마켓플레이스에서 찾기

1. 확장 보기 열기 (`Ctrl+Shift+X`)
2. 검색 필드에 `@agentPlugins` 입력
3. 또는 "더 보기"(三) → Views → Agent Plugins

### 마켓플레이스 플러그인 설치

1. 플러그인 목록에서 찾기
2. "설치" 버튼 클릭
3. 새 마켓플레이스 신뢰 확인 (처음만)
4. 사용자 프로필에 설치됨

### 소스에서 설치

Git 저장소에서 직접 설치:

1. 명령 팔레트: `Chat: Install Plugin From Source`
2. 또는 에이전트 커스터마이징 에디터의 + 버튼
3. Git 저장소 URL 입력 (예: `https://github.com/rwoll/markdown-review`)
4. VS Code가 클론하여 설치

### Copilot CLI 플러그인

Copilot CLI로 설치한 플러그인은 자동 발견됩니다:

- 위치: `~/.copilot/installed-plugins/`
- 마켓플레이스: `~/.copilot/installed-plugins/<marketplace>/<plugin>/`
- 직접 Git 설치: `~/.copilot/installed-plugins/_direct/<plugin>/`

## 설치된 플러그인 관리

### 플러그인 보기

확장 보기에서 "Agent Plugins - Installed" 섹션:

- 설치된 모든 플러그인 표시
- 활성화/비활성화/제거 가능

### 활성화/비활성화

플러그인을 제거하지 않고 기능 끄기:

**방법 1: 확장 보기**
- 우클릭 → 활성화/비활성화

**방법 2: 에이전트 커스터마이징 에디터**
- 플러그인 토글

**범위:** 글로벌 또는 워크스페이스 특정

**효과:** 플러그인 비활성화 시:
- 스킬/에이전트 로드 안 됨
- 훅 실행 안 됨
- MCP 서버 시작 안 됨

### 플러그인 제거

확장 보기에서 우클릭 → "제거"

**동작:**
- 외부 소스 플러그인: 디스크에서 제거
- 마켓플레이스 인라인 플러그인: 마켓플레이스 저장소에서만 제거 (디스크 유지)

## 플러그인 마켓플레이스 설정

### 기본 마켓플레이스

기본적으로 다음에서 발견:
- `copilot-plugins`
- `awesome-copilot`

### 추가 마켓플레이스 등록

`chat.plugins.marketplaces` 설정:

```json
{
  "chat.plugins.marketplaces": [
    "owner/repo",
    "https://github.com/anthropics/claude-code.git",
    "git@github.com:anthropics/claude-code.git",
    "file:///path/to/local/marketplace"
  ]
}
```

### 형식

- **단축형**: `owner/repo` (공개 GitHub)
- **HTTPS**: 전체 `.git` URL
- **SSH**: SCP 스타일 참조
- **파일**: `file:///` 로컬 경로

### 마켓플레이스 플러그인 참조

마켓플레이스는 npm, PyPI 등 외부 패키지 소스 참조 가능.

자세한 스키마: [Claude Code 마켓플레이스 문서](https://code.claude.com/docs/en/plugin-marketplaces)

## 로컬 플러그인 사용

수동으로 다운로드/클론한 플러그인 등록:

`chat.pluginLocations` 설정:

```json
{
  "chat.pluginLocations": {
    "/path/to/my-plugin": true,
    "/path/to/another-plugin": false
  }
}
```

- `true`: 활성화
- `false`: 등록하되 비활성화

## 플러그인 업데이트

### 업데이트 확인

명령 팔레트: `Extensions: Check for Extension Updates`

또는 자동 확인 (24시간마다, `extensions.autoUpdate` 활성화 시)

### 업데이트 동작

**마켓플레이스 플러그인:**
- 마켓플레이스 저장소에서 최신 변경 사항 풀
- 새 버전 확인

**npm/PyPI 플러그인:**
- 자동 업데이트 안 됨
- "업데이트" 버튼 클릭 시 설치 명령 실행
- 사용자 확인 필요

**업데이트 알림:**
- 배경 확인 시 새 버전 발견 → 확인까지 대기

## 워크스페이스 플러그인 권장

### 팀 플러그인 추천

프로젝트에서 플러그인을 권장하도록 설정:

워크스페이스 설정 (`.claude/settings.json` 또는 `.github/copilot/settings.json`):

```json
{
  "extraKnownMarketplaces": {
    "company-tools": {
      "source": {
        "source": "github",
        "repo": "your-org/plugin-marketplace"
      }
    }
  },
  "enabledPlugins": {
    "code-formatter@company-tools": true
  }
}
```

### 첫 채팅 시 알림

사용자가 처음 채팅할 때 권장 플러그인 알림:

확장 보기에서 `@agentPlugins @recommended` 필터로 보기

## 크로스 도구 호환성

### 플러그인 공유

동일 플러그인이 여러 도구에서 작동 가능:
- VS Code
- GitHub Copilot CLI
- Claude Code

### 형식 자동 감지

VS Code는 다음 순서로 `plugin.json` 위치 확인:

1. `.plugin/plugin.json`
2. `plugin.json` (루트)
3. `.github/plugin/plugin.json`
4. `.claude-plugin/plugin.json`

### 멀티 도구 작성 시 주의

**훅 파일 위치:**
- Claude: `hooks/hooks.json`
- Copilot: 루트의 `hooks.json`

**플러그인 루트 토큰:**
- Claude: `${CLAUDE_PLUGIN_ROOT}`
- Copilot: 미정의

**스킬 이름:**
- 모든 도구: 순수 케밥 케이스
- 네임스페이스 프리픽스 금지 (`myorg/skillname` ✗)

**도구명 매핑:**
- Claude: `Read`, `Edit`, `Grep`, `Bash`
- Copilot/VS Code: `search`, `editFiles`, `grep`, `shell`

자세한 내용: [GitHub Copilot CLI 플러그인 레퍼런스](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-plugin-reference)

## 문제 해결

### 플러그인이 설치 후 나타나지 않음

**확인:**
1. `chat.plugins.enabled: true` (조직 레벨 설정일 수 있음)
2. `plugin.json`의 `name` 필드가 유효한가?
   - 소문자, 숫자, 하이픈만 허용
   - 슬래시, 콜론 등 특수문자 금지
3. `plugin.json`이 인식된 위치에 있는가?

### 플러그인의 스킬이 로드되지 않음

**확인:**
1. `SKILL.md`의 `name`이 케밥 케이스인가?
2. 스킬 디렉토리명과 `name` 일치하는가?
3. 플러그인이 활성화되어 있는가?

### 버전이 업데이트되지 않음

**확인:**
1. `plugin.json`의 `version` 필드 증가?
2. 마켓플레이스 `marketplace.json`의 버전도 업데이트?
3. 변경사항 푸시 완료?
4. "업데이트 확인" 명령 실행?

### 설치 실패: "destination path already exists"

캐시 문제. 다음 위치의 캐시 디렉토리 삭제:

- **macOS**: `~/Library/Application Support/Code/agentPlugins/github.com/{org}/{repo}`
- **Linux**: `~/.config/Code/agentPlugins/github.com/{org}/{repo}`
- **Windows**: `%APPDATA%\Code\agentPlugins\github.com\{org}\{repo}`

그 후 재설치 시도.

## 보안 고려사항

⚠️ **주의:** 플러그인은 훅과 MCP 서버를 포함할 수 있으며, 이들은 머신에서 임의 코드 실행 가능합니다.

**안전한 설치:**
1. 신뢰할 수 있는 출처에서만 설치
2. 플러그인 코드 검토 (특히 공개 마켓플레이스)
3. 플러그인 권한 확인
4. 조직 마켓플레이스만 사용 (승인된 플러그인)

## 플러그인 개발 팁

1. **시작**: `plugin.json` 최소 요구사항부터
2. **테스트**: 로컬에서 `chat.pluginLocations`으로 테스트
3. **버전**: 의미론적 버전 관리
4. **문서**: README에 기능 상세히 설명
5. **마켓플레이스**: 팀/커뮤니티와 공유
