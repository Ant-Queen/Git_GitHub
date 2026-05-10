# VS Code 커스텀 레이아웃 설정 가이드

원문: https://code.visualstudio.com/docs/configure/custom-layout

## 1. 개요

VS Code는 기본적인 UI 레이아웃을 제공하면서도 사용자가 원하는 방식으로 커스터마이징할 수 있습니다. 사이드바, 뷰, 패널, 에디터 등을 자신의 작업 스타일에 맞게 배열할 수 있습니다.

## 2. Workbench 커스터마이징

Workbench는 VS Code의 메인 UI 레이아웃을 담당합니다.

### 2.1 Primary Side Bar (주 사이드 바)

기본적으로 화면 좌측에 위치하며 Explorer, Search, Source Control 등의 뷰를 표시합니다.

#### Primary Side Bar 위치 변경

다음 방법 중 하나로 위치를 변경:
- Activity Bar에 우클릭 > "Move Primary Side Bar Right" 선택
- Command Palette에서 "View: Toggle Primary Side Bar Position" 실행
- 메뉴에서 View > Appearance > Move Primary Side Bar Right 선택
- Settings에서 `workbench.sideBar.location`을 `right`로 설정

### 2.2 Secondary Side Bar (보조 사이드 바)

Primary Side Bar의 반대편에 위치하여 두 개의 뷰를 동시에 표시할 수 있습니다.

#### 기본 동작
- 폴더나 멀티루트 워크스페이스 열 때: 기본적으로 표시
- 빈 창: 기본적으로 숨겨짐
- `workbench.secondarySideBar.defaultVisibility` 설정으로 동작 변경

#### Secondary Side Bar 표시

다음 방법 중 하나:
- 제목 표시줄의 레이아웃 제어 버튼 클릭
- Command Palette에서 "View: Toggle Secondary Side Bar Visibility" 실행 (`Ctrl+Alt+B`)
- 메뉴에서 View > Appearance > Secondary Side Bar 선택

#### 뷰와 패널 이동

드래그 앤 드롭으로 Primary/Secondary Side Bar 사이에 뷰와 패널 이동 가능. VS Code가 레이아웃을 세션 간 저장합니다.

**참고**: "View: Reset View Locations" 명령으로 모든 뷰와 패널을 기본 위치로 재설정 가능.

### 2.3 Command Palette 위치

#### 명령 팔레트 이동
1. 명령 팔레트 상단 모서리를 마우스로 드래그
2. 또는 제목 표시줄의 "Customize Layout" 제어 버튼 클릭 후 사전 구성된 위치 선택

### 2.4 Activity Bar 위치

기본적으로 Primary Side Bar와 함께 움직이지만, 숨기거나 상단/하단으로 이동 가능합니다.

#### Activity Bar 위치 설정
- Activity Bar 컨텍스트 메뉴에서 "Activity Bar Position" 선택
- 메뉴에서 View > Appearance > Activity Bar Position 선택
- 옵션: Default, Top, Bottom, Hidden

#### 상단/하단 위치일 때
- Account와 Manage 버튼이 제목 표시줄의 우측으로 이동

### 2.5 Activity Bar 크기

두 가지 크기 옵션:
- **기본 크기**: 큰 아이콘과 레이블 (기본값)
- **Compact 크기**: 고전적인 Activity Bar 형태의 작은 아이콘

#### Activity Bar 크기 변경
- Activity Bar에 우클릭 > Activity Bar Size 메뉴에서 선택
- Settings에서 `workbench.activityBar.compact`를 `true`로 설정

**참고**: Activity Bar Size 옵션은 Activity Bar가 기본(사이드) 위치에 있을 때만 표시됩니다.

### 2.6 Customize Layout 제어 버튼

제목 표시줄의 버튼으로 주요 UI 요소(사이드바, 패널) 표시/숨기기 가능. 우측 버튼은 Customize Layout 드롭다운을 열어 더 세밀한 조정 가능.

