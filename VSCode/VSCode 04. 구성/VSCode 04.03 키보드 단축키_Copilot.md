# VS Code 키보드 단축키 설정 가이드

원문: https://code.visualstudio.com/docs/configure/keybindings

## 1. 개요

Visual Studio Code는 강력한 키보드 단축키 편집 환경을 제공하여 마우스 없이도 대부분의 작업을 수행할 수 있습니다. 기본 단축키를 수정하거나 새로운 단축키를 추가할 수 있으며, 키보드 레이아웃에 관계없이 작동하도록 설정할 수도 있습니다.

## 2. 키보드 단축키 에디터 (Keyboard Shortcuts Editor)

### 열기
- **메뉴**: File > Preferences > Keyboard Shortcuts
- **단축키**: `Ctrl+K Ctrl+S`
- **명령**: Command Palette에서 "Preferences: Open Keyboard Shortcuts" 검색

### 기능
- 모든 사용 가능한 명령을 나열 (단축키 할당 여부와 관계없이)
- 단축키를 변경, 제거, 초기화
- 검색창에서 명령이나 단축키를 입력하여 필터링
- 키보드 레이아웃에 맞춰 단축키를 표시

예를 들어 US 키보드의 `Cmd+\`는 독일 키보드에서 `Ctrl+Shift+Alt+Cmd+7`로 표시됩니다.

## 3. UI 작업의 단축키 커스터마이징 (Customize shortcuts for UI actions)

VS Code의 UI 요소에 대한 단축키를 추가하거나 변경:

1. 작업 항목에 우클릭
2. "Configure Keybinding" 선택
3. 키보드 단축키 에디터가 해당 명령으로 필터링되어 열림
4. `when` 클로저가 자동으로 포함됨

## 4. 키맵 확장 (Keymap extensions)

다른 편집기(Vim, Emacs, Sublime Text 등)의 단축키를 VS Code에서 사용 가능하게 해주는 확장.

### 마이그레이션
1. File > Preferences > Migrate Keyboard Shortcuts from... 선택
2. 인기 있는 키맵 확장 목록 확인
3. 또는 마켓플레이스에서 "Keymaps" 카테고리에서 검색

## 5. 키보드 단축키 참조 (Keyboard Shortcuts Reference)

### 인쇄 가능한 PDF
1. Help > Keyboard Shortcut Reference 선택
2. 플랫폼별 PDF 다운로드:
   - [Windows](https://go.microsoft.com/fwlink/?linkid=832145)
   - [macOS](https://go.microsoft.com/fwlink/?linkid=832143)
   - [Linux](https://go.microsoft.com/fwlink/?linkid=832144)

## 6. 키보드 단축키 충돌 감지 (Detecting keyboard shortcut conflicts)

많은 확장을 설치했을 때 같은 단축키가 여러 명령에 할당될 수 있습니다.

### 충돌 확인
1. 키보드 단축키 에디터에서 항목에 우클릭
2. "Show Same Keybindings" 선택
3. 동일한 단축키를 사용하는 모든 항목 표시

## 7. 키보드 단축키 문제 해결 (Troubleshooting keyboard shortcuts)

### 디버깅 활성화
1. Command Palette에서 "Developer: Toggle Keyboard Shortcuts Troubleshooting" 실행
2. 단축키를 입력하면 Output 패널에서 감지 내용 확인
3. VS Code가 감지한 단축키와 실행된 명령 확인 가능

### 로그 예시
```
[KeybindingService]: / Received keydown event - modifiers: [meta], code: Slash
[KeybindingService]: | Converted keydown event - modifiers: [meta], code: Slash
[KeybindingService]: | Resolving meta+[Slash]
[KeybindingService]: \ From 2 keybinding entries, matched editor.action.commentLine
```

## 8. 수정된 단축키 보기 (Viewing modified keyboard shortcuts)

자신이 수정한 단축키만 필터링하여 표시:

1. 키보드 단축키 에디터의 ... (More Actions) 메뉴 클릭
2. "Show User Keybindings" 선택
3. `@source:user` 필터 자동 적용

## 9. 고급 커스터마이징 (Advanced customization)

### keybindings.json 파일
VS Code는 커스터마이징한 단축키를 `keybindings.json` 파일에 저장합니다. 이 파일을 직접 편집하여 고급 설정이 가능합니다.

#### 파일 열기
- 키보드 단축키 에디터 > 제목 표시줄의 "Open Keyboard Shortcuts (JSON)" 버튼
- Command Palette > "Preferences: Open Default Keyboard Shortcuts (JSON)"

## 10. 키보드 규칙 (Keyboard rules)

### 규칙 구조
각 규칙(keybinding)은 다음 속성으로 구성됩니다:

```json
{
  "key": "ctrl+f",              // 눌린 키 (필수)
  "command": "actions.find",    // 실행할 VS Code 명령 (필수)
  "when": "editorTextFocus"     // 실행 조건 (선택)
}
```

#### 키 조합 (Chords)
두 개의 연속된 키 입력은 스페이스로 구분:

```json
{ "key": "ctrl+k enter", "command": "workbench.action.keepEditor" },
{ "key": "ctrl+k ctrl+w", "command": "workbench.action.closeAllEditors" }
```

### 규칙 평가 순서
1. 규칙은 아래에서 위로 평가
2. `key`와 `when` 조건을 모두 만족하는 첫 번째 규칙이 적용
3. 일치하는 규칙이 있으면 명령 실행 후 더 이상 진행하지 않음
4. `keybindings.json`의 규칙은 기본 규칙 아래에 추가되므로 기본 규칙을 덮어쓸 수 있음

### 예시

```json
// 에디터에 포커스가 있을 때 활성
{ "key": "home", "command": "cursorHome", "when": "editorTextFocus" },
{ "key": "shift+home", "command": "cursorHomeSelect", "when": "editorTextFocus" },

