# VS Code에서 AI 커스터마이징

원문:
- Customization Overview: https://code.visualstudio.com/docs/copilot/customization/overview
- Custom Instructions: https://code.visualstudio.com/docs/copilot/customization/custom-instructions
- Agent Skills: https://code.visualstudio.com/docs/copilot/customization/agent-skills
- Custom Agents: https://code.visualstudio.com/docs/copilot/customization/custom-agents
- MCP Servers: https://code.visualstudio.com/docs/copilot/customization/mcp-servers
- Hooks: https://code.visualstudio.com/docs/copilot/customization/hooks

## 개요

Visual Studio Code는 AI를 코드베이스, 코딩 표준, 워크플로우에 대해 가르칠 수 있는 여러 방법을 제공합니다.

### 커스터마이징 시나리오

#### 1. 코딩 표준 정의

커스텀 지시사항으로 프로젝트 전체 규칙 및 규칙을 AI와 공유. Always-on 지시사항은 모든 요청에 적용되고, 파일 기반 지시사항은 특정 파일 타입이나 폴더를 대상으로 합니다.

예: 모든 파일에 ESLint 규칙을 시행하고 `.tsx` 파일에만 React 패턴 적용.

#### 2. 작업 및 워크플로우 자동화

자주 실행하는 반복 작업을 위해 프롬프트 파일을 만듭니다(컴포넌트 스캐폴딩, 풀 요청 준비).

더 복잡한 다단계 워크플로우의 경우 에이전트 스킬로 패키징합니다.

#### 3. AI 전문화

특정 페르소나를 가정하는 커스텀 에이전트를 만듭니다(보안 검토자, 데이터베이스 관리자, 계획자).

각 에이전트는 고유한 동작, 사용 가능 도구, 언어 모델 기본 설정을 정의합니다.

#### 4. 플러그인 발견 및 설치

에이전트 플러그인(Preview)을 설치하여 슬래시 명령, 스킬, 커스텀 에이전트, 훅, MCP 서버의 미리 패키징된 번들 추가.

#### 5. 외부 도구 및 데이터 연결

MCP 서버를 추가하여 AI가 데이터베이스, API, 기타 서비스에 액세스할 수 있도록 합니다.

훅을 사용하여 모든 파일 편집 후 포매터 실행 또는 보안 정책 시행과 같은 주요 수명 주기 시점에서 쉘 명령 실행.

### 시작하기

증분적으로 AI 커스터마이징 구현:

1. **기초**: Chat 뷰에 `/init` 입력하여 코드베이스를 기반으로 기본 지시사항 생성

2. **타겟 규칙 추가**: 특정 파일 타입이나 프레임워크에 대해 서로 다른 규칙이 필요한 경우 파일 기반 `*.instructions.md` 파일 생성

3. **반복 작업 자동화**: 일반적인 워크플로우에 대한 프롬프트 파일을 만들고 MCP 서버를 추가하여 외부 서비스 연결

4. **전문화된 워크플로우**: 특정 역할에 대한 커스텀 에이전트를 만듭니다. 재사용 가능한 기능을 에이전트 스킬로 패키징합니다.

5. **AI로 커스터마이징 생성**: Chat에서 `/create-prompt`, `/create-instruction`, `/create-skill`, `/create-agent`, `/create-hook` 입력하여 AI가 생성하도록 합니다.

### Agent Customizations 에디터

Chat 뷰의 "Configure Chat" (기어 아이콘)을 선택하거나 Command Palette에서 "Chat: Open Customizations" 실행하여 Agent Customizations 에디터 열기.

이 중앙 UI에서 모든 에이전트 커스터마이징을 생성하고 관리할 수 있습니다. 구성 탭에서 로컬 에이전트, Copilot CLI, Claude 에이전트에 대한 커스터마이징 보기 및 관리 가능.

### 모노레포에서 부모 리포지토리 발견 (Parent Repository Discovery)

모노레포를 사용할 때 보통 리포지토리 루트가 아닌 서브폴더를 VS Code에서 열 수 있습니다.

`chat.useCustomizationsInParentRepositories` 설정을 활성화하면 부모 리포지토리에서도 커스터마이징을 발견합니다.

VS Code는 폴더 계층 구조를 올라가며 `.git` 폴더를 찾은 후, 워크스페이스 폴더와 리포지토리 루트 사이의 모든 폴더에서 커스터마이징을 수집합니다.

---

## 커스텀 지시사항 (Custom Instructions)