#### 레이아웃 모드
1. **Full Screen**: 에디터가 전체 화면을 채웁니다. (View: Toggle Full Screen, `F11`)
2. **Zen Mode**: 에디터 영역만 표시하고 모든 UI 숨김 (View: Toggle Zen Mode, `Ctrl+K Z`)
3. **Centered Layout**: 에디터 영역 내에 에디터를 중앙 정렬 (View: Toggle Centered Layout)

### 2.7 Window 및 Menu 스타일

#### 관련 설정

| 설정 | 설명 |
|------|------|
| `window.titleBarStyle` | 제목 표시줄 모양: native 또는 custom (재시작 필요) |
| `window.title` | 제목 표시줄 텍스트 구성 (변수 사용 가능, 예: `${activeEditorShort}${separator}${rootName}`) |
| `window.titleSeparator` | `window.title`에 사용할 구분자 |
| `window.menuStyle` | 메뉴 스타일: native, custom, 또는 titleBarStyle 상속 (재시작 필요) |
| `window.menuBarVisibility` | 메뉴 표시줄 표시 여부 |

#### Menu Bar Visibility 옵션

| 옵션 | 설명 |
|------|------|
| `classic` | 창 상단에 표시, 전체 화면 시에만 숨김 |
| `visible` | 항상 표시 (전체 화면에서도) |
| `toggle` | 숨겨짐, Alt 키로 토글 |
| `compact` | 사이드 바로 이동 |
| `hidden` | 항상 숨겨짐 |

## 3. Panel 커스터마이징

Panel 영역은 Problems, Terminal, Output 등의 패널을 표시하며 기본적으로 에디터 영역 아래에 위치합니다.

### 3.1 Panel 위치

#### Panel 위치 변경
- 메뉴: View > Appearance > Panel Position
- Panel 제목 표시줄 컨텍스트 메뉴
- Command Palette 명령:
  - View: Move Panel Left
  - View: Move Panel Right
  - View: Move Panel To Bottom
  - View: Move Panel To Top

### 3.2 Panel 정렬 (Alignment)

Panel이 창 너비에 걸쳐 표시되는 방식을 설정합니다.

#### Panel 정렬 옵션

| 옵션 | 설명 |
|------|------|
| **Center** | Panel이 에디터 영역 너비만 차지 (기본값) |
| **Justify** | Panel이 창 전체 너비를 차지 |
| **Left** | Panel이 창 좌측 가장자리부터 에디터 우측 가장자리까지 확장 |
| **Right** | Panel이 창 우측 가장자리부터 에디터 좌측 가장자리까지 확장 |

**참고**: 모든 정렬 옵션에서 Activity Bar가 창의 끝으로 간주됩니다.

#### Panel 정렬 설정
- 메뉴: View > Appearance > Align Panel
- Panel 제목 컨텍스트 메뉴
- Command: "Set Panel Alignment to..." 명령 사용

### 3.3 Panel 크기 최대화

Panel 정렬이 Center일 때, Panel 영역 우측 상단의 chevron 버튼으로 Panel을 에디터 영역 전체로 확장 가능.

#### 최대화 제어
- 버튼 클릭으로 토글
- Command Palette: "View: Toggle Maximized Panel"

### 3.4 뷰와 패널 드래그 앤 드롭

뷰와 패널을 Primary Side Bar, Secondary Side Bar, Panel 영역 간에 드래그 앤 드롭으로 이동할 수 있습니다.

#### 예시
- Source Control 뷰를 Panel로 이동
- Problems 패널을 Primary Side Bar로 이동
- 기존 뷰 그룹에 드래그하여 새 그룹 생성

#### 키보드를 통한 이동
- Command Palette: "View: Move View" 또는 "View: Move Focused View"
- 드롭다운으로 이동할 요소와 목적지 선택

## 4. Notifications (알림)

VS Code는 기본적으로 알림 토스트와 Notification Center를 화면 우측 하단에 표시합니다.

### 4.1 알림 위치 변경

`workbench.notifications.position` 설정 (실험적):

| 위치 | 설명 |
|------|------|
| `bottom-right` | 우측 하단 (기본값), 벨 아이콘은 Status Bar |
| `bottom-left` | 좌측 하단, 벨 아이콘은 Status Bar 좌측 |
| `top-right` | 우측 상단 (OS 수준 알림과 유사), 벨 아이콘은 제목 표시줄 |