// 상황에 따라 다른 명령 실행
{ "key": "f5", "command": "workbench.action.debug.continue", "when": "inDebugMode" },
{ "key": "f5", "command": "workbench.action.debug.start", "when": "!inDebugMode" },

// 전역 단축키
{ "key": "ctrl+f", "command": "actions.find" },
{ "key": "alt+left", "command": "workbench.action.navigateBack" },
{ "key": "alt+right", "command": "workbench.action.navigateForward" }
```

## 11. 허용된 키 (Accepted keys)

### 수정자 (Modifiers)
| 플랫폼 | 수정자 |
|-------|------|
| macOS | `Ctrl+`, `Shift+`, `Alt+`, `Cmd+` |
| Windows | `Ctrl+`, `Shift+`, `Alt+`, `Win+` |
| Linux | `Ctrl+`, `Shift+`, `Alt+`, `Meta+` |

### 키 (Keys)
- **함수 키**: F1-F19
- **알파벳/숫자**: a-z, 0-9
- **기호**: `` ` ``, `-`, `=`, `[`, `]`, `\`, `;`, `'`, `,`, `.`, `/`
- **이동 키**: left, up, right, down, pageup, pagedown, end, home
- **특수 키**: tab, enter, escape, space, backspace, delete
- **기타**: pausebreak, capslock, insert
- **숫자 패드**: numpad0-numpad9, numpad_multiply, numpad_add, numpad_separator, numpad_subtract, numpad_decimal, numpad_divide

## 12. 명령 인수 (Command arguments)

특정 파일이나 폴더에 대해 같은 작업을 자주 수행할 때 명령에 인수를 전달:

```json
{
  "key": "enter",
  "command": "type",
  "args": { "text": "Hello World" },
  "when": "editorTextFocus"
}
```

이 경우 Enter 키를 누르면 "Hello World"가 입력됩니다.

