# VSCode - 구성 (CONFIGURE)
> [from the Visual Studio Code documentation](https://code.visualstudio.com/docs/configure/locales)

## 표시 언어 (Display Language)

### 표시 언어 변경 (Changing the Display Language)

명령팔레트 - `Configure Display Language` - `ko` 선택 - 재시작

> [!NOTE]  
> `argv.json` 파일에 기록 됩니다.  
> C:\Users\사용자\\.vscode\argv.json

<br>

### (X) 사용 가능한 지역 (Available locales)

<br>

### 마켓플레이스 언어 팩 (Marketplace Language Packs)

확장 - `Korean Language Pack for Visual Studio Code`, Microsoft

<br>

### (X) 언어 설정 (Setting the Language)

VSCode 세션에서 특정 언어를 사용
> 세션 : 프로그램을 시작하고 종료할 때까지의 기간 (1회성)

```bash
code . --locale=kr
code . --locale=en
```
> [!NOTE]  
> 외부 터미널에서 사용할 수 있습니다.  
> (VS Code 내부 터미널에서는 작동하지 않습니다.)

<br>
<br>

## 레이아웃 (Layout)

### 워크벤치 (Workbench)

#### 기본 사이드바

![alt text](<../images/VSCode/구성/레이아웃/워크벤치/기본 사이드바.jpg>)

- drag and drop  
- 설정 - `workbench.sideBar.location`

#### 보조 사이드바



- drag and drop  
- 설정 - `workbench.secondarySideBar.defaultVisibility`

> [!NOTE]  
> 모든 뷰와 패널을 기본 위치로 되돌리기  
> 명령팔레트 - `View: Reset View Locations`

#### 명령 팔레트 위치

- drag and drop  
- 레이아웃 사용자 지정 버튼

#### 작업 표시줄 위치 (Activity Bar position)

보기 - 모양 - 작업 표시줄 위치





상태 표시줄