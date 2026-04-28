# VSCode - 구성 (CONFIGURE) - 레이아웃 (Layout)

> [from the Visual Studio Code documentation](https://code.visualstudio.com/docs/configure/locales)

## 워크벤치 (Workbench)

> [!NOTE]  
> 모든 뷰와 패널을 기본 위치로 되돌리기  
> 🎨 명령팔레트 - `View: Reset View Locations`

|  |  |  |
|---|---|---|
| 뷰(Views) | 작업 도구 제공 (탐색, 검색, Git 등) | 주로 사이드바에 위치 |
| 패널(Panels) | 실행/출력 결과 표시 (터미널, 로그 등) | 주로 하반에 위치 |

> [!TIP]  
> 뷰와 패널을 🖱️ Drag and Drop하여 원하는 위치로 이동할 수 있습니다.  

### 🔶 기본 사이드바

![기본 사이드바](</images/VSCode/구성/레이아웃/워크벤치/기본 사이드바.jpg>)

사이드바 위치 변경
- 🖱️ Drag and Drop  
-  [작업 표시줄]에서 마우스 🖱️오른쪽 클릭 [기본 사이드 바를 오른쪽으로 이동]
- ⚙️ 설정 - `workbench.sideBar.location`

<br>

### 🔶 보조 사이드바

![보조 사이드바](</images/VSCode/구성/레이아웃/워크벤치/보조 사이드바.jpg>)

- 🖱️ Drag and Drop  
- ⚙️ 설정 - `workbench.secondarySideBar.defaultVisibility`

<br>

### 🔶 🎨 명령 팔레트 (⌨️ `Ctrl + Shift + P`)

![명령 팔레트](</images/VSCode/구성/레이아웃/워크벤치/명령 팔레트.jpg>)

- 🖱️ Drag and Drop  
- 레이아웃 사용자 지정 버튼  
![레이아웃 사용자 지정 버튼](</images/VSCode/구성/레이아웃/워크벤치/레이아웃 사용자 지정 버튼.jpg>)  
![alt text](</images/VSCode/구성/레이아웃/워크벤치/명령 팔레트 위치 지정.jpg>)

<br>

### 🔶 작업 표시줄 (액티비티 바 Activity Bar)

![작업 표시줄(액티비티 바)](</images/VSCode/구성/레이아웃/워크벤치/작업 표시줄(액티비티 바).jpg>)

- ☰️ 보기 - 모양 - 작업 표시줄 위치
- ⚙️ 설정 - `workbench.activityBar.compact`    (작업 표시줄 크기 변경)

<br>

### 🔶 레이아웃 사용자 지정

![레이아웃 사용자 지정 버튼](</images/VSCode/구성/레이아웃/워크벤치/레이아웃 사용자 지정 버튼.jpg>)

- 전체 화면 ⌨️`F11`
- Zen 모드 ⌨️`Ctrl + K` and `Z`
- 가운데 맞춤 레이아웃

<br>

### 🔶 창 및 메뉴 스타일

|||
|--|--|
| ⚙️ window.titleBarStyle     | 제목 표시줄 스타일 |
| ⚙️ window.title             | 창 제목 표시 형식 |
| ⚙️ window.titleSeparator    | 제목 표시줄 구분 기호 표시 여부 |
| ⚙️ window.menuStyle         | 메뉴 스타일 |
| ⚙️ window.menuBarVisibility | 메뉴 표시줄 표시 여부 |

<br>
<br>

## 패널 (Panel)

![패널](/images/VSCode/구성/레이아웃/패널/패널.jpg)

### 🔶 패널 위치

☰️ 보기 - 모양 - 패널 위치

| | |
| --- | --- |
| 🎨 workbench.action.positionPanelLeft   | 패널을 왼쪽으로 이동 |
| 🎨 workbench.action.positionPanelRight  | 패널을 오른쪽으로 이동 |
| 🎨 workbench.action.positionPanelBottom | 패널을 아래로 이동 |
| 🎨 workbench.action.positionPanelTop    | 패널을 위로 이동 |

### 🔶 패널 정렬

☰️ 보기 - 모양 - 패널 맞춤

### 🔶 패널 최대화

![패널 최대화](</images/VSCode/구성/레이아웃/패널/패널 최대화.jpg>)  
패널 최대화(토글) 🎨 View: Toggle Maximized Panel

### 🔶 뷰와 패널을 드래그 앤 드롭

🖱️ Drag and Drop
뷰와 패널의 위치 이동 🎨 View: Move View

<br>
<br>

## 알림 (Notifications)

![alt text](</images/VSCode/구성/레이아웃/워크벤치/알림.jpg>)

알림 위치 변경 ⚙️ workbench.notifications.position

> [!TIP]  
> 알림 위치가 top-right로 설정된 경우, ⚙️ workbench.notifications.showInTitleBar 옵션을 사용하여 알림을 제목 표시줄에 표시할 수 있습니다.

<br>
<br>

## 툴바 (Tool bars)

![alt text](</images/VSCode/구성/레이아웃/워크벤치/툴 바.jpg>)

대부분의 보기 및 패널 UI의 오른쪽 상단에 도구 모음이 표시됩니다.

<br>
<br>

## 편집기 (Editor)

### 미니맵과 이동 경로

|  |  |
|---|---|
| ☰️ 보기 - 모양 - 미니맵 | 🎨 View: Toggle Minimap |
| ☰️ 보기 - 모양 - 이동 경로 | 🎨 View: Toggle Breadcrumbs |
| ☰️ 보기 - 모양 - 고정 스크롤 | 🎨 View: Toggle Editor Sticky Scroll |

### 에디터 그룹

☰️ 보기 - 편집기 레이아웃

- 레이아웃 대칭 이동 ⌨️ `Shift + Alt + 0`

### 그룹을 분할

🎨 .

⌨️ `Ctrl + K` and `Ctrl + Shift + \`

- 🎨 View: Split Editor in Group  
- 🎨 View: Toggle Split Editor in Group  
- 🎨 View: Join Editor in Group  
- 🎨 View: Toggle Layout of Split Editor in Group

양측 간 이동 방법:
- 🎨 View: Focus First Side in Active Editor
- 🎨 View: Focus Second Side in Active Editor
- 🎨 View: Focus Other Side in Active Editor

☰️ 보기 - 편집기 레이아웃 - 그룹으로 분할
⚙️ workbench.editor.splitInGroupLayout

### 그리드 레이아웃

편집기 레이아웃(분할과 크기조정)

### 플로팅 윈도우

편집기 창을 VSCode프로그램 바깥으로 드래그하여 플로팅 윈도우로 만들 수 있습니다.

#### 컴팩트 모드

상단 "압축 모드 켜기/끄기" 버튼을 클릭하여 편집기 탭을 컴팩트 모드로 전환할 수 있습니다.

#### 맨 위에 고정

상단 "항상 위에 표시 켜기/끄기" 버튼을 클릭하여 편집기 탭을 항상 위에 표시하도록 설정할 수 있습니다.

### 고정된 탭

탭을 마우스 오른쪽 버튼으로 클릭하여 "탭 고정"을 선택하면 해당 탭이 고정됩니다. 고정된 탭은 편집기 그룹의 왼쪽에 위치하며, 닫히지 않고 항상 표시됩니다.

### 잠긴 편집기 그룹

편집기 창 메뉴에서 "그룹 잠금"을 선택하면 해당 편집기 그룹이 잠깁니다.  
항상 표시해 두고 싶은 편집기가 하나 이상 있는 경우 유용합니다.
주된 사용 사례는 "편집기 영역의 터미널" 입니다.