### 지시사항 파일 타입

#### Always-on 지시사항

자동으로 모든 chat 요청에 포함됩니다.

- **`.github/copilot-instructions.md`**: 리포지토리 루트의 단일 파일, 모든 chat 요청에 자동 적용
- **`AGENTS.md`**: 여러 AI 에이전트가 인식하는 단일 지시사항 세트
- **조직 레벨 지시사항**: GitHub 조직 수준에서 정의되어 여러 워크스페이스/리포지토리에서 공유
- **`CLAUDE.md`**: Claude Code 및 기타 Claude 기반 도구와의 호환성

#### 파일 기반 지시사항

에이전트가 작업 중인 파일이 지정된 패턴과 일치하거나 작업 설명이 지시사항 설명과 의미론적으로 일치할 때 적용됩니다.

- **`*.instructions.md`**: 파일 타입이나 위치를 기반으로 조건부 적용. 언어별, 프레임워크별, 또는 특정 모듈에 대한 규칙에 사용.

### `.github/copilot-instructions.md` 사용

1. 워크스페이스 루트에 `.github/copilot-instructions.md` 파일 생성 (`.github` 디렉토리 먼저 생성)

2. Markdown 형식으로 지시사항 설명

3. 다음 목적에 사용:
   - 프로젝트 전체의 코딩 스타일 및 명명 규칙
   - 기술 스택 선언 및 선호 라이브러리
   - 따를 아키텍처 패턴 또는 피할 패턴
   - 보안 요구사항 및 에러 처리 접근법
   - 문서 표준

**예제**:
```markdown
# 프로젝트 일반 코딩 지시사항

## 코드 스타일
- ES6+ 기능 사용(const/let, 화살표 함수, 템플릿 리터럴)
- 의미론적 HTML5 요소 사용(header, main, section, article 등)

## 명명 규칙
- 컴포넌트, 인터페이스는 PascalCase
- 변수, 함수, 메서드는 camelCase
- 상수는 ALL_CAPS

## 보안
- 항상 사용자 입력 검증
- API 호출을 위해 환경 변수로 API 키 관리
```

### `.instructions.md` 파일 사용

파일 기반 조건부 지시사항을 위해 하나 이상의 `*.instructions.md` 파일 생성.

#### 파일 위치

- **워크스페이스**: `.github/instructions` 폴더
- **유저 프로필**: `~/.copilot/instructions`, `~/.claude/rules`

`chat.instructionsFilesLocations` 설정으로 추가 파일 위치 구성.

#### 파일 형식

```markdown
---
name: 'Python 표준'
description: 'Python 파일에 대한 코딩 규칙'
applyTo: '**/*.py'
---
# Python 코딩 표준

- PEP 8 스타일 가이드 준수
- 모든 함수 서명에 타입 힌트 사용
- 공개 함수에 docstring 작성
- 들여쓰기: 4개 공백 사용
```

YAML frontmatter 필드:
- `name`: 지시사항 표시명(선택)
- `description`: UI에서 마우스 올릴 때 표시되는 설명(선택)
- `applyTo`: 지시사항을 적용할 파일의 glob 패턴(선택). 지정하지 않으면 자동 적용 안 됨.

#### 지시사항 파일 생성

1. Chat 뷰에서 "Configure Chat" > Instructions 탭 선택

2. "New Instructions (Workspace)" 또는 "New Instructions (User)" 선택

3. 위치 선택 및 파일명 입력

4. YAML frontmatter와 본문 작성

#### AI로 지시사항 생성

Chat에서 `/create-instruction` 입력하고 규칙 설명 입력. 에이전트가 명확한 질문을 하고 적절한 frontmatter와 내용으로 `.instructions.md` 파일 생성.

또는 진행 중인 대화에서 "extract an instruction from this"를 요청하여 대화에서 정정한 내용을 프로젝트 규칙으로 캡처.

### 효과적인 지시사항 작성 팁

- **짧고 자체 포함**: 각 지시사항은 단순한 문장. 여러 정보 필요하면 여러 지시사항으로 분산.

- **이유 포함**: 규칙이 존재하는 이유를 설명하면 AI가 엣지 케이스에서 더 나은 결정을 내림.
  
  예: "moment.js 대신 date-fns를 사용하라. moment.js는 deprecated이고 번들 크기를 증가시킨다."

- **구체적인 예제**: 추상적 규칙보다 코드 예제가 더 효과적.

