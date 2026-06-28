# VS Code 훅 (Hooks)

## 개요

**훅**은 에이전트 세션의 특정 라이프사이클 지점에서 **결정적이고 코드 기반의 자동화**를 실행합니다. 지시사항이나 커스텀 프롬프트가 동작을 "권장"한다면, 훅은 **보장된 실행**을 제공합니다.

### 훅의 목적

- **보안 정책 강제**: 위험한 명령 차단 (예: `rm -rf`)
- **코드 품질 자동화**: 파일 편집 후 자동 포매팅
- **감시 추적**: 모든 도구 호출 기록
- **컨텍스트 주입**: 세션에 프로젝트 정보 추가
- **승인 제어**: 안전한 작업은 자동 승인, 민감한 작업은 확인 필요

## 훅 라이프사이클 이벤트

VS Code는 8가지 훅 이벤트를 지원합니다:

| 이벤트 | 발생 시점 | 사용 예시 |
|--------|---------|---------|
| **SessionStart** | 새 에이전트 세션 시작 | 리소스 초기화, 세션 로깅 |
| **UserPromptSubmit** | 사용자가 프롬프트 제출 | 사용자 요청 감시, 시스템 컨텍스트 주입 |
| **PreToolUse** | 도구 호출 전 | 위험한 작업 차단, 승인 요청 |
| **PostToolUse** | 도구 완료 후 | 결과 검증, 후속 작업 트리거 |
| **PreCompact** | 대화 컨텍스트 압축 전 | 중요 정보 내보내기 |
| **SubagentStart** | 서브에이전트 생성 | 서브에이전트 추적, 컨텍스트 주입 |
| **SubagentStop** | 서브에이전트 완료 | 결과 수집, 서브에이전트 리소스 정리 |
| **Stop** | 에이전트 세션 종료 | 리포트 생성, 알림 발송 |

## 빠른 시작: 첫 번째 훅

### 예: Prettier로 파일 자동 포매팅

1. `.github/hooks/format.json` 파일 생성:

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

2. 파일 저장
3. VS Code가 자동으로 훅 로드
4. 에이전트가 다음에 파일 편집 시 Prettier 자동 실행
5. "GitHub Copilot Chat Hooks" 출력 채널에서 확인

## 훅 파일 위치

VS Code는 다음 위치에서 훅 구성 파일을 검색합니다:

| 범위 | 위치 |
|------|------|
| 워크스페이스 | `.github/hooks/*.json` |
| 워크스페이스 (Claude 형식) | `.claude/settings.json`, `.claude/settings.local.json` |
| 사용자 | `~/.copilot/hooks`, `~/.claude/settings.json` |
| 커스텀 에이전트 | `.agent.md` 프론트매터의 `hooks` 필드 |
| 플러그인 | `hooks.json` 또는 `hooks/hooks.json` |

### 파일 위치 커스터마이징

`chat.hookFilesLocations` 설정으로 추가 위치 지정:

```json
{
  "chat.hookFilesLocations": {
    ".github/hooks": true,
    ".claude/settings.json": true,
    "~/.claude/settings.json": true,
    "custom/hooks": true,
    "~/my-hooks/security.json": true
  }
}
```

경로를 `false`로 설정하여 특정 위치 비활성화 가능.

## 훅 파일 포맷

### 기본 구조

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

### 훅 명령 속성

| 속성 | 필수 | 설명 |
|------|------|------|
| **type** | 예 | 항상 `"command"` |
| **command** | 예 | 실행할 크로스 플랫폼 명령 |
| **windows** | 아니오 | Windows 전용 명령 (우선) |
| **linux** | 아니오 | Linux 전용 명령 (우선) |
| **osx** | 아니오 | macOS 전용 명령 (우선) |
| **cwd** | 아니오 | 작업 디렉토리 (저장소 루트 상대) |
| **env** | 아니오 | 추가 환경 변수 |
| **timeout** | 아니오 | 타임아웃 (초, 기본값: 30) |

