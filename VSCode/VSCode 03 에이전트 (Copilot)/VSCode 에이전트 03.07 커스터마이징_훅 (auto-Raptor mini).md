# VS Code 에이전트 훅(Hooks)

## 개요
Hooks는 VS Code 에이전트 실행 중 특정 시점에 사용자 정의 셸 명령을 실행하는 기능입니다. 정책 강제, 자동화, 감사, 컨텍스트 주입 등 결정론적 작업에 유용합니다.

## 사용 이유
- 보안 정책 강제: 위험한 도구 호출 차단
- 자동화: 파일 편집 후 포맷터, 린터 실행
- 감사: 도구 사용 기록 로그
- 컨텍스트 주입: 프로젝트 정보나 환경 정보를 추가
- 승인 제어: 민감 작업에 확인 요구

## 빠른 시작 예제
`.github/hooks/format.json`:
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

저장하면 VS Code가 자동 로드하고 에이전트가 파일을 편집할 때마다 Prettier를 실행합니다.

## 훅 이벤트
- `SessionStart`: 새 세션 시작 시
- `UserPromptSubmit`: 사용자 프롬프트 제출 시
- `PreToolUse`: 도구 호출 전에
- `PostToolUse`: 도구 호출 후
- `PreCompact`: 대화 압축 전에
- `SubagentStart`: 서브에이전트 시작 시
- `SubagentStop`: 서브에이전트 종료 시
- `Stop`: 에이전트 세션 종료 시

## 구성 위치
- 워크스페이스: `.github/hooks/*.json`
- Claude 형식 워크스페이스: `.claude/settings.json`, `.claude/settings.local.json`
- 사용자: `~/.copilot/hooks`, `~/.claude/settings.json`
- 커스텀 에이전트: `.agent.md` frontmatter `hooks`
- 플러그인: `hooks.json` 또는 `hooks/hooks.json`

## 훅 파일 형식
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

### 명령 속성
- `type`: 항상 `command`
- `command`: 기본 명령
- `windows` / `linux` / `osx`: OS별 명령
- `cwd`: 작업 디렉토리
- `env`: 추가 환경 변수
- `timeout`: 초 단위 제한

## 입력과 출력
훅은 stdin으로 JSON 입력을 받습니다. 공통 입력 필드:
- `timestamp`
- `cwd`
- `session_id`
- `hook_event_name`
- `transcript_path`

훅은 stdout으로 JSON 출력을 반환할 수 있습니다.

공통 출력 예:
```json
{
  "continue": true,
  "stopReason": "Security policy violation",
  "systemMessage": "Unit tests failed"
}
```

### exit 코드
- `0`: 성공
- `2`: 차단 오류
- 기타: 경고

## `PreToolUse` 특수 출력
`hookSpecificOutput`을 사용해 도구 승인을 제어할 수 있습니다.
- `permissionDecision`: `allow`, `deny`, `ask`
- `permissionDecisionReason`
- `updatedInput`
- `additionalContext`

우선순위: `deny` > `ask` > `allow`

## `PostToolUse` 특수 출력
`decision: 