더 자세한 정보: [Built-in Commands](https://code.visualstudio.com/api/references/commands)

## 13. 여러 명령 실행 (Running multiple commands)

`runCommands` 명령을 사용하여 순차적으로 여러 명령 실행:

### 예시 1: 명령을 인수 없이 실행

```json
{
  "key": "ctrl+alt+c",
  "command": "runCommands",
  "args": {
    "commands": [
      "editor.action.copyLinesDownAction",
      "cursorUp",
      "editor.action.addCommentLine",
      "cursorDown"
    ]
  }
}
```

현재 줄을 복사하고, 현재 줄을 주석 처리하고, 커서를 복사된 줄로 이동합니다.

### 예시 2: 명령에 인수 전달

```json
{
  "key": "ctrl+n",
  "command": "runCommands",
  "args": {
    "commands": [
      {
        "command": "workbench.action.files.newUntitledFile",
        "args": {
          "languageId": "typescript"
        }
      },
      {
        "command": "editor.action.insertSnippet",
        "args": {
          "langId": "typescript",
          "snippet": "class ${1:ClassName} {\n\tconstructor() {\n\t\t$0\n\t}\n}"
        }
      }
    ]
  }
}
```

새로운 TypeScript 파일을 만들고 클래스 스니펫을 삽입합니다.

### 여러 인수 전달

```json
{
  "key": "ctrl+shift+e",
  "command": "runCommands",
  "args": {
    "commands": [
      {
        "command": "myCommand",
        "args": ["arg1", "arg2"]
      }
    ]
  }
}
```

배열을 첫 번째 인수로 전달하려면 배열을 다시 감싸기: `"args": [ [1, 2, 3] ]`

## 14. 단축키 제거 (Removing a keyboard shortcut)

### UI를 통해 제거
1. 키보드 단축키 에디터에서 항목에 우클릭
2. "Remove Keybinding" 선택

### keybindings.json을 통해 제거

명령 앞에 `-` 기호를 붙여 제거 규칙 생성:

```json
// 기본 단축키에서
{ "key": "tab", "command": "tab", "when": ... },
{ "key": "tab", "command": "jumpToNextSnippetPlaceholder", "when": ... },

// 두 번째 규칙을 제거하려면 keybindings.json에 추가:
{ "key": "tab", "command": "-jumpToNextSnippetPlaceholder" }
```

### 단축키 비활성화

특정 단축키를 완전히 비활성화하려면 명령을 빈 문자열로 설정:

```json
// 모든 tab 단축키를 비활성화
{ "key": "tab", "command": "" }
```

## 15. 키보드 레이아웃 (Keyboard layouts)

### UI 표시
- 모든 키보드 단축키는 현재 시스템의 키보드 레이아웃으로 렌더링됨
- 예: French (France) 레이아웃에서 `Split Editor`는 `Ctrl+*`로 표시됨

### keybindings.json 편집 시
- VS Code는 오해의 소지가 있는 단축키를 강조 표시
- 예: US 레이아웃으로 정의되었지만 현재 레이아웃에서 다른 키를 눌러야 하는 경우

### 단축키 정의 위젯
1. `keybindings.json` 편집 중 `Ctrl+K Ctrl+K` 입력
2. 원하는 키 조합 입력
3. VS Code가 JSON 표현과 감지된 키 표시
4. Enter를 눌러 규칙 스니펫 삽입

**참고**: Linux에서는 VS Code 시작 시 키보드 레이아웃을 감지하고 캐시합니다. 레이아웃 변경 후에는 VS Code를 다시 시작하는 것이 권장됩니다.

## 16. 키보드 레이아웃 독립적 바인딩 (Keyboard layout-independent bindings)

스캔 코드를 사용하면 키보드 레이아웃 변경 시에도 작동하는 단축키를 정의할 수 있습니다:

```json
{ "key": "cmd+[Slash]", "command": "editor.action.commentLine", "when": "editorTextFocus" }
```

### 허용된 스캔 코드
- **함수 키**: [F1]-[F19]
- **문자/숫자**: [KeyA]-[KeyZ], [Digit0]-[Digit9]
- **기호**: [Backquote], [Minus], [Equal], [BracketLeft], [BracketRight], [Backslash], [Semicolon], [Quote], [Comma], [Period], [Slash]
- **이동 키**: [ArrowLeft], [ArrowUp], [ArrowRight], [ArrowDown], [PageUp], [PageDown], [End], [Home]
- **특수 키**: [Tab], [Enter], [Escape], [Space], [Backspace], [Delete]
- **기타**: [Pause], [CapsLock], [Insert]
- **숫자 패드**: [Numpad0]-[Numpad9], [NumpadMultiply], [NumpadAdd], [NumpadComma], [NumpadSubtract], [NumpadDecimal], [NumpadDivide]

## 17. When 클로저 컨텍스트 (When clause contexts)

### 개념
`when` 클로저는 단축키가 활성화되는 조건을 지정하는 부울 표현식입니다.

예: F5 키는 "디버거 사용 가능 AND 디버그 모드 아님"일 때만 디버깅 시작 명령 실행:

```json
{ "key": "f5", "command": "workbench.action.debug.start", "when": "debuggersAvailable && !inDebugMode" }
```

### 조건부 연산자 (Conditional Operators)

| 연산자 | 기호 | 예시 |
|-------|------|------|
| 동일성 | `==` | `"editorLangId == typescript"` |
| 부등성 | `!=` | `"resourceExtname != .js"` |
| OR | `\|\|` | `"isLinux\|\|isWindows"` |
| AND | `&&` | `"textInputFocus && !editorReadonly"` |
| 매칭 | `=~` | `"resourceScheme =~ /^untitled$\|^file$/"` |

### 주요 컨텍스트
- `editorTextFocus`: 에디터에 텍스트 포커스가 있을 때
- `inDebugMode`: 디버그 모드일 때
- `debuggersAvailable`: 사용 가능한 디버거가 있을 때
- `resourceExtname`: 현재 파일의 확장자
- `editorLangId`: 현재 에디터의 언어 ID
- `isLinux`, `isMac`, `isWindows`: 플랫폼별 구분

더 자세한 정보: [When clause contexts reference](https://code.visualstudio.com/api/references/when-clause-contexts)

## 18. 리팩토링 커스텀 단축키 (Custom keyboard shortcuts for refactorings)

`editor.action.codeAction` 명령으로 특정 리팩토링에 단축키 할당:

```json
{
  "key": "ctrl+shift+r ctrl+e",
  "command": "editor.action.codeAction",
  "args": {
    "kind": "refactor.extract.function"
  }
}
```

더 자세한 정보: [Refactoring article](https://code.visualstudio.com/docs/editing/refactoring#_keyboard-shortcuts-for-code-actions)

## 19. 일반적인 질문 (Common questions)

### Q1: 특정 키가 어떤 명령에 할당되어 있는지 알려면?

키보드 단축키 에디터에서 단축키를 입력하여 검색하면 그 단축키에 할당된 명령이 표시됩니다.

예: `Ctrl+Shift+P`를 검색하면 "Show All Commands"를 표시합니다.

### Q2: 특정 작업에 단축키를 추가하려면? (예: Ctrl+D로 줄 삭제)

기본 키보드 단축키에서 규칙을 찾아 `keybindings.json`에 수정된 버전을 추가:

```json
// 원본 (기본 키보드 단축키)
{ "key": "ctrl+shift+k", "command": "editor.action.deleteLines", "when": "editorTextFocus" },

// 수정 (keybindings.json), Ctrl+D도 같은 작업 실행
{ "key": "ctrl+d", "command": "editor.action.deleteLines", "when": "editorTextFocus" }
```

### Q3: 특정 파일 타입에만 단축키를 적용하려면?

`when` 클로저에서 `editorLangId` 컨텍스트 사용:

```json
{ "key": "shift+alt+a", "command": "editor.action.blockComment", "when": "editorTextFocus && editorLangId == csharp" }
```

### Q4: keybindings.json에서 수정한 단축키가 작동하지 않는 이유?

일반적인 원인:
- **문법 오류**: JSON 파일의 구문 확인
- `when` 클로저 제거 시도
- 다른 `key` 조합 사용
- 충돌하는 단축키 확인

## 20. 관련 리소스

- [VS Code 기본 단축키 참조](https://code.visualstudio.com/docs/reference/default-keybindings)
- [When clause contexts reference](https://code.visualstudio.com/api/references/when-clause-contexts)
- [Built-in Commands](https://code.visualstudio.com/api/references/commands)

---

**최종 업데이트**: 2026년 5월 9일