- **명확한 규칙만**: 린터나 포매터가 이미 시행하는 규칙은 건너뛰기.

- **파일별 지시사항**: 다양한 규칙이 필요하면 여러 `*.instructions.md` 파일을 `applyTo` 패턴으로 선택적 적용.

- **모노레포 설정**: `chat.useNestedAgentsMdFiles` 활성화하여 여러 폴더별 `AGENTS.md` 파일 지원.

---

## 에이전트 스킬 (Agent Skills)

### 커스텀 지시사항 vs 에이전트 스킬

| 비교 | 에이전트 스킬 | 커스텀 지시사항 |
|-----|-------------|-------------|
| 목적 | 전문화된 기능 및 워크플로우 가르치기 | 코딩 표준 및 지시사항 정의 |
| 이식성 | VS Code, Copilot CLI, Copilot 클라우드에서 작동 | VS Code 및 GitHub.com에만 해당 |
| 내용 | 지시사항, 스크립트, 예제, 리소스 | 지시사항만 |
| 범위 | 작업별, 요청 시 로드 | 항상 적용 또는 glob 패턴 |
| 표준 | 개방 표준 (agentskills.io) | VS Code 고유 |

### 스킬 생성

스킬은 `SKILL.md` 파일을 포함하는 디렉토리로 저장됩니다.

#### 스킬 저장 위치

- **프로젝트 스킬**: `.github/skills/`, `.claude/skills/`, `.agents/skills/`
- **개인 스킬**: `~/.copilot/skills/`, `~/.claude/skills/`, `~/.agents/skills/`

`chat.agentSkillsLocations` 설정으로 추가 위치 구성.

#### Agent Customizations 에디터로 스킬 생성

1. Chat 뷰 > "Configure Chat" > Skills 탭

2. "New Skill (Workspace)" 또는 "New Skill (User)" 선택

3. 위치 선택 및 스킬명 입력

4. `SKILL.md` 파일 편집:
   - YAML frontmatter 작성
   - 본문에 상세한 지시사항, 가이드라인, 예제 추가
   - 선택사항: 스킬 디렉토리에 스크립트, 예제, 리소스 추가

#### SKILL.md 파일 형식

```markdown
---
name: webapp-testing
description: 웹 애플리케이션 테스트 실행 및 모니터링. 로그인, 폼 제출, 반응성 확인 등 테스트할 때 사용.
argument-hint: [test file] [options]
user-invocable: true
disable-model-invocation: false
context: inline
---

# 웹 애플리케이션 테스트 스킬

## 개요
웹 애플리케이션의 기능을 자동화된 테스트로 검증합니다...

## 테스트 절차

1. 테스트 환경 준비
2. 브라우저에서 애플리케이션 열기
3. 사용자 상호작용 시뮬레이션
4. 결과 검증

## 참조 파일
[테스트 템플릿](./test-template.js)을 참고하세요.
```

Frontmatter 필드:
- `name`: 스킬 고유 식별자 (소문자, 숫자, 하이픈만 사용. 최대 64자)
- `description`: 스킬이 무엇을 하는지, 언제 사용하는지 설명 (최대 1024자)
- `argument-hint`: Chat에서 스킬 호출 시 표시될 힌트 텍스트
- `user-invocable`: `/` 메뉴에 표시할지 여부 (기본값: true)
- `disable-model-invocation`: 에이전트가 자동으로 로드할 수 있는지 여부 (기본값: false)
- `context`: `inline` (기본값) 또는 `fork` - 포크된 컨텍스트는 전용 subagent에서 실행

#### AI로 스킬 생성

Chat에서 `/create-skill` 입력하고 스킬 설명 입력. 에이전트가 디렉토리 구조, 지시사항, frontmatter를 포함한 `SKILL.md` 파일 생성.

또는 진행 중인 대화에서 "create a skill from how we just debugged that"를 요청하여 다단계 프로세스를 재사용 가능한 스킬로 캡처.

또는 Agent Customizations 에디터에서 "Generate Skill" 선택.

### 포크된 컨텍스트에서 스킬 실행 (실험)

기본적으로 스킬이 로드되면 지시사항이 부모 에이전트의 컨텍스트에 추가됩니다.

큰 스킬이나 중간 추론이 메인 대화에 필요 없는 경우, `context: fork`로 설정하면 스킬이 전용 subagent에서 실행되고 최종 결과만 부모 에이전트로 반환됩니다.

이를 통해 메인 대화의 컨텍스트를 깨끗하게 유지할 수 있습니다.