### 4.2 알림 위치 변경 방법

1. Notification Center 열기 (벨 아이콘 클릭)
2. 헤더 도구모음의 위치 아이콘 클릭
3. 원하는 위치 선택

### 4.3 제목 표시줄 벨 아이콘 제어

알림 위치가 `top-right`일 때, `workbench.notifications.showInTitleBar` 설정으로 제목 표시줄의 벨 아이콘 표시 여부 제어.

## 5. Tool bars (도구 모음)

뷰와 패널의 우측 상단에 표시되는 도구 모음을 커스터마이징할 수 있습니다.

### 5.1 도구 모음 항목 숨기기

자주 사용하지 않는 작업을 숨기려면:

1. 작업에 우클릭
2. "Hide '작업명'" 선택 (예: "Hide 'Clear Search Results'")
3. 또는 드롭다운에서 체크 해제
4. 숨겨진 작업은 "..." More Actions 메뉴로 이동

### 5.2 숨겨진 항목 복원

- 도구 모음 버튼 영역에 우클릭 > "Reset Menu" 선택
- 숨겨진 작업 재확인
- Command Palette: "View: Reset All Menus" (전체 메뉴 복원)

## 6. Editor 커스터마이징

에디터 영역의 레이아웃을 Workbench와 독립적으로 커스터마이징할 수 있습니다.

### 6.1 Minimap과 Breadcrumbs

View > Appearance 메뉴에서 다음 항목을 토글:

- **Minimap**: 현재 파일의 시각적 개요 표시 (View: Toggle Minimap)
- **Breadcrumbs**: 폴더, 파일, 현재 기호 정보 표시 (View: Toggle Breadcrumbs)
- **Sticky Scroll**: 중첩된 기호 범위 표시 (View: Toggle Sticky Scroll)

### 6.2 Editor Groups (에디터 그룹)

기본적으로 모든 에디터는 같은 그룹에 탭으로 추가됩니다. 새 그룹을 만들어 관련 파일을 정리하거나 나란히 편집할 수 있습니다.

#### 새 에디터 그룹 생성
1. 에디터를 측면으로 드래그
2. 또는 에디터 탭 컨텍스트 메뉴에서 Split 명령 선택 (좌, 우, 상, 하)
3. View > Editor Layout 메뉴
4. Command Palette

#### 에디터 그룹 레이아웃 토글
- Shift+Alt+0: 수직/수평 레이아웃 빠르게 전환

### 6.3 Split in Group (그룹 내 분할)

같은 그룹 내에서 같은 파일을 나란히 편집:

