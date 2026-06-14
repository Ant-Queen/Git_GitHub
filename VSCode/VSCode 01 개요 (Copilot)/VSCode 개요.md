# Visual Studio Code 상세 문서 요약 (한국어)

> **원본 사이트**: https://code.visualstudio.com/docs  
> **최종 업데이트**: 2026년 6월  
> **VS Code 버전**: v1.124 이상

이 파일은 https://code.visualstudio.com/docs 의 전체 항목을 한국어로 상세하게 정리한 종합 가이드입니다.

---

## 📑 목차

- [1. 소개](#1-소개)
- [2. 시작하기](#2-시작하기)
- [3. 사용자 인터페이스](#3-사용자-인터페이스워크벤치)
- [4. 에디터 기초](#4-에디터-기초)
- [5. 설정과 맞춤화](#5-설정과-맞춤화)
- [6. 키보드 단축키](#6-키보드-단축키)
- [7. 확장 프로그램](#7-확장프로그램extensions)
- [8. 디버깅](#8-디버깅)
- [9. 버전 관리](#9-버전-관리git)
- [10. 터미널](#10-터미널)
- [11. 작업 자동화](#11-작업-자동화)
- [12. 원격 개발](#12-원격-개발-및-컨테이너)
- [13. 언어 지원](#13-언어-및-언어-서버)
- [14. AI 에이전트](#14-ai-에이전트-및-최신-기능)
- [15. 확장 개발](#15-확장-개발자용-자료)
- [16. 명령줄 인터페이스](#16-명령줄과-통합)
- [17. 팁과 트릭](#17-팁과-트릭)
- [18. 지원 및 커뮤니티](#18-도움말-및-지원)

---

## 1. 소개

### Visual Studio Code란?

**Visual Studio Code (VS Code)** 는 Microsoft에서 만든 무료, 오픈소스 코드 편집기입니다.

#### 주요 특징
- ⚡ **경량 및 빠른 성능**: 최소한의 리소스로 빠른 실행
- 🔌 **풍부한 확장성**: 50만 개 이상의 확장 프로그램 (Marketplace)
- 🛠️ **통합 개발 도구**: 디버깅, 터미널, Git, 테스팅 내장
- 🌐 **크로스 플랫폼**: Windows, macOS, Linux 지원
- 🤖 **AI 에이전트 지원**: Copilot 및 커스텀 AI 에이전트
- 📱 **원격 개발**: SSH, WSL, Docker, Codespaces 지원
- 🎨 **아름다운 UI**: 다양한 테마 및 커스터마이징 옵션
- 📦 **설정 동기화**: Microsoft/GitHub 계정으로 설정 싱크

#### 지원 플랫폼
| 플랫폼 | 방법 | 명령어 |
|--------|------|--------|
| Windows | Microsoft Store / 공식 다운로드 | `winget install Microsoft.VisualStudioCode` |
| macOS | Homebrew / 공식 다운로드 | `brew install visual-studio-code` |
| Linux | 패키지 매니저 / 공식 다운로드 | `apt install code` (Ubuntu) |

---

## 2. 시작하기

### 2.1 설치 및 초기 설정

#### Windows 설치
1. https://code.visualstudio.com/Download 에서 다운로드
2. 설치 파일 실행 및 설치 마법사 따라가기
3. 설치 완료 후 VS Code 실행

#### macOS 설치
1. https://code.visualstudio.com/Download 에서 다운로드 (Apple Silicon 또는 Intel 선택)
2. DMG 파일 실행
3. Applications 폴더로 드래그 앤 드롭

#### Linux 설치 (Ubuntu/Debian)
```bash
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
rm -f packages.microsoft.gpg
sudo apt update
sudo apt install code
```

### 2.2 첫 실행 및 기본 설정

#### 시작 탭
- Welcome 탭에서 기본 기능 소개
- 추천 확장 프로그램 제시
- 시작 팁 및 튜토리얼

#### 초기 설정 체크리스트
```
✓ 테마 선택: 라이트 / 다크 / 커스텀
✓ 폰트 설정: 선호하는 폰트 및 크기 지정
✓ 파일 자동저장 설정
✓ 확장 프로그램 설치: Python, JavaScript 등
✓ Git 사용자 정보 설정
✓ 단축키 커스터마이징 (필요시)
```

#### 권장 초기 확장 프로그램
- **Prettier** - Code Formatter: 자동 코드 포맷팅
- **ESLint**: JavaScript 린팅
- **Python**: Python 개발 환경
- **GitLens**: Git 통합 강화
- **Thunder Client** 또는 **REST Client**: API 테스팅
- **Live Server**: 웹 개발 라이브 프리뷰

### 2.3 링크
- 📖 [공식 시작 가이드](https://code.visualstudio.com/docs/getstarted/overview)

---

## 3. 사용자 인터페이스(워크벤치)

### 3.1 주요 UI 구성 요소

#### 활동 바 (Activity Bar)
```
┌─────┐
│ 🏠  │  탐색기 (Explorer)
│ 📊  │  검색 (Search)
│ 🌳  │  소스 제어 (Source Control)
│ 🐛  │  디버그 (Debug)
│ 📦  │  확장 (Extensions)
└─────┘
```
- 좌측 세로 막대
- 다양한 보기 전환
- `Ctrl+B`로 토글

#### 사이드바 (Sidebar)
- **탐색기**: 폴더/파일 구조 표시
  - 다중 루트 워크스페이스 지원
  - 파일 검색 및 빠른 열기
  - 파일 우클릭 메뉴로 생성/삭제/이동
  
- **검색**: 전체 텍스트 검색
  - 정규표현식(Regex) 지원
  - 특정 폴더/파일 제외 기능
  - 검색/치환 일괄 처리
  
- **소스 제어**: Git 저장소 관리
  - 변경사항 스테이징
  - 커밋 메시지 작성
  - 분기 전환
  
- **디버그**: 디버깅 설정 및 실행
  - 중단점 관리
  - 변수 보기
  - 콜 스택 확인

#### 에디터 영역 (Editor Area)
- 여러 탭으로 파일 편집
- 탭 미리보기 (기울임체로 표시)
- 분할 편집 (Split Editor): `Ctrl+\`
- 사이드-바이-사이드 편집
- 그룹 레이아웃 커스터마이징

#### 상태 바 (Status Bar)
```
좌측                          우측
- 현재 분기명                - 텍스트 인코딩 (UTF-8)
- 동기화 상태                - 줄 끝 형식 (LF/CRLF)
- 오류/경고 개수            - 파일 언어 모드
                              - 줄 번호 및 열 번호
```

#### 패널 (Panel)
- **문제 (Problems)**: 오류 및 경고 목록
- **출력 (Output)**: 디버그 및 빌드 출력
- **디버그 콘솔 (Debug Console)**: 디버깅 중 명령 실행
- **터미널 (Terminal)**: 통합 터미널
- `Ctrl+J`로 토글

### 3.2 레이아웃 커스터마이징

#### 활동 바 위치 변경
```json
// settings.json
"workbench.activityBar.location": "top" // "top" | "bottom" | "hidden"
```

#### 사이드바 위치 변경
```json
"workbench.sideBar.location": "right" // "left" | "right"
```

#### 부분 화면 모드 (Zen Mode)
- `Ctrl+K Z`: Zen 모드 활성화
- 방해 요소 숨기고 집중 모드 제공
- 타이핑, 검색, 명령 팔레트 여전히 작동

### 3.3 링크
- 📖 [사용자 인터페이스 상세 가이드](https://code.visualstudio.com/docs/getstarted/userinterface)

---

## 4. 에디터 기초

### 4.1 기본 편집 기능

#### 커서 및 선택
| 기능 | 단축키 | 설명 |
|------|--------|------|
| 다중 커서 | `Ctrl+Alt+Up/Down` | 위/아래로 커서 추가 |
| 모든 일치 선택 | `Ctrl+Shift+L` | 선택 텍스트와 같은 모든 텍스트 선택 |
| 다음 일치 선택 | `Ctrl+D` | 한 번에 하나씩 일치하는 텍스트 선택 |
| 현재 줄 선택 | `Ctrl+L` | 전체 줄 선택 |
| 들여쓰기/내어쓰기 | `Tab` / `Shift+Tab` | 들여쓰기 조정 |

#### 고급 편집
| 기능 | 단축키 | 설명 |
|------|--------|------|
| 줄 이동 | `Alt+Up/Down` | 줄 위/아래로 이동 |
| 줄 복제 | `Shift+Alt+Up/Down` | 줄 복제 |
| 줄 삭제 | `Ctrl+Shift+K` | 전체 줄 삭제 |
| 주석 토글 | `Ctrl+/` | 선택 줄 주석 처리 |
| 블록 주석 | `Shift+Alt+A` | 블록 주석 처리 |

### 4.2 IntelliSense (자동완성)

**IntelliSense** 는 코드 완성, 파라미터 정보, 빠른 정보를 제공합니다.

#### 자동완성 활성화
```python
# Python 예제
import os
os.  # <- IntelliSense 자동 완성 표시
```

#### 자동완성 옵션
```json
// settings.json
"editor.quickSuggestions": {
  "other": true,
  "comments": false,
  "strings": false
},
"editor.suggestOnTriggerCharacters": true
```

#### 스니펫 사용
- `Ctrl+Shift+P` → "Insert Snippet" 검색
- 자주 사용하는 코드 템플릿 삽입
- 언어별로 다양한 기본 스니펫 제공

### 4.3 코드 네비게이션

| 기능 | 단축키 | 설명 |
|------|--------|------|
| 정의로 이동 | `F12` | 심볼의 정의 위치로 이동 |
| 선언 보기 | `Ctrl+Alt+F12` | 정의 인라인 표시 |
| 구현 보기 | `Ctrl+F12` | 구현 위치로 이동 |
| 모든 참조 찾기 | `Shift+Alt+F12` | 모든 참조 위치 표시 |
| 심볼 이름 바꾸기 | `F2` | 선택된 심볼의 모든 인스턴스 이름 변경 |

### 4.4 코드 리팩토링

| 기능 | 단축키 | 설명 |
|------|--------|------|
| 빠른 수정 | `Ctrl+.` | 자동 수정 제안 |
| 메서드 추출 | - | 선택 코드를 함수로 추출 |
| 변수 추출 | - | 선택 표현식을 변수로 추출 |
| 인라인 | - | 변수/상수 인라인 치환 |

### 4.5 검색 및 치환

#### 파일 내 검색
```
Ctrl+F        검색 상자 열기
Ctrl+H        검색 및 치환 열기
Ctrl+Shift+F  전체 폴더 검색
```

#### 고급 검색 옵션
- **정규표현식**: `.*` 패턴 지원
- **전체 단어**: 정확한 단어만 검색
- **대/소문자 구분**: 대소문자 구분 검색

#### 검색 예제
```regex
// 모든 console.log 찾기
console\.log\(.*\)

// 주석 제외하고 검색
(?!\/\/).*searchTerm
```

### 4.6 링크
- 📖 [에디터 시작 가이드](https://code.visualstudio.com/docs/editing/getting-started)

---

## 5. 설정과 맞춤화

### 5.1 설정 파일 구조

#### 설정 범위
1. **사용자 설정 (User Settings)**: 모든 프로젝트 적용
2. **작업영역 설정 (Workspace Settings)**: 현재 폴더만 적용
3. **폴더 설정 (Folder Settings)**: 다중 루트에서 특정 폴더만 적용

#### 설정 파일 위치
| 플랫폼 | 경로 |
|--------|------|
| Windows | `%APPDATA%\Code\User\settings.json` |
| macOS | `$HOME/Library/Application Support/Code/User/settings.json` |
| Linux | `$HOME/.config/Code/User/settings.json` |
| Workspace | `.vscode/settings.json` |

### 5.2 주요 설정 예제

#### 에디터 설정
```json
{
  // 폰트 및 크기
  "editor.fontFamily": "'Fira Code', 'Courier New'",
  "editor.fontSize": 14,
  "editor.fontLigatures": true,
  "editor.lineHeight": 1.6,
  
  // 줄 번호 및 렌더링
  "editor.lineNumbers": "on",
  "editor.renderLineNumbers": true,
  "editor.renderWhitespace": "boundary",
  
  // 자동 저장
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000,
  
  // 탭 및 들여쓰기
  "editor.insertSpaces": true,
  "editor.tabSize": 2,
  "editor.detectIndentation": true,
  
  // 포맷팅
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnPaste": true,
  
  // 코드 완성
  "editor.quickSuggestions": {
    "other": true,
    "comments": false,
    "strings": false
  },
  "editor.suggestOnTriggerCharacters": true,
  
  // 다른 기능
  "editor.wordWrap": "on",
  "editor.minimap.enabled": true,
  "editor.mouseWheelZoom": true
}
```

#### 파일 및 폴더 설정
```json
{
  // 파일 인코딩
  "files.encoding": "utf8",
  "files.eol": "\n",
  
  // 최종 줄 바꿈
  "files.insertFinalNewline": true,
  "files.trimFinalNewlines": true,
  "files.trimTrailingWhitespace": true,
  
  // 제외할 폴더
  "files.exclude": {
    "**/.git": true,
    "**/.vscode": false,
    "**/node_modules": true,
    "**/__pycache__": true
  },
  
  // 검색에서 제외
  "search.exclude": {
    "**/node_modules": true,
    "**/dist": true,
    "**/.git": true
  }
}
```

#### 언어별 설정
```json
{
  // Python 설정
  "[python]": {
    "editor.defaultFormatter": "ms-python.python",
    "editor.formatOnSave": true,
    "editor.tabSize": 4
  },
  
  // JavaScript 설정
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true,
    "editor.tabSize": 2
  },
  
  // JSON 설정
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true
  }
}
```

### 5.3 테마 및 아이콘 테마

#### 기본 제공 테마
- **Dark (Default dark)**: 기본 다크 테마
- **Light (Default light)**: 기본 라이트 테마
- **High Contrast**: 고대비 테마
- **Quiet Light**: 조용한 라이트 테마

#### 테마 변경
```json
{
  "workbench.colorTheme": "One Dark Pro",
  "workbench.iconTheme": "Material Icon Theme"
}
```

#### 인기 테마 및 아이콘 테마
- **드래큘라 (Dracula)**: 인기 높은 어두운 테마
- **머티리얼 테마 (Material Theme)**: Google 머티리얼 디자인 기반
- **원 다크 프로 (One Dark Pro)**: Atom 기반 다크 테마
- **머티리얼 아이콘 테마 (Material Icon Theme)**: 다양한 파일 아이콘

### 5.4 설정 동기화 (Settings Sync)

#### 활성화 방법
1. `Ctrl+Shift+P` → "Settings Sync" 검색
2. "Settings Sync: Turn On" 선택
3. Microsoft 또는 GitHub 계정으로 로그인
4. 동기화할 항목 선택

#### 동기화되는 항목
- 설정 (settings.json)
- 확장 프로그램
- 키 바인딩
- 스니펫
- UI 상태

### 5.5 링크
- 📖 [설정 및 맞춤화 상세 가이드](https://code.visualstudio.com/docs/getstarted/settings)

---

## 6. 키보드 단축키

### 6.1 필수 단축키

#### 편집 관련
| 기능 | Windows | macOS |
|------|---------|-------|
| 줄 복제 | `Shift+Alt+Up/Down` | `Shift+Option+Up/Down` |
| 줄 이동 | `Alt+Up/Down` | `Option+Up/Down` |
| 줄 삭제 | `Ctrl+Shift+K` | `Cmd+Shift+K` |
| 줄 추가 | `Ctrl+Shift+Enter` | `Cmd+Shift+Enter` |
| 주석 토글 | `Ctrl+/` | `Cmd+/` |
| 블록 주석 | `Shift+Alt+A` | `Shift+Option+A` |
| 들여쓰기 | `Tab` | `Tab` |
| 내어쓰기 | `Shift+Tab` | `Shift+Tab` |

#### 네비게이션 관련
| 기능 | Windows | macOS |
|------|---------|-------|
| 파일 열기 | `Ctrl+P` | `Cmd+P` |
| 기호 이동 | `Ctrl+Shift+O` | `Cmd+Shift+O` |
| 줄 이동 | `Ctrl+G` | `Cmd+G` |
| 에디터 전환 | `Ctrl+Tab` | `Cmd+Tab` |
| 사이드바 토글 | `Ctrl+B` | `Cmd+B` |
| 터미널 토글 | `Ctrl+` | `Ctrl+` ` |

#### 검색 관련
| 기능 | Windows | macOS |
|------|---------|-------|
| 파일 검색 | `Ctrl+F` | `Cmd+F` |
| 검색 및 치환 | `Ctrl+H` | `Cmd+Option+F` |
| 전체 폴더 검색 | `Ctrl+Shift+F` | `Cmd+Shift+F` |
| 다음 찾기 | `F3` | `Cmd+G` |
| 이전 찾기 | `Shift+F3` | `Cmd+Shift+G` |

#### 명령 관련
| 기능 | Windows | macOS |
|------|---------|-------|
| 명령 팔레트 | `Ctrl+Shift+P` | `Cmd+Shift+P` |
| 문제 패널 | `Ctrl+Shift+M` | `Cmd+Shift+M` |
| 디버그 콘솔 | `Ctrl+Shift+Y` | `Cmd+Shift+Y` |

### 6.2 단축키 커스터마이징

#### 단축키 설정 파일 열기
```
Ctrl+K Ctrl+S  (또는 Preferences: Open Keyboard Shortcuts)
```

#### keybindings.json 편집 예제
```json
[
  {
    "key": "ctrl+shift+n",
    "command": "workbench.action.files.newUntitledFile"
  },
  {
    "key": "ctrl+alt+t",
    "command": "workbench.action.toggleActivityBarVisibility"
  },
  {
    "key": "ctrl+shift+d",
    "command": "editor.action.deleteLines",
    "when": "editorTextFocus"
  },
  {
    "key": "ctrl+l",
    "command": "editor.action.selectAll",
    "when": "!editorTextFocus"
  }
]
```

#### 조건부 단축키
```json
{
  "key": "F5",
  "command": "workbench.action.debug.start",
  "when": "!inDebugMode"
},
{
  "key": "F5",
  "command": "workbench.action.debug.continue",
  "when": "inDebugMode"
}
```

### 6.3 링크
- 📖 [키보드 단축키 상세 가이드](https://code.visualstudio.com/docs/getstarted/keybindings)

---

## 7. 확장(프로그램)(Extensions)

### 7.1 확장 프로그램 설치 및 관리

#### 설치 방법

**방법 1: UI를 통한 설치**
1. 좌측 활동 바에서 확장(Extensions) 아이콘 클릭
2. 검색창에 확장 프로그램명 입력
3. "설치" 버튼 클릭
4. 필요시 VS Code 재실행

**방법 2: 명령 팔레트를 통한 설치**
```
Ctrl+Shift+P → "Extensions: Install Extensions" → 검색어 입력
```

**방법 3: 명령줄을 통한 설치**
```bash
code --install-extension <Publisher>.<Extension>
code --install-extension ms-python.python
code --install-extension esbenp.prettier-vscode
```

### 7.2 추천 확장 프로그램 (필수)

#### 🎨 코드 포맷팅 및 스타일
- **Prettier - Code formatter** (`esbenp.prettier-vscode`)
  - 자동 코드 포맷팅
  - JavaScript, TypeScript, CSS, JSON 등 지원
  
- **ESLint** (`dbaeumer.vscode-eslint`)
  - JavaScript/TypeScript 린팅
  - 오류 및 경고 자동 표시
  - 자동 수정 기능

#### 🐍 Python 개발
- **Python** (`ms-python.python`)
  - Python 인터프리터 관리
  - IntelliSense 및 린팅
  - 디버깅 및 테스팅
  
- **Pylance** (`ms-python.vscode-pylance`)
  - 향상된 Python 타입 체크
  - IntelliSense 성능 개선

#### 🔧 개발 도구
- **GitLens** (`eamodio.gitlens`)
  - Git 히스토리 시각화
  - 코드 저자 정보 표시
  - 분기 관리 및 비교
  
- **REST Client** (`humao.rest-client`)
  - HTTP 요청 테스팅
  - .http 파일로 API 테스트
  
- **Thunder Client** (`rangav.vscode-thunder-client`)
  - Postman 대체 API 테스팅 도구

#### 🌐 웹 개발
- **Live Server** (`ritwickdey.liveserver`)
  - 라이브 리로드 웹 서버
  - HTML/CSS/JavaScript 개발
  
- **HTML CSS Support** (`ecmel.vscode-html-css`)
  - HTML 및 CSS 자동완성
  
- **Thunder Client**: API 테스팅

#### 📝 문서 및 마크다운
- **Markdown Preview Enhanced** (`shd101wyy.markdown-preview-enhanced`)
  - 향상된 마크다운 미리보기
  - 다이어그램 및 수학 수식 지원
  
- **Markdown All in One** (`yzhang.markdown-all-in-one`)
  - 마크다운 작성 기능 강화
  - 목차 자동 생성

#### 🎯 생산성
- **Todo Tree** (`gruntfuggly.todo-tree`)
  - TODO, FIXME 등 주석 추적
  
- **Better Comments** (`aaron-bond.better-comments`)
  - 주석 색상 구분
  
- **Bookmarks** (`alefragnani.bookmarks`)
  - 중요한 줄 북마크

### 7.3 확장 프로그램 관리

#### 비활성화 및 제거
- 확장 패널에서 확장 우클릭
- "비활성화 (Disable)" 또는 "제거 (Uninstall)" 선택

#### 작업영역별 확장 권장
- 확장 페이지 → "권장" 탭
- `extensions.json` 작성:

```json
// .vscode/extensions.json
{
  "recommendations": [
    "ms-python.python",
    "esbenp.prettier-vscode",
    "dbaeumer.vscode-eslint",
    "eamodio.gitlens"
  ]
}
```

#### 확장 프로그램 비활성화 조건
```json
// settings.json
"extensions.ignoreRecommendations": false
```

### 7.4 링크
- 📖 [확장 프로그램 상세 가이드](https://code.visualstudio.com/docs/editor/extension-marketplace)
- 🔗 [VS Code Marketplace](https://marketplace.visualstudio.com/VSCode)

---

## 8. 디버깅

### 8.1 디버깅 기본 개념

#### 중단점 (Breakpoint)
- **설정**: 줄 번호 좌측 클릭 또는 `F9`
- **조건부 중단점**: 우클릭 → "중단점 추가"
- **로그 포인트**: 메시지 출력하고 계속 실행

#### 디버그 세션
1. `.vscode/launch.json` 설정 파일 생성
2. 디버그 구성 추가
3. `F5` 또는 "디버그 시작" 클릭
4. 중단점에서 실행 중지

### 8.2 launch.json 구성

#### Python 디버깅
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: Current File",
      "type": "python",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal",
      "justMyCode": true
    },
    {
      "name": "Python: Flask",
      "type": "python",
      "request": "launch",
      "module": "flask",
      "env": {"FLASK_APP": "app.py"},
      "args": ["run"],
      "jinja": true
    }
  ]
}
```

#### JavaScript/Node.js 디버깅
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Node.js: Launch",
      "type": "node",
      "request": "launch",
      "program": "${workspaceFolder}/index.js",
      "console": "integratedTerminal"
    },
    {
      "name": "Node.js: Attach",
      "type": "node",
      "request": "attach",
      "port": 9229
    }
  ]
}
```

#### C++ 디버깅
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "C++: GDB Launch",
      "type": "cppdbg",
      "request": "launch",
      "program": "${workspaceFolder}/a.out",
      "args": [],
      "stopAtEntry": false,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "externalConsole": true,
      "MIMode": "gdb",
      "setupCommands": [
        {
          "description": "Enable pretty-printing",
          "text": "-enable-pretty-printing",
          "ignoreFailures": true
        }
      ]
    }
  ]
}
```

### 8.3 디버그 명령 및 단축키

| 기능 | 단축키 | 설명 |
|------|--------|------|
| 디버그 시작 | `F5` | 디버깅 시작 |
| 계속 | `F5` | 다음 중단점까지 계속 실행 |
| 한 줄 실행 | `F10` | 다음 줄 실행 (함수 호출 건너뜀) |
| 한 단계 실행 | `F11` | 다음 줄 실행 (함수 내부로 들어감) |
| 한 단계 나오기 | `Shift+F11` | 현재 함수 탈출 |
| 디버그 중지 | `Shift+F5` | 디버깅 종료 |
| 다시 시작 | `Ctrl+Shift+F5` | 디버깅 다시 시작 |

### 8.4 디버그 뷰

#### 변수 (Variables)
- 지역 변수 (Local)
- 전역 변수 (Global)
- 변수 값 확인 및 수정

#### 조사식 (Watch)
- 특정 변수/표현식 지속적 모니터링
- 값 변화 감지
- 조건식 평가

#### 콜 스택 (Call Stack)
- 함수 호출 스택 시각화
- 각 스택 프레임 클릭으로 이동
- 함수 호출 경로 파악

#### 중단점 (Breakpoints)
- 모든 중단점 목록
- 조건 확인 및 수정
- 중단점 활성화/비활성화

### 8.5 링크
- 📖 [디버깅 상세 가이드](https://code.visualstudio.com/docs/editor/debugging)

---

## 9. 버전 관리(Git)

### 9.1 Git 기본 통합

#### Git 설정 확인
```bash
git --version        # Git 설치 확인
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

### 9.2 소스 제어 패널

#### 주요 기능
- **변경사항 표시**: 추적 (Changes), 스테이지됨 (Staged Changes)
- **커밋**: 스테이지된 파일로 커밋 생성
- **분기**: 분기 생성, 전환, 삭제
- **비교**: 변경사항 상세 비교

#### 패널 접근
- 좌측 활동 바의 소스 제어 아이콘 클릭
- `Ctrl+Shift+G`로 빠르게 열기

### 9.3 주요 Git 작업

#### 저장소 초기화 및 클론
```
Ctrl+Shift+P → "Git: Initialize Repository" 또는 "Git: Clone"
```

#### 파일 스테이징
- 파일 좌측의 "+" 아이콘 클릭
- 전체 파일 스테이징
- 부분 선택 스테이징

#### 커밋 작성
1. 메시지 입력창에 커밋 메시지 작성
2. `Ctrl+Enter` 또는 커밋 버튼 클릭
3. 커밋 생성

#### 분기 관리
```
Ctrl+Shift+P → "Git: Create Branch" / "Git: Checkout to..."
```

#### Push / Pull
```
상태 바의 분기명 우클릭 → "Push to" / "Pull from"
또는 Ctrl+Shift+P → "Git: Push" / "Git: Pull"
```

### 9.4 GitLens 확장 (권장)

**고급 Git 기능 제공:**
- 코드 작성자 정보 (Blame)
- 커밋 히스토리 시각화
- 분기 비교
- 파일 히스토리 탐색

### 9.5 병합 및 충돌 해결

#### 충돌 표시
```
<<<<<<< HEAD (현재 분기)
변경사항 1
=======
변경사항 2
>>>>>>> feature-branch
```

#### 해결 방법
1. 충돌 부분 클릭
2. "Current Change" 또는 "Incoming Change" 선택
3. 또는 수동으로 편집
4. 스테이징 및 커밋

### 9.6 링크
- 📖 [버전 관리 상세 가이드](https://code.visualstudio.com/docs/editor/versioncontrol)

---

## 10. 터미널

### 10.1 통합 터미널 기본

#### 터미널 열기
- `Ctrl+` ` (Grave/물음표 키)
- 좌측 하단 패널의 터미널 탭 클릭
- `Ctrl+Shift+P` → "Toggle Integrated Terminal"

#### 셸 선택
- Windows: PowerShell, Cmd, Git Bash, WSL
- macOS: Bash, Zsh
- Linux: Bash, Zsh, Fish 등

#### 셸 변경
```json
// settings.json
"terminal.integrated.defaultProfile.windows": "PowerShell",
"terminal.integrated.defaultProfile.linux": "bash",
"terminal.integrated.defaultProfile.osx": "zsh"
```

### 10.2 터미널 커스터마이징

#### 폰트 및 크기
```json
{
  "terminal.integrated.fontFamily": "'Fira Code'",
  "terminal.integrated.fontSize": 12,
  "terminal.integrated.lineHeight": 1.2
}
```

#### 색상 및 테마
```json
{
  "terminal.integrated.inheritEnv": true,
  "terminal.integrated.env.windows": {
    "CUSTOM_VAR": "value"
  }
}
```

### 10.3 터미널 분할

#### 새 터미널
- `Ctrl+Shift+` ` → 새 터미널 생성
- `Ctrl+Shift+5` → 터미널 분할

#### 터미널 전환
- `Ctrl+PageDown` / `Ctrl+PageUp`
- 터미널 탭 클릭

### 10.4 링크
- 📖 [터미널 상세 가이드](https://code.visualstudio.com/docs/editor/integrated-terminal)

---

## 11. 작업 자동화

### 11.1 작업(Tasks) 소개

`.vscode/tasks.json` 파일로 빌드, 테스트, 배포 등을 자동화합니다.

### 11.2 작업 정의 예제

#### 기본 구조
```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "echo",
      "type": "shell",
      "command": "echo",
      "args": ["Hello World"],
      "group": {
        "kind": "build",
        "isDefault": true
      }
    }
  ]
}
```

#### Python 예제
```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Run Python File",
      "type": "shell",
      "command": "python",
      "args": ["${file}"],
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "problemMatcher": [],
      "presentation": {
        "echo": true,
        "reveal": "always",
        "focus": false,
        "panel": "shared"
      }
    },
    {
      "label": "Run Pytest",
      "type": "shell",
      "command": "pytest",
      "args": ["${workspaceFolder}/tests"],
      "group": "test"
    }
  ]
}
```

#### Node.js 예제
```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "npm build",
      "type": "shell",
      "command": "npm",
      "args": ["run", "build"],
      "group": {
        "kind": "build",
        "isDefault": true
      }
    },
    {
      "label": "npm test",
      "type": "shell",
      "command": "npm",
      "args": ["test"],
      "group": "test"
    }
  ]
}
```

### 11.3 작업 실행

#### 명령 팔레트
```
Ctrl+Shift+P → "Tasks: Run Task" → 원하는 작업 선택
```

#### 단축키
```
Ctrl+Shift+B   기본 빌드 작업 실행
```

### 11.4 링크
- 📖 [작업 자동화 상세 가이드](https://code.visualstudio.com/docs/editor/tasks)

---

## 12. 원격 개발 및 컨테이너

### 12.1 Remote 확장 설치

필수 확장 프로그램:
- **Remote - SSH** (`ms-vscode-remote.remote-ssh`)
- **Remote - WSL** (`ms-vscode-remote.remote-wsl`)
- **Dev Containers** (`ms-vscode-remote.remote-containers`)

### 12.2 SSH 원격 개발

#### SSH 설정
1. `.ssh/config` 파일 생성 (또는 기존 파일 수정)

```
Host myserver
    HostName 192.168.1.100
    User username
    IdentityFile ~/.ssh/id_rsa
    Port 22
```

2. VS Code 팔레트에서 "Remote-SSH: Connect to Host..."
3. 호스트 선택 및 연결

#### 원격 폴더 열기
- 원격 연결 후 "File → Open Folder"로 원격 폴더 선택

### 12.3 WSL (Windows Subsystem for Linux)

#### WSL 설정
1. Windows 11/10에서 WSL2 설치
2. Linux 배포판 설치 (Ubuntu, Debian 등)
3. VS Code에서 "Remote-WSL: New WSL Window"

#### WSL 폴더 열기
```bash
# WSL 터미널에서
code /path/to/folder
```

### 12.4 Dev Containers (Docker)

#### devcontainer.json 설정
```json
{
  "name": "Python Dev Container",
  "image": "mcr.microsoft.com/devcontainers/python:3.11",
  "features": {
    "ghcr.io/devcontainers/features/git:1": {},
    "ghcr.io/devcontainers/features/github-cli:1": {}
  },
  "postCreateCommand": "pip install -r requirements.txt",
  "customizations": {
    "vscode": {
      "extensions": [
        "ms-python.python",
        "ms-python.vscode-pylance"
      ]
    }
  }
}
```

#### 컨테이너에서 개발
1. 워크스페이스에 `.devcontainer/devcontainer.json` 생성
2. `Ctrl+Shift+P` → "Dev Containers: Reopen in Container"
3. 컨테이너 빌드 및 연결

### 12.5 GitHub Codespaces

#### Codespaces 시작
1. GitHub 저장소에서 "Code → Codespaces → Create Codespace"
2. 브라우저 또는 VS Code에서 열기
3. 클라우드 기반 개발 환경 사용

### 12.6 링크
- 📖 [원격 개발 상세 가이드](https://code.visualstudio.com/docs/remote/remote-overview)

---

## 13. 언어 및 언어 서버

### 13.1 언어 지원 확장

#### Python
- **확장**: Python (`ms-python.python`)
- **기능**: IntelliSense, 디버깅, 테스팅, Linting
- **권장**: Pylance, Black, Flake8

#### JavaScript / TypeScript
- **내장**: 기본 지원
- **권장**: ESLint, Prettier, Thunder Client

#### C/C++
- **확장**: C/C++ Extension Pack
- **기능**: IntelliSense, 디버깅, CMake 통합
- **권장**: Clang, GCC

#### Java
- **확장**: Extension Pack for Java
- **기능**: IntelliSense, 디버깅, Maven/Gradle 지원
- **권장**: Spring Boot Extensions

#### Go
- **확장**: Go (`golang.go`)
- **기능**: IntelliSense, 포맷팅, 테스팅, 디버깅

#### Rust
- **확장**: rust-analyzer (`rust-lang.rust-analyzer`)
- **기능**: IntelliSense, 포맷팅, 린팅

### 13.2 Language Server Protocol (LSP)

**LSP** 는 에디터와 언어 서버 간 통신 프로토콜입니다.

#### LSP 기능
- 자동완성 (Completion)
- 정의 이동 (Go to Definition)
- 참조 찾기 (Find References)
- 이름 변경 (Rename)
- 포맷팅 (Formatting)
- 호버 정보 (Hover Information)
- 진단 (Diagnostics)

### 13.3 링크
- 📖 [언어별 지원 상세 가이드](https://code.visualstudio.com/docs/languages/overview)

---

## 14. AI 에이전트 및 최신 기능

### 14.1 AI 에이전트 개요

자율 AI 에이전트는 복잡한 작업을 자동으로 수행합니다.

#### 에이전트 종류

1. **로컬 에이전트**: 로컬 머신에서 실행
2. **Copilot CLI**: 커맨드라인 인터페이스
3. **클라우드 에이전트**: 클라우드에서 실행
4. **서드파티 에이전트**: 외부 제공자의 에이전트

### 14.2 Copilot Chat

#### 활성화
1. Copilot Chat 확장 설치
2. `Ctrl+Shift+I`로 실행
3. 자연어 질문 입력

#### 기능
- 코드 설명 및 작성
- 버그 수정 제안
- 테스트 코드 생성
- 리팩토링 조언

### 14.3 AI 커스터마이징

#### 커스텀 인스트럭션 설정
- `.instructions.md` 파일로 AI 동작 정의
- 프로젝트별 AI 규칙 설정
- 개인 스타일 반영

### 14.4 브라우저 에이전트 테스팅

통합 브라우저를 통한 자동 테스트:
- UI 자동화
- E2E 테스트
- 스크린샷 기반 검증

### 14.5 최신 업데이트 (v1.124)

- **Autopilot 기본 활성화**: 자동 AI 보조 기능
- **빠른 에이전트 세션 네비게이션**: 세션 간 빠른 전환
- **Copilot CLI 원격 제어 (실험)**: GitHub.com에서 세션 모니터링

### 14.6 링크
- 📖 [AI 에이전트 상세 가이드](https://code.visualstudio.com/docs/agents/overview)

---

## 15. 확장 개발자용 자료

### 15.1 확장 API

VS Code 확장은 JavaScript/TypeScript로 개발합니다.

#### 기본 구조
```javascript
const vscode = require('vscode');

function activate(context) {
  console.log('Extension activated!');
  
  let disposable = vscode.commands.registerCommand(
    'extension.helloWorld',
    () => {
      vscode.window.showInformationMessage('Hello World!');
    }
  );
  
  context.subscriptions.push(disposable);
}

function deactivate() {}

module.exports = { activate, deactivate };
```

#### 주요 API
- **Commands**: 명령 등록 및 실행
- **StatusBar**: 상태 바 아이템 추가
- **TreeView**: 트리 보기 추가
- **WebView**: 커스텀 UI 생성
- **LanguageClient**: LSP 구현

### 15.2 발행 및 배포

1. **Marketplace 등록**
   - https://marketplace.visualstudio.com/manage
   - 게시자 계정 생성

2. **확장 패키징**
   ```bash
   npm install -g vsce
   vsce package
   ```

3. **게시**
   ```bash
   vsce publish
   ```

### 15.3 링크
- 📖 [확장 API 상세 가이드](https://code.visualstudio.com/api)

---

## 16. 명령줄과 통합

### 16.1 code CLI 명령어

#### 기본 사용법
```bash
code                       # VS Code 실행
code .                     # 현재 폴더 열기
code /path/to/folder       # 특정 폴더 열기
code file.txt              # 파일 열기
```

#### 편집 옵션
```bash
code --new-window          # 새 창에서 열기
code --reuse-window        # 기존 창에서 열기
code --wait                # 파일 편집 완료까지 대기
code -g file.txt:10:5      # 파일, 줄, 열 지정
```

#### 확장 프로그램 관리
```bash
code --install-extension ms-python.python
code --uninstall-extension ms-python.python
code --list-extensions     # 설치된 확장 목록
```

#### 개발자 옵션
```bash
code --no-sandbox          # 샌드박스 비활성화
code --disable-extensions  # 확장 비활성화
code --verbose             # 상세 로그 출력
```

### 16.2 link 기능

VS Code URI로 파일/설정 열기:
```
vscode://file/c:/path/to/file.txt
vscode://file/c:/path/to/file.txt:10:5
vscode://settings
vscode://extensions
```

### 16.3 링크
- 📖 [명령줄 상세 가이드](https://code.visualstudio.com/docs/editor/command-line)

---

## 17. 팁과 트릭

### 17.1 생산성 팁

#### 1. 빠른 파일 이동 및 열기
```
Ctrl+P              파일 빠른 열기
@                   기호로 필터링
#                   워크스페이스 기호
```

#### 2. 다중 선택 및 편집
```
Ctrl+D              다음 일치하는 텍스트 선택
Ctrl+Shift+L        모든 일치하는 텍스트 선택
Ctrl+Alt+Up/Down    위/아래에 커서 추가
```

#### 3. 코드 이동 및 복제
```
Alt+Up/Down         줄 이동
Shift+Alt+Up/Down   줄 복제
```

#### 4. 리팩토링
```
F2                  이름 변경
Ctrl+Shift+R        검색 및 치환 (정규표현식)
Ctrl+.              빠른 수정 제안
```

#### 5. 커맨드 팔레트 활용
```
Ctrl+Shift+P        명령 팔레트 (거의 모든 기능 접근)
```

### 17.2 성능 최적화

#### 확장 프로그램 정리
- 사용하지 않는 확장 비활성화
- 불필요한 언어 서버 제거

#### 워크스페이스 최적화
```json
{
  "search.exclude": {
    "**/node_modules": true,
    "**/.git": true
  },
  "files.exclude": {
    "**/__pycache__": true
  }
}
```

#### 소스 제어 최적화
- 큰 저장소에서는 Git 작업 제한

### 17.3 유용한 확장 조합

#### 웹 개발 스택
- Prettier, ESLint, Live Server, REST Client

#### Python 개발 스택
- Python, Pylance, Black, Pylint, Pytest

#### 생산성 스택
- GitLens, Todo Tree, Better Comments, Bookmarks

### 17.4 워크스페이스 설정 최적화

#### 프로젝트별 설정 (`.vscode/settings.json`)
```json
{
  "python.linting.enabled": true,
  "python.linting.pylintEnabled": true,
  "[python]": {
    "editor.tabSize": 4,
    "editor.defaultFormatter": "ms-python.python",
    "editor.formatOnSave": true
  },
  "search.exclude": {
    "**/venv": true,
    "**/.git": true
  }
}
```

---

## 18. 도움말 및 지원

### 18.1 공식 리소스

| 리소스 | 주소 |
|--------|------|
| 공식 문서 | https://code.visualstudio.com/docs |
| GitHub 저장소 | https://github.com/microsoft/vscode |
| Marketplace | https://marketplace.visualstudio.com/VSCode |
| Issues / 버그 보고 | https://github.com/microsoft/vscode/issues |
| FAQ | https://code.visualstudio.com/docs/supporting/faq |

### 18.2 커뮤니티 지원

- **Stack Overflow**: [vs code 태그](https://stackoverflow.com/questions/tagged/vscode)
- **Reddit**: https://www.reddit.com/r/vscode/
- **Discord**: VS Code 커뮤니티 서버
- **GitHub Discussions**: VS Code 저장소의 토론

### 18.3 버그 신고 및 기능 요청

#### GitHub Issues 활용
1. https://github.com/microsoft/vscode/issues 방문
2. 유사한 이슈 검색
3. 없으면 새로운 이슈 작성
4. 자세한 설명 및 재현 방법 제시

### 18.4 링크
- 📖 [FAQ](https://code.visualstudio.com/docs/supporting/faq)
- 🔗 [공식 GitHub Issues](https://github.com/microsoft/vscode/issues)

---

## 부록

### A. 유용한 단축키 요약 (Windows)

**자주 사용되는 필수 단축키:**

```
Ctrl+P          파일 빠른 열기
Ctrl+Shift+P    명령 팔레트
Ctrl+/          주석 토글
Ctrl+K Ctrl+C   블록 주석
Ctrl+K Ctrl+U   블록 주석 해제
Ctrl+H          검색 및 치환
Ctrl+F          검색
Ctrl+G          줄 이동
F12             정의로 이동
Ctrl+Shift+O    기호 이동
F5              디버그 시작
Ctrl+Shift+B    빌드 작업 실행
Ctrl+Shift+M    문제 패널
Ctrl+B          사이드바 토글
Ctrl+J          패널 토글
Ctrl+` `        터미널 토글
Alt+Up/Down     줄 이동
Shift+Alt+Up/Down  줄 복제
Ctrl+D          다음 일치 선택
Ctrl+Shift+L    모든 일치 선택
```

### B. 일반적인 문제 해결

#### Q: VS Code가 느립니다
**A**: 
- 불필요한 확장 비활성화
- 큰 폴더 검색 제외
- 편집기 미니맵 비활성화

#### Q: Git 동기화가 안 됩니다
**A**:
- SSH 키 설정 확인
- 인증 정보 다시 입력
- GitLens 확장으로 디버깅

#### Q: Python IntelliSense가 작동하지 않습니다
**A**:
- Python 확장 설치 확인
- Python 인터프리터 경로 설정
- Pylance 확장 설치

#### Q: 터미널이 기본 셸로 열리지 않습니다
**A**:
- `settings.json`에서 기본 프로필 설정
- 터미널 설정 확인
- VS Code 재실행

### C. 추천 설정 모음 (최적화된 settings.json)

```json
{
  // 에디터 기본 설정
  "editor.fontSize": 14,
  "editor.fontFamily": "'Fira Code', 'Courier New'",
  "editor.fontLigatures": true,
  "editor.lineHeight": 1.6,
  "editor.tabSize": 2,
  "editor.insertSpaces": true,
  "editor.trimAutoWhitespace": true,
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  
  // 자동 저장
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000,
  "files.eol": "\n",
  "files.insertFinalNewline": true,
  "files.trimTrailingWhitespace": true,
  
  // 검색 제외
  "search.exclude": {
    "**/node_modules": true,
    "**/.git": true,
    "**/dist": true
  },
  "files.exclude": {
    "**/__pycache__": true,
    "**/*.pyc": true
  },
  
  // 언어별 설정
  "[python]": {
    "editor.tabSize": 4,
    "editor.defaultFormatter": "ms-python.python"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true
  },
  
  // 터미널
  "terminal.integrated.fontSize": 12,
  "terminal.integrated.lineHeight": 1.2,
  
  // 테마
  "workbench.colorTheme": "One Dark Pro",
  "workbench.iconTheme": "Material Icon Theme",
  
  // 기타
  "editor.minimap.enabled": true,
  "editor.renderWhitespace": "boundary",
  "editor.wordWrap": "on"
}
```

---

## 최종 정보

| 항목 | 정보 |
|------|------|
| **공식 사이트** | https://code.visualstudio.com |
| **다운로드** | https://code.visualstudio.com/Download |
| **문서** | https://code.visualstudio.com/docs |
| **마켓플레이스** | https://marketplace.visualstudio.com/VSCode |
| **GitHub** | https://github.com/microsoft/vscode |
| **라이선스** | MIT |
| **지원** | Windows, macOS, Linux |

**이 문서는 계속 업데이트됩니다.**  
**마지막 수정**: 2026년 6월 14일

## 시작하기
- 설치 및 기본 설정: Windows/macOS/Linux 설치 안내 및 첫 실행 가이드
- 링크: https://code.visualstudio.com/docs/getstarted/overview

## 에디터 기초
- 편집기 기능: 파일 편집, 다중 커서, 코드 완성, IntelliSense
- 링크: https://code.visualstudio.com/docs/editing/getting-started

## 사용자 인터페이스(워크벤치)
- 사이드바, 상태바, 패널, 액티비티 바 등 UI 구성 요소 설명 및 사용법
- 링크: https://code.visualstudio.com/docs/getstarted/userinterface

## 설정과 맞춤화
- 사용자/작업영역 설정, JSON 편집, 설정 동기화
- 테마, 아이콘, 에디터 레이아웃 조정
- 링크: https://code.visualstudio.com/docs/getstarted/settings

## 키보드 단축키
- 플랫폼별 단축키, 단축키 사용자 지정 방법
- 링크: https://code.visualstudio.com/docs/getstarted/keybindings

## 확장(Extensions)
- Marketplace에서 확장 설치/관리, 개발자 확장 가이드
- 추천: 언어 지원, 테마, Linter, 디버거 등
- 링크: https://code.visualstudio.com/docs/editor/extension-marketplace

## 디버깅
- 런치 구성(launch.json), 브레이크포인트, 변수/콜스택 확인 방법
- 링크: https://code.visualstudio.com/docs/editor/debugging

## 버전 관리(Git)
- 내장 Git 통합: 커밋, 브랜치, 병합, 원격 저장소 동기화
- 링크: https://code.visualstudio.com/docs/editor/versioncontrol

## 원격 개발 및 컨테이너
- Remote - SSH, Remote - Containers, WSL 연동 등 원격 개발 환경 설정
- 링크: https://code.visualstudio.com/docs/remote/remote-overview

## 언어 및 언어 서버
- 언어 확장 설치, LSP(Language Server Protocol)를 통한 풍부한 편집 기능 제공
- 링크: https://code.visualstudio.com/docs/languages/overview

## 확장 개발자용 자료
- VS Code 확장 API, 샘플 및 배포 방법
- 링크: https://code.visualstudio.com/api

## 명령줄과 통합
- `code` CLI 사용법: 파일/폴더 열기, 확장 관리, 원격 작업 등
- 링크: https://code.visualstudio.com/docs/editor/command-line

## AI 에이전트 및 최신 기능
- AI 에이전트, 세션 관리, 통합 브라우저 테스트 등 최신 에이전트 관련 기능 안내
- 링크: https://code.visualstudio.com/docs/agents/overview

## 팁과 트릭
- 생산성 향상 팁: 스니펫, 리팩토링 단축키, 검색/치환 고급 사용법

## 도움말 및 지원
- 커뮤니티, 이슈 보고, 기능 요청 등 지원 채널 안내
- 링크: https://code.visualstudio.com/docs/supporting/faq

---

원하시면 이 요약을 더 상세하게 확장하거나, 특정 섹션(예: 디버깅, 확장 개발)을 깊게 번역해 드리겠습니다.