### 스킬을 슬래시 명령으로 사용

스킬은 Chat에서 슬래시 명령으로 사용 가능합니다. `/` 입력하면 사용 가능한 스킬 및 프롬프트 목록이 표시됩니다.

스킬 호출 후 추가 컨텍스트 추가 가능. 예: `/webapp-testing for the login page` 또는 `/github-actions-debugging PR #42`.

기본적으로 모든 스킬이 `/` 메뉴에 표시되지만, frontmatter의 `user-invocable`과 `disable-model-invocation`로 제어 가능.

---

## 커스텀 에이전트 (Custom Agents)

### 커스텀 에이전트를 사용하는 이유

다양한 작업은 다양한 기능이 필요합니다.

계획 에이전트는 실수 방지를 위해 읽기 전용 도구만 필요하지만, 구현 에이전트는 전체 편집 기능이 필요합니다.

커스텀 에이전트로 각 작업에 정확히 필요한 도구를 지정하고 전문화된 지시사항을 제공합니다.

### 핸드오프 (Handoffs)

핸드오프를 통해 에이전트 간에 가이드된 순차 워크플로우를 만들 수 있습니다.

chat 응답 완료 후 다음 에이전트로 이동할 수 있는 버튼이 나타납니다.

**워크플로우 예**:
- 계획 생성 → 구현 시작
- 구현 완료 → 코드 검토
- 실패한 테스트 작성 → 통과하는 테스트 작성

Frontmatter에서 핸드오프 정의:

```markdown
---
name: "Planner"
description: "구현 계획 생성"
tools: ['search', 'web']
handoffs:
  - label: "Start Implementation"
    agent: implementation
    prompt: "위의 계획을 기반으로 구현을 시작합니다."
    send: false
    model: "GPT-5.2 (copilot)"
---
```

### 커스텀 에이전트 파일 위치

- **워크스페이스**: `.github/agents` 폴더
- **유저 프로필**: `~/.copilot/agents` 또는 VS Code 프로필 유저 데이터

`chat.agentFilesLocations` 설정으로 추가 위치 구성.

### 커스텀 에이전트 파일 구조

`.agent.md` 파일 형식.

#### Header (선택사항)

YAML frontmatter:

```markdown
---
name: "코드 리뷰어"
description: "코드 품질 및 최선의 실습 검토"
tools: ['read', 'web']
model: "GPT-5 (copilot)"
user-invocable: true
disable-model-invocation: false
agents: ["*"]
handoffs: []
---
```

Frontmatter 필드:
- `name`: 에이전트명 (생략하면 파일명 사용)
- `description`: Chat 입력 필드에 표시되는 placeholder 텍스트
- `tools`: 이 에이전트가 사용 가능한 도구 목록
- `agents`: 이 에이전트가 subagent로 사용할 수 있는 에이전트 목록 (`*`로 모두 허용)
- `model`: 사용할 AI 모델 (문자열 또는 배열로 우선순위 지정)
- `user-invocable`: 에이전트 드롭다운에 표시할지 여부 (기본값: true)
- `disable-model-invocation`: 다른 에이전트가 subagent로 호출할 수 있는지 여부 (기본값: false)
- `handoffs`: 다음 에이전트 전환을 위한 버튼

#### Body

커스텀 에이전트 구현을 Markdown으로 작성. 에이전트 선택 시 본문이 프롬프트에 앞에 추가됩니다.

도구 참조: `#tool:<tool-name>` 구문 사용 (예: `#tool:web/fetch`).

### 커스텀 에이전트 생성

1. Chat 뷰 > "Configure Chat" > Agents 탭

2. "New Agent (Workspace)" 또는 "New Agent (User)" 선택

3. 위치 선택 및 파일명 입력

4. 에이전트 세부사항 설정:
   - YAML frontmatter에 기본 설정 입력
   - 본문에 에이전트 지시사항 작성

또는 `/create-agent` 입력하고 페르소나 설명 입력하여 AI로 생성.

### 자주 묻는 질문

**커스텀 에이전트는 Chat 모드와 다른가?**

커스텀 에이전트는 이전에 커스텀 chat 모드로 불렸으며, 기능은 동일하지만 용어가 업데이트되었습니다.

기존 `.chatmode.md` 파일은 `.agent.md`로 이름 변경 후 적절한 위치로 이동하면 계속 사용 가능합니다.

---

## MCP 서버 (Model Context Protocol)

### MCP란?

