# VS Code 접근성 정리

## 개요

Visual Studio Code는 접근성을 높이기 위해 화면 확대, 고대비 테마, 색각 이상 지원, 키보드 내비게이션, 스크린 리더 최적화 등 다양한 기능을 제공합니다.

## Zoom (확대/축소)

- `보기 > 모양 > 확대/축소`에서 확대/축소를 조절할 수 있습니다.
- 단축키
  - `Ctrl+=` : 확대
  - `Ctrl+-` : 축소
  - `Ctrl+Numpad0` : 확대/축소 초기화
- `window.zoomLevel` 설정에 값이 저장됩니다.
- 기본값은 `0`이고, 각 단계는 20%씩 크거나 작아집니다.
- 소수값 입력으로 미세 조정도 가능합니다.

## Accessibility Help (접근성 도움말)

- `Open Accessibility Help` 명령(`Alt+F1`)으로 현재 컨텍스트에 맞는 접근성 도움말을 표시합니다.
- 에디터, 터미널, 노트북, Chat 뷰, 인라인 채팅 등에서 사용할 수 있습니다.
- 도움말 메뉴에서 추가 문서 열기 및 도움말 닫기가 가능합니다.

## High Contrast Theme (고대비 테마)

- 모든 플랫폼에서 고대비 색상 테마를 지원합니다.
- `파일 > 기본 설정 > 테마 > 색상 테마` 또는 `Ctrl+K Ctrl+T`로 선택할 수 있습니다.

## Color Vision Accessibility (색각 이상 접근성)

- 마켓플레이스에서 색각 이상 친화적인 테마를 검색할 수 있습니다.
- `확장 보기`(`Ctrl+Shift+X`)에서 `color blind`로 검색하면 관련 테마를 찾을 수 있습니다.
- 추천 테마
  - GitHub
  - Gotthard
  - Blinds
  - Greative
  - Pitaya Smoothie

## Customizing Warning Colors (경고/오류 색상 사용자 정의)

- `settings.json`에서 `workbench.colorCustomizations`를 사용해 오류 및 경고 색상을 변경할 수 있습니다.
- 주요 설정
  - `editorError.foreground` : 오류 물결선 색상
  - `editorWarning.foreground` : 경고 물결선 색상
  - `editorError.background` : 오류 배경 색상
  - `editorWarning.background` : 경고 배경 색상
- 배경 색상을 지정하면 오류/경고 구분에 도움이 됩니다.

## Dim Unfocused Editors and Terminals (비활성 창 흐리게)

- 비활성 에디터와 터미널을 흐리게 하여 현재 포커스 위치를 쉽게 구분할 수 있습니다.
- 설정
  - `accessibility.dimUnfocused.enabled` : `true`로 설정하여 기능 사용
  - `accessibility.dimUnfocused.opacity` : 0.2에서 1 사이, 기본값은 0.75

## Keyboard navigation (키보드 내비게이션)

- 명령 팔레트(`Ctrl+Shift+P`)에서 명령을 검색하고 실행할 수 있습니다.
- `F6`와 `Shift+F6`로 워크벤치 내의 다음/이전 영역으로 포커스를 이동할 수 있습니다.
- 키보드 단축키 편집기(`파일 > 기본 설정 > 키보드 단축키` 또는 `Ctrl+K Ctrl+S`)에서 단축키를 확인하고 변경할 수 있습니다.

### Anchor selection (앵커 선택)

- 선택 시작 위치를 설정하고 커서까지 선택을 확장하는 기능입니다.
- 명령
  - `Set Selection Anchor` : `Ctrl+K Ctrl+B`
  - `Select From Anchor to Cursor` : `Ctrl+K Ctrl+K`
  - `Cancel Selection Anchor` : `Escape`
  - `Go to Selection Anchor` : 설정된 앵커 위치로 이동

## Tab navigation (탭 내비게이션)

- `Tab` 키로 UI 컨트롤 간 이동, `Shift+Tab`으로 역방향 이동이 가능합니다.
- 툴바와 탭 목록은 각각 하나의 탭 정지점만 가지고 있으며, 탭 정지점 내에서는 화살표 키로 이동합니다.
- WebView(예: Markdown 미리보기)는 시각적으로 자연스러운 순서를 따르지 않으므로 `F6`/`Shift+F6`로 이동하는 것이 더 좋습니다.

## Tab trapping (탭 트래핑)

- 기본적으로 소스 코드 파일 내에서 `Tab`은 들여쓰기 용도로 사용되며 포커스를 벗어나지 않습니다.
- `Ctrl+M`으로 Tab 트래핑을 전환할 수 있으며, 활성화 시 `Tab`이 포커스를 이동합니다.
- `editor.tabFocusMode` 설정으로 기본 동작을 제어할 수 있습니다.
- 읽기 전용 파일에서는 Tab 트래핑이 기본적으로 비활성화됩니다.
- 통합 터미널도 동일한 동작을 따릅니다.

## Screen readers (스크린 리더)

- VS Code는 화면 읽기 도구를 지원하며, 다음 도구에서 테스트되었습니다.
  - Windows: NVDA, JAWS
  - macOS: VoiceOver
  - Linux: Orca
- NVDA 사용자는 브라우즈 모드 대신 포커스 모드를 사용하는 것이 좋습니다.
- 제안 항목이 표시될 때 스크린 리더가 이를 읽어주며, `Ctrl+Up`, `Ctrl+Down`으로 이동하고 `Shift+Escape`로 닫을 수 있습니다.
- 오류 및 경고 항목은 `F8`/`Shift+F8`로 이동할 수 있습니다.
- Diff 보기에서는 `F7`/`Shift+F7`로 접근 가능한 Diff 뷰어를 사용합니다.

