# Visual Studio Code 공식 문서 정리

> 원본 사이트: https://code.visualstudio.com/docs
> 마지막 업데이트: 2026년 6월

---

## 📚 목차

1. [개요](#개요)
2. [주요 문서 카테고리](#주요-문서-카테고리)
3. [AI 에이전트](#ai-에이전트)
4. [시작하기](#시작하기)
5. [핵심 기능](#핵심-기능)
6. [개발 도구](#개발-도구)
7. [확장 프로그램 및 커스터마이징](#확장-프로그램-및-커스터마이징)
8. [지원 및 커뮤니티](#지원-및-커뮤니티)

---

## 개요

**Visual Studio Code (VS Code)** 는 Microsoft에서 만든 무료 오픈소스 코드 편집기입니다. 
Windows, macOS, Linux에서 사용 가능하며, 다양한 프로그래밍 언어와 개발 환경을 지원합니다.

### 주요 특징
- 🚀 가볍고 빠른 성능
- 🔌 풍부한 확장 프로그램 생태계
- 🤖 AI 에이전트 통합 (Copilot)
- 🔍 강력한 검색 및 리팩토링 도구
- 📱 원격 개발 지원
- 🐛 통합 디버깅 및 테스팅
- 📝 Git 및 Source Control 내장

---

## 주요 문서 카테고리

### 1. **AI 에이전트 (Agents)**
- **경로**: `/docs/agents/overview`
- **설명**: 자율 AI 에이전트에게 작업을 위임하고, 로컬, 백그라운드 또는 클라우드에서 실행
- **주요 기능**:
  - 여러 AI 제공자 지원
  - 세션 추적 및 관리
  - 브라우저를 통한 자동 테스트 및 검증
  - 비용 및 성능 최적화 가이드

### 2. **시작하기 (Get Started)**
- **경로**: `/docs/getstarted/overview`
- **설명**: VS Code 설치, 기본 설정, 주요 기능 학습
- **포함 내용**:
  - 플랫폼별 설치 가이드 (Windows, macOS, Linux)
  - 기본 편집 기능
  - 설정 및 커스터마이징
  - 확장 프로그램 설치

### 3. **편집기 (Editor)**
- **경로**: `/docs/core-editor/overview`
- **설명**: VS Code 에디터의 핵심 기능 및 활용 방법
- **주요 주제**:
  - 코드 편집 기본 사항
  - 검색 및 바꾸기
  - 다중 선택 (Multi-selection)
  - 코드 스니펫 (Snippets)
  - IntelliSense (자동완성)
  - 포맷팅 및 린팅

### 4. **소스 제어 (Source Control)**
- **설명**: Git 및 GitHub 통합
- **기능**:
  - Git 저장소 초기화 및 관리
  - 커밋, 푸시, 풀 작업
  - 분기(Branch) 관리
  - 병합(Merge) 및 충돌 해결
  - GitHub 연동

### 5. **터미널 (Terminal)**
- **설명**: 통합 터미널 사용법
- **기능**:
  - 내장 터미널 (PowerShell, Bash 등)
  - 여러 터미널 인스턴스 관리
  - 작업(Tasks) 자동화
  - 쉘 통합 (Shell Integration)

### 6. **디버깅 (Debugging)**
- **설명**: 코드 디버깅 도구 및 기법
- **기능**:
  - 중단점(Breakpoints) 설정
  - 변수 관찰 (Watch)
  - 콜 스택 분석
  - 언어별 디버거 지원

### 7. **테스팅 (Testing)**
- **설명**: 테스트 프레임워크 통합 및 실행
- **기능**:
  - 테스트 발견 및 실행
  - 테스트 디버깅
  - 테스트 결과 보고

### 8. **엔터프라이즈 (Enterprise)**
- **경로**: `/docs/enterprise/overview`
- **설명**: 엔터프라이즈 환경에 맞는 VS Code 설정
- **포함 내용**:
  - 정책(Policies) 관리
  - 확장 프로그램 관리
  - AI 커스터마이징 옵션
  - 보안 및 규정 준수

### 9. **원격 개발 (Remote)**
- **설명**: SSH, WSL, Docker를 통한 원격 개발
- **기능**:
  - SSH 원격 개발
  - Windows Subsystem for Linux (WSL)
  - Docker 컨테이너에서 개발
  - Codespaces 통합

### 10. **고급 설정 (Advanced Setup)**
- **설명**: 고급 사용자를 위한 설정 및 최적화
- **주제**:
  - 포터블 설정
  - 환경 변수 설정
  - 성능 최적화
  - 다중 모니터 설정

### 11. **언어 및 런타임 (Languages & Runtimes)**
- **경로**: `/docs/languages/overview`
- **설명**: JavaScript, Python, C++, Java 등 다양한 언어 지원
- **각 언어별 정보**:
  - 확장 프로그램 추천
  - 디버깅 설정
  - 린팅 및 포맷팅
  - 테스팅 도구

### 12. **확장 프로그램 문서 (Extension Docs)**
- **경로**: `/docs/extension-docs/overview`
- **설명**: VS Code 확장 프로그램 개발 가이드
- **포함 내용**:
  - 확장 프로그램 아키텍처
  - API 참조
  - 확장 프로그램 발행 방법

---

## AI 에이전트

### AI 에이전트란?
자율적으로 작업을 반복하여 완료하는 AI 기반 도구입니다.

### 주요 가이드

#### 🎯 AI 사용 최적화
- **경로**: `/docs/agents/guides/optimize-usage`
- **내용**:
  - AI 에이전트 최대 활용 팁
  - 비용 최적화 전략
  - 성능 향상 방법

#### 🧪 브라우저 에이전트를 통한 테스트 및 디버깅
- **경로**: `/docs/agents/guides/browser-agent-testing-guide`
- **기능**:
  - 통합 브라우저를 이용한 자동 테스트
  - 애플리케이션 문제 자동 수정
  - UI/UX 검증 자동화

#### ⚙️ AI 커스터마이징
- **경로**: `/docs/agent-customization/overview`
- **내용**:
  - 커스텀 인스트럭션 설정
  - 스킬(Skills) 정의
  - MCP 서버 구성
  - 개인 워크플로우에 맞춘 AI 설정

### 에이전트 종류

1. **로컬 에이전트**: 로컬 머신에서 실행
2. **Copilot CLI**: 커맨드라인 인터페이스
3. **클라우드 에이전트**: 클라우드에서 실행
4. **서드파티 에이전트**: 외부 제공자의 에이전트

---

## 시작하기

### VS Code 설치

#### Windows
- Microsoft Store에서 설치 또는 https://code.visualstudio.com/Download에서 다운로드
- 설치 후 "code" 커맨드로 터미널에서 VS Code 실행 가능

#### macOS
- 공식 웹사이트에서 다운로드
- Homebrew로도 설치 가능: `brew install visual-studio-code`

#### Linux
- 각 배포판의 패키지 매니저를 통해 설치
- 또는 공식 리포지토리에서 다운로드

### 기본 설정

1. **테마 선택**: 라이트, 다크, 커스텀 테마
2. **폰트 설정**: 편집기 폰트 크기 및 종류 조정
3. **확장 프로그램 설치**: 작업에 필요한 확장 프로그램 설치
4. **키 바인딩 커스터마이징**: 단축키 설정

### 자주 사용되는 단축키

| 단축키 | 기능 |
|--------|------|
| `Ctrl+Shift+P` | 명령 팔레트 (Command Palette) |
| `Ctrl+P` | 파일 빠른 이동 (Quick Open) |
| `Ctrl+~` | 터미널 열기 |
| `Ctrl+/` | 주석 토글 |
| `Alt+Up/Down` | 줄 이동 |
| `Ctrl+K Ctrl+F` | 포맷팅 |
| `F5` | 디버깅 시작 |
| `Ctrl+B` | 사이드바 토글 |

---

## 핵심 기능

### 📝 편집 기능

- **IntelliSense**: 자동완성, 파라미터 힌트, 빠른 정보
- **코드 네비게이션**: 정의로 이동, 모든 참조 찾기
- **리팩토링**: 이름 바꾸기, 코드 추출 등
- **다중 선택**: 여러 위치에서 동시 편집
- **코드 스니펫**: 재사용 가능한 코드 템플릿

### 🔍 검색 및 바꾸기

- 정규표현식(Regex) 지원
- 전체 폴더 검색
- 파일별 검색 필터링
- 검색 결과 미리보기

### 🎨 포맷팅 및 린팅

- 자동 코드 포맷팅
- 일관성 있는 스타일 유지
- 린터 통합 (ESLint, Pylint 등)
- 저장 시 자동 수정

### 🔌 IntelliSense

- 언어별 지능형 자동완성
- 라이브러리 및 API 문서 표시
- 타입 힌트 및 서명 도움말
- 빠른 정보 (Hover Information)

---

## 개발 도구

### 소스 제어 (Git)

**주요 기능**:
- 저장소 클론, 초기화
- 커밋, 푸시, 풀
- 분기 생성 및 전환
- 병합 및 충돌 해결
- GitHub 연동

**팁**:
- 사이드바의 Source Control 패널 사용
- `Ctrl+Shift+G`로 빠르게 열기

### 터미널

**기능**:
- PowerShell, Bash, Zsh 등 지원
- 여러 터미널 인스턴스 관리
- 분할 터미널 (Split Terminal)
- 커스텀 쉘 구성

**작업 자동화**:
- `tasks.json`을 통한 작업 정의
- 빌드, 테스트, 배포 자동화
- 문제 감지(Problem Matchers)

### 디버깅

**기본 기능**:
- 중단점 설정 및 조건부 중단점
- 변수 보기 및 조사
- 콜 스택 추적
- 즉시 실행 (Debug Console)

**언어별 디버거**:
- JavaScript/Node.js
- Python
- C/C++
- Java
- Go

### 테스팅

**지원 기능**:
- 테스트 프레임워크 자동 발견
- 테스트 수행 및 디버깅
- 테스트 커버리지 보고
- CI/CD 통합

**지원 프레임워크**:
- Jest (JavaScript)
- pytest (Python)
- JUnit (Java)
- unittest (Python)

---

## 확장 프로그램 및 커스터마이징

### 확장 프로그램 설치

1. **방법 1**: 사이드바의 Extensions 패널에서 검색하여 설치
2. **방법 2**: 명령 팔레트에서 `Extensions: Install Extensions` 사용
3. **방법 3**: 터미널에서 `code --install-extension <extension-id>` 명령 사용

### 인기 확장 프로그램 카테고리

- **언어 지원**: Python, Java, C++, Go, Rust 등
- **테마**: Material Theme, Dracula, One Dark Pro 등
- **생산성**: ESLint, Prettier, Live Server 등
- **AI**: Copilot, Copilot Chat 등
- **DB**: MySQL, PostgreSQL, MongoDB 등

### 커스터마이징

#### 설정 파일

```json
// settings.json
{
  "editor.fontSize": 14,
  "editor.fontFamily": "'Fira Code'",
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "python.linting.enabled": true,
  "python.linting.pylintEnabled": true
}
```

#### 키 바인딩 커스터마이징

```json
// keybindings.json
[
  {
    "key": "ctrl+alt+k",
    "command": "editor.action.commentLine",
    "when": "editorTextFocus"
  }
]
```

#### 워크스페이스 설정

- 프로젝트별로 `.vscode/settings.json` 생성
- 팀 전체가 동일한 개발 환경 유지

### 테마 및 아이콘

- **색상 테마**: VS Code는 다양한 내장 테마 제공
- **파일 아이콘 테마**: 파일 종류별 아이콘 커스터마이징
- **커스텀 테마**: 사용자 정의 테마 생성 가능

---

## 엔터프라이즈

### 엔터프라이즈용 VS Code 설정

#### 정책(Policy) 관리

- 관리자가 사용자 설정 제어
- 특정 확장 프로그램 허용/차단
- 업데이트 정책 설정

#### 확장 프로그램 관리

- 조직 내 승인된 확장 프로그램 목록 관리
- 자동 확장 프로그램 배포
- 버전 관리 및 업데이트 제어

#### AI 커스터마이징

- 조직의 AI 정책 설정
- 커스텀 인스트럭션 정의
- 데이터 보안 및 프라이버시 설정

#### 보안 및 규정 준수

- RBAC (역할 기반 접근 제어)
- 감사 로깅 (Audit Logging)
- 데이터 암호화

---

## 원격 개발 (Remote Development)

### SSH 원격 개발

- 원격 서버에 연결하여 개발
- 로컬 확장 프로그램 지원
- 원격 터미널 접근

### Windows Subsystem for Linux (WSL)

- Windows에서 Linux 환경 사용
- WSL 배포판 지원
- 파일 시스템 접근

### Docker

- Docker 컨테이너에서 개발
- 일관된 개발 환경 보장
- 팀 전체가 동일한 환경 사용

### GitHub Codespaces

- 클라우드 기반 개발 환경
- 설정 자동화 가능 (`devcontainer.json`)
- 브라우저 및 VS Code에서 접근 가능

---

## 언어별 개발 환경

### JavaScript/TypeScript

- **추천 확장**: ESLint, Prettier, JavaScript (ES6) code snippets
- **디버거**: 내장 Node.js 디버거
- **테스팅**: Jest, Mocha, Vitest

### Python

- **추천 확장**: Python, Pylance, Python Docstring Generator
- **디버거**: Python 디버거 (pdb)
- **테스팅**: pytest, unittest
- **포맷팅**: Black, autopep8

### C/C++

- **추천 확장**: C/C++ Extension Pack
- **디버거**: GDB, LLDB, MSVC
- **빌드**: CMake, Make

### Java

- **추천 확장**: Extension Pack for Java
- **디버거**: 내장 Java 디버거
- **빌드**: Maven, Gradle

### Go

- **추천 확장**: Go Extension
- **디버거**: Delve
- **테스팅**: Go 테스트 프레임워크

---

## 고급 기능

### 다중 루트 워크스페이스

- 여러 폴더를 하나의 워크스페이스에서 관리
- `.code-workspace` 파일로 설정 저장

### 원격 SSH 개발

- 로컬 코드 편집, 원격 서버에서 실행
- 파일 자동 동기화

### 작업 자동화

`tasks.json`을 통한 빌드, 테스트, 배포 자동화:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "build",
      "command": "npm",
      "args": ["run", "build"],
      "type": "shell"
    }
  ]
}
```

### 디버그 구성

`.vscode/launch.json`으로 디버그 설정 커스터마이징:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: Current File",
      "type": "python",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal"
    }
  ]
}
```

---

## 지원 및 커뮤니티

### 공식 채널

- **GitHub**: https://github.com/microsoft/vscode
- **Issues**: 버그 보고 및 기능 제안
- **Discussions**: 커뮤니티 토론

### 커뮤니티 지원

- **Stack Overflow**: VS Code 태그로 질문 및 답변
- **Reddit**: https://www.reddit.com/r/vscode/
- **LinkedIn**: VS Code 공식 페이지
- **X (Twitter)**: @code

### 추가 리소스

- **공식 블로그**: VS Code 새로운 기능 및 팁
- **YouTube**: 튜토리얼 및 팁 영상
- **Podcast**: VS Code Insiders Podcast
- **Learn**: Microsoft Learn에서의 대화형 학습

### 피드백 및 요청

- **기능 제안**: https://go.microsoft.com/fwlink/?LinkID=533482
- **버그 보고**: GitHub Issues
- **문제 지원**: Microsoft Support

---

## 최신 업데이트 (v1.124)

### 주요 변경사항

- **Autopilot 기본 활성화**: AI 기반 기능 강화
- **에이전트 세션 네비게이션 개선**: 빠른 세션 전환
- **Copilot CLI 원격 제어 (실험 기능)**: GitHub.com 또는 GitHub Mobile에서 세션 모니터링 및 제어

### 성능 개선

- 에이전트 처리 워크플로우 최적화
- 모델 평가 및 코딩 하네스 개선

---

## 참고 정보

| 항목 | 링크 |
|------|------|
| 공식 사이트 | https://code.visualstudio.com |
| 다운로드 | https://code.visualstudio.com/Download |
| 문서 | https://code.visualstudio.com/docs |
| 확장 마켓플레이스 | https://marketplace.visualstudio.com/VSCode |
| GitHub | https://github.com/microsoft/vscode |
| MCP (Model Context Protocol) | https://code.visualstudio.com/mcp |
| License | https://code.visualstudio.com/License |

---

## 자주 묻는 질문 (FAQ)

- **Q: VS Code는 무료인가요?**  
  A: 네, VS Code는 무료 오픈소스 소프트웨어입니다.

- **Q: VS Code에서 지원하는 언어는 무엇인가요?**  
  A: JavaScript, TypeScript, Python, C++, Java, C#, PHP, Go, Rust 등 다양한 언어를 지원합니다.

- **Q: 확장 프로그램은 어디서 찾나요?**  
  A: VS Code Marketplace (https://marketplace.visualstudio.com)에서 확장 프로그램을 검색하고 설치할 수 있습니다.

- **Q: 설정을 동기화할 수 있나요?**  
  A: 네, Settings Sync 기능으로 Microsoft 또는 GitHub 계정을 통해 설정을 동기화할 수 있습니다.

- **Q: 원격 개발을 어떻게 하나요?**  
  A: Remote - SSH, WSL, Docker 확장 프로그램을 사용하여 원격 개발을 할 수 있습니다.

---

**문서 작성일**: 2026년 6월 14일  
**원본 사이트**: https://code.visualstudio.com/docs  
**라이선스**: 이 요약은 VS Code 공식 문서의 구조와 개요를 정리한 것입니다.