### OS별 명령 (우선순위)

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "./scripts/format.sh",
        "windows": "powershell -File scripts\\format.ps1",
        "linux": "./scripts/format-linux.sh",
        "osx": "./scripts/format-mac.sh"
      }
    ]
  }
}
```

## 훅 입출력

### 훅 입력 (stdin)

모든 훅은 JSON 객체를 stdin으로 받습니다:

**공통 필드 (모든 이벤트):**

```json
{
  "timestamp": "2026-06-21T10:30:00Z",
  "cwd": "/path/to/workspace",
  "session_id": "session-123",
  "hook_event_name": "PreToolUse",
  "transcript_path": "/tmp/transcript.md"
}
```

**이벤트별 추가 필드:**

- **PreToolUse**: `tool_name`, `tool_input`, `tool_use_id`
- **PostToolUse**: 위 필드 + `tool_response`
- **UserPromptSubmit**: `prompt`
- **SessionStart**: `source` (항상 "new")
- **SubagentStart/Stop**: `agent_id`, `agent_type`
- **PreCompact**: `trigger`

### 훅 출력 (stdout)

훅은 JSON을 stdout으로 반환할 수 있습니다:

```json
{
  "continue": true,
  "stopReason": "보안 정책 위반",
  "systemMessage": "단위 테스트 실패",
  "hookSpecificOutput": {
    "hookEventName": "PreToolUse",
    "permissionDecision": "deny",
    "permissionDecisionReason": "파괴적인 명령이 차단되었습니다",
    "updatedInput": { "files": ["src/safe.ts"] },
    "additionalContext": "사용자는 읽기 전용 접근만 가능합니다"
  }
}
```

### 종료 코드

| 코드 | 의미 |
|------|------|
| **0** | 성공: stdout의 JSON 파싱 |
| **2** | 차단 오류: 작업 중지, 에러 표시 |
| **기타** | 경고: 작업 계속, 경고 표시 |

### 출력 필드

| 필드 | 타입 | 설명 |
|------|------|------|
| **continue** | boolean | false면 작업 중지 (기본값: true) |
| **stopReason** | string | 중지 이유 (continue: false일 때 표시) |
| **systemMessage** | string | 사용자에게 표시될 경고 메시지 |
| **hookSpecificOutput** | object | 이벤트별 세부 제어 |

## 훅 이벤트 상세

### PreToolUse (도구 호출 전)

**입력:**
```json
{
  "tool_name": "editFiles",
  "tool_input": { "files": ["src/main.ts"] },
  "tool_use_id": "tool-123"
}
```

**출력 (hookSpecificOutput):**
```json
{
  "permissionDecision": "deny|ask|allow",
  "permissionDecisionReason": "이유",
  "updatedInput": { "files": ["src/safe.ts"] },
  "additionalContext": "추가 정보"
}
```

**permissionDecision 우선순위:**
- `deny` (가장 제한적): 도구 호출 차단
- `ask`: 사용자 확인 필요
- `allow` (가장 허용적): 자동 승인

여러 훅이 실행될 때 가장 제한적인 결정이 우선됩니다.

### PostToolUse (도구 완료 후)

**입력:**
```json
{
  "tool_name": "editFiles",
  "tool_input": { "files": ["src/main.ts"] },
  "tool_use_id": "tool-123",
  "tool_response": "파일 편집 완료"
}
```

**출력:**
```json
{
  "decision": "block",
  "reason": "검증 실패",
  "hookSpecificOutput": {
    "additionalContext": "린팅 오류 발생"
  }
}
```

### SessionStart (세션 시작)

**입력:**
```json
{
  "source": "new"
}
```

**출력:**
```json
{
  "hookSpecificOutput": {
    "additionalContext": "프로젝트: my-app v2.1.0 | 브랜치: main"
  }
}
```

### Stop (세션 종료)

**입력:**
```json
{
  "stop_hook_active": false
}
```

**출력:**
```json
{
  "hookSpecificOutput": {
    "decision": "block",
    "reason": "테스트 스위트를 실행하지 않으면 완료 불가"
  }
}
```

⚠️ **주의:** Stop 훅이 세션을 차단하면 추가 AI 크레딧이 소비됩니다.

### UserPromptSubmit (프롬프트 제출)

사용자가 프롬프트를 제출할 때 실행됩니다.

**추가 입력:** `prompt` 필드 포함

**사용 예:** 사용자 요청 감시, 시스템 컨텍스트 주입

### SubagentStart/SubagentStop

서브에이전트 생성/완료 시 실행됩니다.

**입력:**
```json
{
  "agent_id": "subagent-456",
  "agent_type": "Plan"
}
```

## UI로 훅 설정

### 훅 설정 UI 열기

1. 채팅 입력에 `/hooks` 입력
2. 또는 명령 팔레트: `Chat: Configure Hooks`
3. 또는 챗 뷰 설정(기어) → 훅

### 훅 생성 흐름

1. 훅 이벤트 타입 선택
2. 새 훅 생성 또는 기존 훅 편집 선택
3. 훅 구성 파일 선택/생성
4. 명령 필드에 커서 위치

## AI로 훅 생성

`/create-hook` 명령으로 AI 생성:

```
/create-hook 모든 파일 편집 후 ESLint 실행
```

AI가 질문을 한 후 적절한 이벤트, 명령, 설정을 가진 훅 구성 파일 생성합니다.

## 에이전트 스코프 훅 (미리보기)

커스텀 에이전트의 프론트매터에서 훅 정의:

```yaml
---
name: "엄격한 포매터"
description: "모든 편집 후 자동 포매팅"
hooks:
  PostToolUse:
    - type: command
      command: "./scripts/format-changed-files.sh"