## Screen reader mode (스크린 리더 모드)

- VS Code는 스크린 리더 사용을 감지하면 스크린 리더 최적화 모드로 전환합니다.
- 상태 표시줄에 `Screen Reader Optimized`가 표시됩니다.
- 해당 텍스트를 클릭하거나 `Toggle Screen Reader Accessibility Mode` 명령으로 모드를 종료할 수 있습니다.
- 일부 기능(예: 접기, 미니맵)은 이 모드에서 비활성화됩니다.
- 설정값 `editor.accessibilitySupport`는 `on`, `off`, `auto`를 지원합니다.

## Resize table columns via the keyboard (표 열 크기 조정)

- `list.resizeColumn` 명령을 단축키에 할당할 수 있습니다.
- 실행 후 조정할 열을 선택하고 원하는 너비 비율을 입력합니다.

## Accessible View (접근성 뷰)

- `Open Accessible View` 명령(`Alt+F2`)으로 접근성 뷰를 열 수 있습니다.
- 문자 단위, 줄 단위로 내용을 검사할 수 있습니다.
- 호버, 알림, 코멘트, 노트북 출력, 터미널 출력, 채팅 응답, 인라인 완성, 디버그 콘솔 출력 등에서 사용할 수 있습니다.

## Input control and result navigation (입력 컨트롤 및 결과 내비게이션)

- 입력 컨트롤과 결과 사이 이동은 일관적입니다.
- `Ctrl+Down`과 `Ctrl+Up`으로 확장 보기, 키보드 단축키 편집기, 댓글, 문제, 디버그 콘솔 등의 입력과 결과를 오갈 수 있습니다.

## Terminal accessibility (터미널 접근성)

- 터미널에서 `Alt+F1`로 접근성 도움말을 표시할 수 있습니다.
- 터미널 버퍼에 접근하기 위해 `Alt+F2`를 사용할 수 있으며, 스크린 리더의 브라우즈 모드로 이동합니다.
- 셸 통합 기능으로 추가 명령을 사용할 수 있습니다.
  - `Run Recent Command`
  - `Go to Recent Directory`
  - `Go to Symbol in Accessible View` : `Ctrl+Shift+O`
- `terminal.integrated.minimumContrastRatio`는 텍스트 대비를 조정합니다.
  - 값 범위: 1~21
  - `powerline` 문자에는 적용되지 않습니다.
- `editor.tabFocusMode`로 터미널이 `Tab` 키를 받을지 여부를 제어할 수 있습니다.

## Status bar accessibility (상태 표시줄 접근성)

- 상태 표시줄에 포커스가 있을 때 `F6`로 이동한 뒤 화살표 키로 항목 간 이동이 가능합니다.

## Diff editor accessibility (Diff 편집기 접근성)

- `F7`/`Shift+F7`으로 접근 가능한 Diff 뷰어를 사용하여 변경 사항을 탐색할 수 있습니다.
- `Enter`로 선택한 줄로 돌아가고 `Escape` 또는 `Shift+Escape`로 닫을 수 있습니다.

## Debugger accessibility (디버거 접근성)

- 디버거 상태 변경이 음성으로 안내됩니다.
- 모든 디버그 작업은 키보드로 접근할 수 있습니다.
- 실행 및 디버그 뷰와 디버그 콘솔은 Tab 내비게이션을 지원합니다.
- 디버그 호버는 `Ctrl+K Ctrl+I`로 접근할 수 있습니다.
- 디버그 영역에 포커스를 이동하는 단축키를 만들 수 있습니다.
- `Debug: Add to Watch` 명령은 변수 값을 안내합니다.

## Accessibility Signals (접근성 신호)

- 커서가 이동하거나 줄에 마커가 추가되면 접근성 신호가 재생될 수 있습니다.
- `accessibility.signals.*` 설정으로 소리 및 안내를 제어할 수 있습니다.
- `Help: List Signal Sounds` 명령으로 가능한 소리를 확인하고 활성화/비활성화할 수 있습니다.
- `Help: List Signal Announcements` 명령으로 안내 메시지 목록을 확인하고 제어할 수 있습니다.

## Hover accessibility (호버 접근성)

- 일부 호버는 화면 확대/탐색기에서 사용하기 어려울 수 있습니다.
- 호버가 활성화된 상태에서 `Alt`(또는 `Option`) 키를 누르면 호버가 고정되어 사라지지 않습니다.
- 키를 놓으면 호버 잠금이 해제됩니다.

## Current known issues (현재 알려진 문제)

- macOS: VoiceOver 지원이 가능합니다.
- Linux: Orca 스크린 리더와 잘 작동합니다.
  - Orca가 에디터 내용을 읽지 않을 경우 `editor.accessibilitySupport`를 `on`으로 설정합니다.
  - 그래도 동작하지 않으면 환경 변수 `ACCESSIBILITY_ENABLED=1`을 설정해 봅니다.

## Next steps (다음 내용)

- Voice interactions: `https://code.visualstudio.com/docs/configure/accessibility/voice`
- Visual Studio Code User Interface: `https://code.visualstudio.com/docs/getstarted/userinterface`
- Basic Editing: `https://code.visualstudio.com/docs/editing/codebasics`
- Code Navigation: `https://code.visualstudio.com/docs/editing/editingevolved`