#### 명령
- View: Split Editor in Group (`Ctrl+K Ctrl+Shift+\`)
- View: Toggle Split Editor in Group: 분할 모드 토글
- View: Join Editor in Group: 단일 에디터로 복귀
- View: Toggle Layout of Split Editor in Group: 수평/수직 레이아웃 전환

#### 분할 에디터 간 이동
- View: Focus First Side in Active Editor: 첫 번째(좌측/상단) 포커스
- View: Focus Second Side in Active Editor: 두 번째(우측/하단) 포커스
- View: Focus Other Side in Active Editor: 분할 에디터 간 토글

#### 설정
- `workbench.editor.splitInGroupLayout`: 선호하는 분할 레이아웃 (horizontal 또는 vertical)

### 6.4 Grid Layout (그리드 레이아웃)

여러 행과 열의 에디터 그룹을 표시할 수 있는 고급 레이아웃:

#### Grid 레이아웃 사용
- View > Editor Layout 메뉴에서 옵션 선택 (Two Columns, Three Columns, Grid (2x2) 등)
- 그룹 간의 sash를 드래그하여 크기 조정

### 6.5 Floating Windows (부동 창)

에디터, 터미널, 또는 특정 뷰를 부동 창으로 열 수 있습니다. 다중 모니터 환경에서 유용합니다.

#### 부동 창 열기
1. 에디터를 메인 윈도우 밖으로 드래그 앤 드롭
2. 또는 에디터 탭 우클릭 > "Move into New Window" 또는 "Copy into New Window" (`Ctrl+K O`)
3. "Move Editor Group into New Window" 또는 "Copy Editor Group into New Window" (에디터 그룹 통째로)

#### 부동 창 특징
- 여러 에디터를 그리드 레이아웃으로 열 수 있음
- 재시작 후 위치와 에디터가 복원됨

#### Compact Mode (부동 창)

부동 창의 불필요한 UI 요소를 제거하여 콘텐츠 공간 확대:
- 부동 창 제목 표시줄에서 "Set Compact Mode" 선택
- 다시 클릭하여 원래 모드로 복귀

#### Pin to Top (부동 창)

부동 창을 화면 상단에 고정하여 메인 VS Code 창에서 작업하면서도 항상 표시:
- 부동 창 제목 표시줄에서 "Set Always on Top" 선택
- 다시 클릭하여 고정 해제

### 6.6 Pinned Tabs (고정 탭)

에디터 탭을 고정하면 항상 표시되고 닫히지 않습니다.

#### 탭 고정하기
- 에디터 탭 우클릭 > "Pin Editor" 또는
- Command Palette: "View: Pin Editor" (`Ctrl+K Shift+Enter`)

#### 고정 탭의 특징
- 비고정 탭보다 항상 먼저 표시
- 많은 탭이 열려도 스크롤되지 않음
- Close Others, Close All 명령으로 닫히지 않음
- 에디터 개수 제한 초과 시에도 유지

#### 고정 탭 해제
- 핀 아이콘 클릭 또는
- "Unpin editor tab" 컨텍스트 메뉴 또는
- Command: "View: Unpin Editor"

#### 고정 탭 표시 방식

`workbench.editor.pinnedTabSizing` 설정:
- `normal`: 다른 탭과 동일하게 표시 (기본값)
- `shrink`: 고정 크기로 축소되어 에디터 레이블 일부 표시
- `compact`: 아이콘 또는 첫 글자만 표시

#### 별도 행에 고정 탭 표시

`workbench.editor.pinnedTabsOnSeparateRow` 설정으로 고정 탭을 일반 탭 위의 별도 행에 표시. 두 행 간 드래그 앤 드롭으로 고정/고정 해제 가능.

### 6.7 Locked Editor Groups (잠긴 에디터 그룹)

전체 에디터 그룹을 잠가서 항상 표시되게 하고, 새 에디터는 다른 그룹에 열리게 합니다.

#### 에디터 그룹 잠금

1. 에디터 도구 모음의 More Actions "..." > "Lock Group" 선택 또는
2. Command Palette: "View: Lock Editor Group"

#### 잠긴 그룹의 동작
- 새 에디터는 잠긴 그룹에 열리지 않음 (명시적으로 이동하지 않는 한)
- 새 에디터가 잠긴 그룹을 건너뛰면 최근 사용한 잠기지 않은 그룹 또는 새 그룹에 열림
- 잠금 상태는 재시작 시 저장 및 복원됨
- 빈 그룹도 잠글 수 있음

#### 자동 잠금 그룹

`workbench.editor.autoLockGroups` 설정으로 특정 에디터 타입을 자동으로 잠금 (기본값: 터미널만).

**사용 예**: 좌측에서 텍스트 편집, 우측에 항상 표시되는 터미널.

#### 관련 명령
- View: Lock Editor Group
- View: Unlock Editor Group
- View: Toggle Editor Group Lock

**참고**: 2개 이상의 에디터 그룹이 있어야 이 명령들을 사용할 수 있습니다.

## 7. 관련 리소스

- [Visual Studio Code User Interface](https://code.visualstudio.com/docs/getstarted/userinterface) - UI 개요
- [Basic Editing](https://code.visualstudio.com/docs/editing/codebasics) - 에디터 기능
- [Code Navigation](https://code.visualstudio.com/docs/editing/editingevolved) - 코드 네비게이션

---

**최종 업데이트**: 2026년 5월 9일