MCP는 AI 모델을 외부 도구와 서비스에 연결하는 개방 표준입니다.

VS Code에서 MCP 서버는 파일 작업, 데이터베이스, 외부 API와 같은 작업을 위한 도구를 제공합니다.

MCP 서버는 도구 외에도 리소스, 프롬프트, 인터랙티브 앱을 제공할 수 있습니다.

### MCP 서버 빠른 시작

1. Extensions 뷰 열기 (Ctrl+Shift+X) 및 `@mcp playwright` 검색

2. "Install" 선택하여 Playwright MCP 서버 설치

3. 신뢰 확인 시 "Yes" 선택 (VS Code가 서버 도구 발견)

4. Chat 뷰 열기 (Ctrl+Alt+I) 및 프롬프트 입력:
   ```
   Go to code.visualstudio.com, decline the cookie banner, 
   and give me a screenshot of the homepage.
   ```

5. Playwright 도구를 사용하여 브라우저에서 페이지를 열고 스크린샷 캡처

**팁**: Chat 입력에서 "Configure Tools" 버튼으로 모든 Playwright MCP 서버 도구 보기 및 토글.

### MCP 서버 추가

#### mcp.json 파일 수동 구성

두 가지 위치에서 MCP 서버 구성:

- **워크스페이스**: `.vscode/mcp.json` (소스 제어에 포함하여 팀과 공유)
- **유저 프로필**: `MCP: Open User Configuration` 명령 실행 (모든 워크스페이스에서 사용 가능)

또는 Command Palette에서 `MCP: Add Server` 실행하고 안내된 흐름 따르기.

#### mcp.json 예제

```json
{
  "servers": {
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp"
    },
    "playwright": {
      "command": "npx",
      "args": ["-y", "@microsoft/mcp-server-playwright"]
    }
  }
}
```

VS Code는 설정 파일에 IntelliSense 제공. 전체 스키마는 MCP configuration reference 참고.

**주의**: 민감한 정보(API 키)는 하드코딩하지 말고 입력 변수나 환경 파일 사용.

### MCP 서버 관리

VS Code는 여러 옵션으로 MCP 서버 관리:

- **Extensions 뷰**: MCP SERVERS - INSTALLED 섹션에서 우클릭하거나 기어 아이콘 선택
- **mcp.json 에디터**: MCP: Open User/Workspace Configuration 명령 후 인라인 코드 렌즈 사용
- **Command Palette**: `MCP: List Servers` 실행하고 서버 선택 후 작업 선택

### MCP 서버 활성화/비활성화

전역적으로 또는 특정 워크스페이스에서 MCP 서버 활성화/비활성화:

- Extensions 뷰에서 우클릭 > "Enable" 또는 "Disable"
- Command Palette에서 `MCP: List Servers` 실행 후 선택
- Agent Customizations 에디터에서 토글

### 다른 MCP 기능

#### 리소스 (Resources)

MCP 서버의 데이터를 Chat 프롬프트의 컨텍스트로 액세스. 파일, 데이터베이스 테이블, API 응답 등.

Chat 뷰에서 "Add Context" > "MCP Resources" 선택 또는 `MCP: Browse Resources` 명령 실행.

#### 프롬프트 (Prompts)

MCP 서버의 사전 구성 프롬프트 템플릿 사용. Chat 입력에서 `/<MCP server>.<prompt>` 입력.

#### MCP Apps

Chat에서 인라인으로 렌더링되는 양식, 시각화, 드래그-드롭 목록 같은 인터랙티브 UI 컴포넌트.

### MCP 서버 신뢰

새 MCP 서버를 추가하거나 구성을 변경할 때, 처음 실행하기 전에 신뢰를 확인해야 합니다.

대화에서 서버 구성 링크를 선택하여 검토 후 신뢰 결정.

신뢰를 재설정하려면 `MCP: Reset Trust` 명령 실행.

**경고**: 로컬 MCP 서버는 머신에서 임의 코드를 실행할 수 있습니다. 신뢰할 수 있는 소스의 서버만 추가하고 추가 전에 게시자와 서버 구성을 검토하세요.

더 자세한 내용: https://code.visualstudio.com/docs/copilot/customization/mcp-servers

---

## 훅 (Hooks) - Preview

### 훅란?

훅을 통해 에이전트 세션 중 주요 수명 주기 시점에 커스텀 쉘 명령을 실행할 수 있습니다.

