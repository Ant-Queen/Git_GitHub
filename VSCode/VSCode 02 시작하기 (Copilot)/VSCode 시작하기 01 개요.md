# VS Code 시작하기 - 개요

> **원본 페이지**: https://code.visualstudio.com/docs/getstarted/overview  
> **페이지 제목**: Get started with Visual Studio Code  
> **마지막 업데이트**: 2026년 6월

---

## 📚 목차

1. [소개](#소개)
2. [VS Code 설치](#vs-code-설치)
3. [AI 기능 활성화](#ai-기능-활성화)
4. [다음 단계](#다음-단계)
5. [일반적인 질문 (FAQ)](#일반적인-질문-faq)

---

## 소개

### Visual Studio Code란?

**Visual Studio Code (VS Code)** 는 다음과 같은 특징을 갖춘 현대적 코드 편집기입니다:

- ✅ **무료**: 완전 무료 오픈소스 소프트웨어
- ✅ **경량**: 빠른 실행과 낮은 시스템 요구사항
- ✅ **크로스 플랫폼**: Windows, macOS, Linux 모두 지원
- ✅ **AI 중심**: AI 에이전트 기반 플랫폼
- ✅ **확장성**: 50만 개 이상의 확장 프로그램
- ✅ **강력한 기능**: 디버깅, Git 통합, IntelliSense 내장
- ✅ **개발자 친화적**: 개발자 커뮤니티가 적극 지원

### 두 가지 사용 방법

#### 1. 데스크톱 버전 설치
- [공식 웹사이트에서 다운로드](https://code.visualstudio.com/download)
- Windows, macOS, Linux 설치 파일 제공
- 모든 기능 지원

#### 2. 웹 브라우저 버전 (온라인)
- [vscode.dev](https://vscode.dev) 접속
- **추가 설정 없음** (Zero Setup)
- 브라우저에서 즉시 편집 시작 가능
- [VS Code for the Web 상세 정보](https://code.visualstudio.com/docs/remote/vscode-web)

---

## VS Code 설치

### 시스템 요구사항

설치 전에 [시스템 요구사항](https://code.visualstudio.com/docs/supporting/requirements)을 확인하세요.

### 설치 버전

VS Code는 두 가지 릴리스 버전을 제공합니다:

| 버전 | 설명 | 업데이트 주기 |
|------|------|----------|
| **Stable (안정 버전)** | 안정성과 신뢰성 우선 | 매주 출시 |
| **Insiders (개발자 버전)** | 새로운 기능 미리 체험 | 매일 밤 출시 |

> **팁**: 두 버전은 동시에 설치 가능하며, 별도로 실행됩니다.

### Windows에서 설치

#### 1단계: 설치 파일 다운로드
- [공식 다운로드 페이지](https://code.visualstudio.com/download)에서 **User Setup 설치 프로그램** (`.exe` 파일) 다운로드

#### 2단계: 설치 프로그램 실행
- 다운로드된 `.exe` 파일 실행
- 설치 마법사의 지시 따르기
- 기본 설정으로 진행 가능

#### 3단계: 설치 완료
- 설치 완료 후 VS Code 자동 실행
- **PATH에 자동 추가**: 터미널에서 `code .` 명령어로 폴더 직접 열기 가능

#### 다른 Windows 설치 옵션
- **System Setup**: 모든 사용자를 위한 설치
- **ZIP Archive**: 설치 없이 실행 가능
- 자세한 정보: [Windows 상세 설치 가이드](https://code.visualstudio.com/docs/setup/windows)

### macOS에서 설치

#### 1단계: 설치 파일 다운로드
- [공식 다운로드 페이지](https://code.visualstudio.com/download)에서 macOS 버전 다운로드
- **Intel 칩셋** 또는 **Apple Silicon (M1/M2)** 선택

#### 2단계: 설치
- 다운로드된 DMG 파일 열기
- VS Code 아이콘을 Applications 폴더로 드래그 앤 드롭

#### 3단계: 설치 완료
- Applications 폴더에서 VS Code 실행

### Linux에서 설치

#### Ubuntu/Debian
1. Microsoft 저장소 키 설정
2. 패키지 저장소 추가
3. `apt` 패키지 매니저로 설치

```bash
# 저장소 설정
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg

# 저장소 추가
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'

# VS Code 설치
rm -f packages.microsoft.gpg
sudo apt update
sudo apt install code
```

#### 기타 배포판
- 공식 다운로드 페이지에서 해당 배포판 선택
- 또는 Snap, Flatpak 등 다양한 패키지 형식 지원

---

## AI 기능 활성화

### AI 기능 개요

VS Code는 **GitHub Copilot** 을 통한 AI 기능 기본 지원합니다:

- **인라인 제안**: 입력하면서 코드 자동 완성
- **AI 에이전트**: 복잡한 작업 자동 수행
- **Copilot Chat**: AI와 대화하며 코딩
- **기타 AI 기능**: 설명, 리팩토링, 테스트 생성 등

### Copilot 시작하기

#### 1단계: 로그인 또는 사인 업

두 가지 방법으로 시작 가능:

**방법 1: VS Code 상단 타이틀 바**
- "Sign In" 버튼 클릭

**방법 2: 상태 바의 Copilot 아이콘**
- 우측 하단의 Copilot 아이콘 위로 마우스 호버
- "Enable AI features" 버튼 클릭

#### 2단계: 로그인 방법 선택

- GitHub 계정으로 로그인
- Microsoft 계정으로 로그인 (GitHub 연동)
- 팝업 브라우저에서 인증 진행

#### 3단계: 구독 확인 및 설정

**기존 Copilot 구독이 있는 경우:**
- VS Code는 자동으로 해당 구독 사용

**구독이 없는 경우:**
- [Copilot Free 플랜](https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/managing-copilot-free/about-github-copilot-free) 자동 가입
- **무료 한도**: 
  - 매월 일정량의 인라인 제안
  - 매월 AI 크레딧 할당

#### 4단계: Copilot 사용 시작

VS Code에서 다양한 AI 기능 즉시 사용 가능:
- 코드 작성 중 자동 완성
- `Ctrl+I` (또는 `Cmd+I`): 인라인 편집
- `Ctrl+Shift+I` (또는 `Cmd+Shift+I`): Copilot Chat 열기

### 커스텀 언어 모델 사용

> **팁**: 자신의 언어 모델 API 키를 사용하여 AI 기능 커스터마이징 가능

자세한 정보: [VS Code에서 언어 모델 사용](https://code.visualstudio.com/docs/agent-customization/language-models#_bring-your-own-language-model-key)

---

## 다음 단계

### 1. 🤖 AI 에이전트 학습

#### 주제
자율 AI 에이전트를 활용하여 복잡한 코딩 작업 자동화

#### 학습 방법
- 대화형 튜토리얼 진행
- 실제 프로젝트 예제를 통한 학습

#### 링크
[AI 에이전트 시작하기 튜토리얼](https://code.visualstudio.com/docs/getstarted/getting-started)

---

### 2. 💪 강력한 편집기 기능 학습

#### 주제
VS Code의 핵심 편집 기능, 디버깅, 언어 지원 이해

#### 포함 내용
- **편집 기본**
  - 파일 편집 및 네비게이션
  - 다중 커서 및 선택
  - IntelliSense 자동완성
  - 코드 스니펫

- **디버깅**
  - 중단점 설정
  - 변수 확인
  - 콜 스택 분석
  - 언어별 디버거 설정

- **언어 지원**
  - Python, JavaScript, Java 등
  - 언어 서버 프로토콜 (LSP)
  - 자동완성 및 포맷팅

#### 링크
[강력한 편집기 가이드](https://code.visualstudio.com/docs/editing/getting-started)

---

### 3. 🔌 확장 프로그램 및 개방형 플랫폼

#### 주제
VS Code를 확장하고 커스터마이징하는 방법

#### 포함 내용
- **확장 프로그램 (Extensions)**
  - Marketplace에서 50만 개 이상 선택
  - 언어 지원, 테마, 도구 등
  
- **MCP 서버 (Model Context Protocol)**
  - AI 에이전트의 기능 확장
  - 커스텀 데이터 소스 연결
  
- **커스텀 인스트럭션**
  - AI 동작 개인화
  - 프로젝트별 규칙 정의
  
- **개방형 API**
  - VS Code 확장 개발
  - 커스텀 플러그인 작성

#### 링크
[확장 프로그램 및 플랫폼 가이드](https://code.visualstudio.com/docs/configure/extensions/extensions)

---

## 일반적인 질문 (FAQ)

### Q1: VS Code의 시스템 요구사항은 무엇인가요?

**A**: VS Code는 매우 가볍고 최소한의 하드웨어 요구사항을 가집니다:

**Windows:**
- Windows 10 또는 그 이상
- 최소 1.6 GHz 프로세서
- 1 GB RAM (2 GB 권장)
- 500 MB 디스크 공간

**macOS:**
- macOS 10.13 또는 그 이상
- Apple Silicon 또는 Intel 프로세서 지원
- 1 GB RAM (2 GB 권장)
- 500 MB 디스크 공간

**Linux:**
- Ubuntu 14.04 또는 그 이상 (또는 동등한 배포판)
- 1 GB RAM (2 GB 권장)
- 500 MB 디스크 공간

> **자세한 정보**: [공식 시스템 요구사항 페이지](https://code.visualstudio.com/docs/supporting/requirements)

---

### Q2: VS Code의 설치 파일 크기는 얼마나 되나요?

**A**: VS Code는 매우 가벼운 에디터입니다:

- **설치 후 크기**: 약 200-300 MB (추가 확장 제외)
- **다운로드 파일 크기**: 약 50-100 MB (플랫폼별 다름)

> **비교**: 다른 IDE (예: Visual Studio, IntelliJ)는 보통 1-3 GB 이상

---

### Q3: 새로운 프로젝트를 어떻게 만들고 실행하나요?

**A**: 프로젝트 생성 및 실행 방법:

#### 1단계: 새 폴더 만들기
```bash
mkdir my-project
cd my-project
```

#### 2단계: VS Code에서 폴더 열기
```bash
code .
```
또는 VS Code에서: File → Open Folder

#### 3단계: 프로젝트 초기화 (언어/프레임워크별)

**Node.js/JavaScript:**
```bash
npm init -y
```

**Python:**
```bash
python -m venv venv
source venv/bin/activate  # macOS/Linux
# 또는
venv\Scripts\activate  # Windows
```

**Git 저장소:**
```bash
git init
```

#### 4단계: 파일 작성 및 편집
- VS Code 에디터에서 코드 작성
- Copilot AI 기능 활용
- 디버깅 및 테스트 실행

---

### Q4: 현재 실행 중인 VS Code 버전을 어떻게 확인하나요?

**A**: 여러 방법이 있습니다:

#### 방법 1: UI를 통한 확인
1. 메뉴 → Help → About Visual Studio Code
2. 버전 정보 표시

#### 방법 2: 명령 팔레트 사용
1. `Ctrl+Shift+P` (또는 `Cmd+Shift+P`)
2. "About" 또는 "Show Version" 검색
3. 결과 확인

#### 방법 3: 터미널 명령어
```bash
code --version
```

---

### Q5: "VS Code 설치가 지원되지 않음"이라는 메시지가 나타나요. 어떻게 해야 하나요?

**A**: 이 메시지는 다음과 같은 이유로 나타날 수 있습니다:

#### 원인 1: 어댑터 설치 안 됨
- **해결**: 필요한 언어/플랫폼 확장 설치
- 예: Python 디버거, C++ 컴파일러 등

#### 원인 2: 비표준 설치 경로
- **해결**: 공식 설치 파일로 다시 설치

#### 원인 3: 손상된 설치 파일
- **해결**: VS Code 완전 제거 후 재설치

#### 원인 4: 지원되지 않는 OS
- **해결**: [시스템 요구사항 확인](https://code.visualstudio.com/docs/supporting/requirements)

---

### Q6: VS Code를 깔끔하게 완전 제거하려면 어떻게 하나요?

**A**: 플랫폼별 완전 제거 방법:

#### Windows
1. **설정 → 앱 → 프로그램 제거**
   - Visual Studio Code 찾기
   - 제거 버튼 클릭

2. **남은 파일 삭제**
   - `%APPDATA%\Code` 폴더 삭제
   - `%USERPROFILE%\.vscode` 폴더 삭제
   - `.code` 또는 `.vscode-oss` 폴더 삭제

#### macOS
1. **Applications 폴더에서 VS Code 삭제**
   - Finder → Applications
   - Visual Studio Code를 휴지통으로 이동

2. **설정 및 데이터 삭제**
   ```bash
   rm -rf ~/Library/Application\ Support/Code
   rm -rf ~/Library/Caches/com.microsoft.VSCode
   ```

#### Linux
```bash
# Ubuntu/Debian
sudo apt remove code

# 설정 및 데이터 삭제
rm -rf ~/.config/Code
rm -rf ~/.vscode
```

---

## 다음 리소스

### 튜토리얼 및 가이드
- 📖 [튜토리얼: 첫 앱 만들기](https://code.visualstudio.com/docs/getstarted/getting-started)
- 🎥 [소개 동영상](https://code.visualstudio.com/docs/getstarted/introvideos)
- 📚 [전체 문서](https://code.visualstudio.com/docs)

### 커뮤니티 및 지원
- 💬 [Stack Overflow](https://stackoverflow.com/questions/tagged/vscode) - 질문하기
- 🐛 [GitHub Issues](https://github.com/microsoft/vscode/issues) - 버그 보고
- 💡 [기능 요청](https://go.microsoft.com/fwlink/?LinkID=533482) - 새로운 기능 제안
- 🌐 [Reddit](https://www.reddit.com/r/vscode/) - 커뮤니티 토론

### 공식 채널
- 🔗 [공식 웹사이트](https://code.visualstudio.com)
- 📦 [Marketplace](https://marketplace.visualstudio.com/VSCode)
- 🔄 [GitHub 저장소](https://github.com/microsoft/vscode)
- 📰 [공식 블로그](https://code.visualstudio.com/blogs)

---

## 요약

### 설치 요약
```
1. 다운로드: https://code.visualstudio.com/download
2. 플랫폼별 설치 진행
3. VS Code 실행
4. 첫 프로젝트 열기
```

### AI 시작 요약
```
1. 로그인 (GitHub/Microsoft 계정)
2. Copilot Free 플랜 자동 가입 (또는 기존 구독 사용)
3. AI 기능 즉시 사용 가능
```

### 학습 경로
```
설치 → AI 기능 활성화 → 편집기 기본 학습 → 확장 프로그램 탐색 → 프로젝트 시작
```

---

**이 문서는 공식 VS Code 문서를 기반으로 작성되었습니다.**  
**원본 페이지**: https://code.visualstudio.com/docs/getstarted/overview  
**마지막 수정**: 2026년 6월 14일