---

이 에이전트의 모든 편집 후 파일이 자동 포매팅됩니다.
```

**활성화:**
- `chat.useCustomAgentHooks: true` 설정

에이전트 스코프 훅은 해당 에이전트가 활성 또는 서브에이전트로 실행될 때만 작동합니다.

## 플러그인의 훅

### 훅 파일 위치

| 형식 | 위치 |
|------|------|
| Claude | `hooks/hooks.json` |
| Copilot | 플러그인 루트의 `hooks.json` |

VS Code가 자동으로 형식 감지합니다.

### 플러그인 경로 참조

Claude 형식 플러그인의 `${CLAUDE_PLUGIN_ROOT}` 토큰:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "${CLAUDE_PLUGIN_ROOT}/scripts/validate-tool.sh"
      }
    ]
  }
}
```

VS Code가 런타임에 절대 경로로 확장합니다.

## 실제 예제

### 예제 1: 위험한 명령 차단

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "./scripts/block-dangerous.sh"
      }
    ]
  }
}
```

**script:**
```bash
#!/bin/bash
TOOL_NAME=$1

if [[ "$TOOL_NAME" == "executeCommand" && "$COMMAND" == *"rm -rf"* ]]; then
  echo '{"continue": false, "stopReason": "파괴적인 명령 차단됨"}'
  exit 2
fi

echo '{"continue": true}'
exit 0
```

### 예제 2: 모든 편집 후 Prettier 실행

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "npx prettier --write \"$TOOL_INPUT_FILE_PATH\"",
        "timeout": 30
      }
    ]
  }
}
```

### 예제 3: 세션 시작 시 프로젝트 정보 주입

```json
{
  "hooks": {
    "SessionStart": [
      {
        "type": "command",
        "command": "./scripts/inject-context.sh"
      }
    ]
  }
}
```

**script:**
```bash
PROJECT_INFO=$(cat package.json | jq '.name, .version')
BRANCH=$(git rev-parse --abbrev-ref HEAD)

echo "{\"hookSpecificOutput\": {\"additionalContext\": \"프로젝트: $PROJECT_INFO | 브랜치: $BRANCH\"}}"
exit 0
```

## 문제 해결

### 훅이 실행되지 않음

**확인:**
1. 훅 파일이 `.github/hooks/` 또는 설정된 위치에 있나?
2. 파일이 `.json` 확장자인가?
3. `type: "command"` 설정했나?
4. 문법이 올바른가? (JSON 검증)

### 권한 거부 오류

```bash
chmod +x script.sh
```

훅 스크립트에 실행 권한 부여

### 타임아웃 오류

- `timeout` 값 증가
- 또는 스크립트 최적화

### JSON 파싱 오류

훅 스크립트가 유효한 JSON을 출력하는지 확인:

```bash
# jq로 검증
echo '...' | jq '.'
```

## 보안 고려사항

⚠️ **주의:** 훅은 VS Code와 같은 권한으로 실행됩니다.

**권장사항:**
1. 훅 스크립트 검토 (특히 공유 저장소)
2. 최소 권한 원칙 준수
3. 신뢰할 수 있는 출처에서만 훅 설치
4. 입력 검증 및 살균 필수
5. 자격증명을 하드코딩하지 말 것 (환경 변수 사용)

### 에이전트와 훅 보안

에이전트가 훅 스크립트를 편집할 수 있으면 훅을 통해 자신의 코드 실행 가능합니다.

**해결책:**
```
chat.tools.edits.autoApprove: false
```

훅 스크립트 편집에 수동 승인 필요