자동화된 워크플로우, 보안 정책 시행, 작업 검증, 외부 도구 통합을 위해 사용합니다.

### 훅 사용 사례

- **보안 정책 시행**: `rm -rf`나 `DROP TABLE` 같은 위험한 명령 차단
- **코드 품질 자동화**: 파일 수정 후 포매터, 린터, 테스트 자동 실행
- **감사 추적**: 도구 호출, 명령 실행, 파일 변경 로깅
- **컨텍스트 주입**: 프로젝트별 정보, API 키, 환경 세부사항 추가
- **승인 제어**: 안전한 작업은 자동 승인, 민감한 작업은 확인 요청

### 빠른 시작: 첫 번째 훅

파일 편집 후 Prettier 실행하는 훅:

1. 워크스페이스에 `.github/hooks/format.json` 파일 생성:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "npx prettier --write \"$TOOL_INPUT_FILE_PATH\""
      }
    ]
  }
}
```

2. 파일 저장 - VS Code가 자동으로 훅 로드

3. 에이전트가 다음에 파일 편집하면 Prettier가 변경된 파일에서 실행

4. "GitHub Copilot Chat Hooks" output 채널에서 훅 실행 확인

### 훅 수명 주기 이벤트

VS Code는 8가지 훅 이벤트를 지원합니다:

| 이벤트 | 발생 시점 | 사용 예 |
|-------|---------|--------|
| SessionStart | 새 세션 시작 시 | 리소스 초기화, 세션 시작 로깅 |
| UserPromptSubmit | 사용자 프롬프트 제출 시 | 사용자 요청 감사, 시스템 컨텍스트 주입 |
| PreToolUse | 에이전트 도구 호출 전 | 위험한 작업 차단, 승인 요청, 입력 수정 |
| PostToolUse | 도구 실행 후 | 포매터/린터 실행, 결과 로깅 |
| PreCompact | 대화 컨텍스트 압축 전 | 중요 컨텍스트 내보내기, 상태 저장 |
| SubagentStart | Subagent 시작 시 | 중첩된 에이전트 추적, 리소스 초기화 |
| SubagentStop | Subagent 완료 시 | 결과 집계, 리소스 정리 |
| Stop | 세션 종료 시 | 보고서 생성, 리소스 정리 |

### 훅 파일 위치

VS Code는 다음 위치에서 훅 구성 파일 검색:

- **워크스페이스**: `.github/hooks/*.json`
- **유저 프로필**: `~/.copilot/hooks`, `~/.claude/settings.json`
- **커스텀 에이전트**: 에이전트 `.agent.md` frontmatter의 `hooks` 필드
- **플러그인**: 플러그인의 `hooks.json` 또는 `hooks/hooks.json`

`chat.hookFilesLocations` 설정으로 커스텀 위치 설정.

### 훅 구성 형식

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "./scripts/validate-tool.sh",
        "timeout": 15
      }
    ],
    "PostToolUse": [
      {
        "type": "command",
        "command": "npx prettier --write \"$TOOL_INPUT_FILE_PATH\""
      }
    ]
  }
}
```

훅 명령 속성:

| 속성 | 타입 | 설명 |
|-----|------|------|
| type | string | 항상 "command" |
| command | string | 실행할 명령(크로스 플랫폼) |
| windows | string | Windows 전용 명령 |
| linux | string | Linux 전용 명령 |
| osx | string | macOS 전용 명령 |
| cwd | string | 작업 디렉토리 |
| env | object | 추가 환경 변수 |
| timeout | number | 타임아웃(초, 기본값: 30) |

### 훅 입출력

훅은 stdin/stdout을 통해 VS Code와 JSON으로 통신합니다.

**공통 입력 필드**:
```json
{
  "timestamp": "2026-02-09T10:30:00.000Z",
  "cwd": "/path/to/workspace",
  "sessionId": "session-identifier",
  "hookEventName": "PreToolUse",
  "transcript_path": "/path/to/transcript.json"
}
```

**공통 출력 필드**:
```json
{
  "continue": true,
  "stopReason": "보안 정책 위반",
  "systemMessage": "단위 테스트 실패"
}
```

**Exit codes**:
- 0: 성공 (stdout을 JSON으로 파싱)
- 2: 차단 오류 (처리 중단 및 stderr 에러 표시)
- 기타: 비차단 경고 (처리 계속)

더 자세한 내용: https://code.visualstudio.com/docs/copilot/customization/hooks

---

**최종 업데이트**: 2026년 5월 6일