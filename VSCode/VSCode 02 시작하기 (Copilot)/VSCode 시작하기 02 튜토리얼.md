# VS Code 튜토리얼: AI 에이전트 코딩

> **원본 페이지**: https://code.visualstudio.com/docs/getstarted/getting-started  
> **페이지 제목**: Tutorial: Agentic coding in VS Code  
> **마지막 업데이트**: 2026년 6월

---

## 📚 목차

1. [소개](#소개)
2. [사전 조건](#사전-조건)
3. [프로젝트 폴더 생성](#프로젝트-폴더-생성)
4. [에이전트 창으로 기능 빌드](#에이전트-창으로-기능-빌드)
5. [편집기에서 에이전트로 코드 작성](#편집기에서-에이전트로-코드-작성)
6. [다음 단계](#다음-단계)

---

## 소개

### 튜토리얼 목표

이 튜토리얼에서 배우는 내용:

✅ **AI 에이전트를 사용한 개발**
- 에이전트에 자연어로 요청
- 에이전트가 자동으로 코드 생성 및 수정
- 에이전트의 오류 자동 수정

✅ **두 가지 워크플로우**
1. **에이전트 우선 접근**: Agents 창에서 작업 위임
2. **코드 우선 접근**: Chat 뷰에서 코드 작성하며 에이전트 보조

✅ **VS Code 기본 기능**
- 워크스페이스 관리
- 통합 브라우저 사용
- Git 소스 제어

### 학습 프로젝트

**개인 포트폴리오 페이지 구축**

- 📄 **기술**: HTML, CSS, JavaScript
- 🎨 **특징**: 헤더, 프로젝트 카드, 연락처 섹션
- ⚡ **장점**: 별도 런타임 또는 빌드 도구 불필요
- 🌐 **미리보기**: VS Code 통합 브라우저에서 즉시 확인

---

## 사전 조건

### 필수 설치 항목

#### 1. Visual Studio Code 다운로드 및 설치
- 📥 [공식 다운로드 페이지](https://code.visualstudio.com/download)
- 플랫폼별 버전 선택: Windows, macOS, Linux

#### 2. VS Code에서 AI 기능 활성화
- GitHub 계정 로그인
- Copilot 구독 또는 Copilot Free 플랜 가입
- 📖 [AI 기능 활성화 가이드](https://code.visualstudio.com/docs/getstarted/overview#_enable-ai-features)

#### 3. Git 설치
- 📥 [Git 공식 웹사이트](https://git-scm.com/)에서 다운로드
- 플랫폼별 설치 진행
- 터미널에서 `git --version` 으로 확인

### 💡 팁: Copilot Free 플랜

아직 Copilot 구독이 없다면:

- 🆓 [Copilot Free 플랜 가입](https://github.com/github-copilot/signup)
- 매월 인라인 제안 무료 한도 제공
- 매월 AI 크레딧 할당

---

## 프로젝트 폴더 생성

### 워크스페이스 개념

**워크스페이스 = 프로젝트 폴더**
- 에이전트는 폴더 컨텍스트 내에서 작동
- VS Code에서 별도 창 열 필요 없음 (Agents 창에서 여러 폴더 관리)

### 1단계: 프로젝트 폴더 생성

**경로**:
```bash
# 컴퓨터에 myportfolio 폴더 생성
mkdir myportfolio
cd myportfolio
```

### 2단계: Git 저장소 초기화

**커맨드 라인에서**:
```bash
cd myportfolio
git init
```

또는

**VS Code 내에서**:
1. 좌측 사이드바에서 "Source Control" 뷰 선택
2. "Initialize Repository" 버튼 클릭

### 결과

✅ 빈 폴더 `myportfolio` 생성  
✅ Git 저장소 초기화 (`.git` 폴더 생성)  
✅ 에이전트가 작업할 준비 완료

---

## 에이전트 창으로 기능 빌드

### Agents 창 개요

**용도**: 에이전트 중심 워크플로우에 최적화된 전용 창

**장점**:
- 여러 프로젝트 간편 관리
- 각 프로젝트마다 VS Code 창 열 필요 없음
- 에이전트 세션 목록 및 추적
- 파일 변경사항 확인 및 커밋

### 1단계: Agents 창 열기

**방법 1: 버튼 클릭**
1. VS Code 타이틀 바에서 "Open in Agents" 버튼 클릭

**방법 2: 명령 팔레트**
1. `Ctrl+Shift+P` (또는 `Cmd+Shift+P`)
2. "Chat: Open Agents Window" 검색 및 실행

**방법 3: 시작 페이지**
1. VS Code Welcome 페이지에서 Agents 창 열기 옵션 클릭

### 2단계: 로그인

- GitHub 또는 Microsoft 계정으로 로그인
- VS Code에 이미 로그인되어 있으면 자동 연동
- Copilot 구독 확인

### 3단계: 새 에이전트 세션 시작

#### 세션 생성
1. 좌측 사이드바의 "New" 버튼 클릭
2. 워크스페이스 드롭다운에서 "myportfolio" 폴더 선택

#### 폴더 신뢰 확인
- 프롬프트가 나타나면 "Yes, I trust the authors" 선택
- 🔒 **Workspace Trust**: 폴더의 코드 실행 허용 여부 결정

#### 에이전트 구성

**기본 설정**:

| 설정 | 설명 | 기본값 |
|------|------|--------|
| **Agent** | 작업 수행 에이전트 유형 | Generic (일반) |
| **Language Model** | 사용할 AI 모델 | 기본 모델 |
| **Default Approvals** | 자동 승인 설정 | 안전한 작업만 자동 승인 |
| **Folder & Branch** | 작업 위치 및 Git 분기 | 현재 분기 |

> **참고**: Copilot CLI가 선택되어야 로컬 머신에서 에이전트 실행

### 4단계: 포트폴리오 페이지 생성

#### 프롬프트 입력

Chat 입력창에 다음 프롬프트 입력:

```
Create a personal portfolio page with HTML, CSS, and JavaScript 
in separate files. Include a header with my name and a short bio, 
a section for projects with cards, and a contact section. 
Use modern styling and add some sample content.
```

#### 에이전트 작업 과정

1. 📋 **분석 및 계획**: 요청 분석, 작업 계획 수립
2. 🔨 **파일 생성**: HTML, CSS, JavaScript 파일 생성
3. 📝 **코드 작성**: 각 파일에 코드 작성
4. 🔧 **오류 수정**: 문제 발생 시 자동 수정
5. ✅ **완료**: 모든 파일 생성 완료

**Chat 뷰에서 실시간 모니터링**:
- 에이전트 진행 상황 표시
- 생성된 파일 목록
- 오류 및 승인 요청

---

### 5단계: 포트폴리오 미리보기 및 반복

#### 통합 브라우저에서 미리보기

**방법**:
1. Files 패널에서 `index.html` 우클릭
2. "Open in Integrated Browser" 선택

**장점**:
- VS Code를 나갈 필요 없음
- 실시간 변경사항 확인

#### 요소 선택 모드

**목적**: 페이지의 특정 요소 선택하여 에이전트에 컨텍스트 전달

**사용 방법**:
1. 통합 브라우저 툴바에서 "Add Element to Chat" 버튼 클릭
2. 페이지 요소 위로 마우스 이동
3. 변경하고 싶은 요소 선택 (예: 제목)
4. 에이전트가 자동으로 HTML, CSS, 스크린샷을 프롬프트에 추가

#### 디자인 변경 요청

**예제 프롬프트**:

```
Use a gradient color for the text and use cursive.
```

**프로세스**:
1. 프롬프트 입력
2. 에이전트가 선택된 요소 수정
3. 통합 브라우저에서 페이지 새로고침
4. 변경사항 확인

---

### 6단계: 변경사항 검토 및 커밋

#### Changes 패널 확인

**위치**: Agents 창의 "Changes" 탭

**표시 정보**:
- 에이전트가 생성/수정한 모든 파일
- 변경 통계 (추가/삭제/수정 줄 수)
- 파일별 변경 유형 표시

#### Diff 뷰에서 코드 검토

**방법**:
1. Changes 패널에서 파일 선택
2. Diff 뷰 열기
3. 에이전트의 수정 사항 확인

**Diff 뷰 기능**:
- 🟢 초록색: 추가된 줄
- 🔴 빨간색: 삭제된 줄
- ⚙️ 컨트롤: 개별 편집 내용 수락/취소
- 💬 피드백: 특정 코드 부분에 대한 인라인 피드백 작성

#### 변경사항 커밋

**방법**:
1. Changes 패널에서 "Commit Changes" 버튼 클릭
2. 에이전트의 모든 변경사항이 Git 커밋됨
3. Changes 패널이 비워짐 (대기 중인 변경사항 없음)

---

## 편집기에서 에이전트로 코드 작성

### 코드 우선 워크플로우

**목적**: 코드 작성에 집중하면서 에이전트의 보조를 받기

**예제**: 테마 토글러 기능 추가

### 1단계: 편집기에서 워크스페이스 열기

**방법**:
1. Agents 창의 타이틀 바에서 "Open in Editor" 버튼 클릭
2. 새로운 VS Code 창 열기 (워크스페이스 포함)
3. 좌측 사이드바: Explorer 뷰 (파일 목록)
4. 우측 사이드바: Chat 뷰 (에이전트 세션)

**화면 구성**:
```
┌─────────────────────────────────────────────┐
│ Explorer  │  편집 영역  │  Chat View       │
│  파일     │  코드 편집  │  에이전트 세션   │
│           │             │                   │
└─────────────────────────────────────────────┘
```

### 2단계: Chat 뷰에서 새 세션 시작

#### 새 Chat 시작
1. Chat 뷰 타이틀 바에서 "New Chat" (+ 버튼) 클릭
2. 새로운 에이전트 세션 생성

#### 세션 대상 선택
- "Session Target" 드롭다운에서 "Local" 선택
- 편집기 컨텍스트에서 에이전트 실행
- 파일, 도구, 통합 브라우저 접근 가능

### 3단계: 에이전트 작업 요청

#### 프롬프트 입력

```
Add a theme switcher button that toggles between 
a light and dark color theme for the page.
```

#### 에이전트 작동

1. 📝 **인라인 Diff**: 편집기에 변경사항이 실시간으로 표시
2. 📄 **파일 변경 목록**: Chat 뷰에서 수정된 파일 표시
3. ⏱️ **스트리밍**: 변경사항이 계속 에디터로 스트리밍됨

#### 변경사항 수락/거부

**개별 편집 검토**:
1. 편집기에서 인라인 Diff 오버레이 표시
2. "Keep" 버튼: 변경사항 수락
3. "Undo" 버튼: 변경사항 취소

---

### 4단계: 변경사항 미리보기

#### 통합 브라우저에서 열기

1. 편집기 탭의 `index.html` 선택
2. 타이틀 바의 "Open in Integrated Browser" (🌐) 버튼 클릭
3. 새로운 테마 토글러 기능 확인

#### 에이전트에 검증 요청

**프롬프트**:

```
Verify that the theme switcher works correctly and review 
the design aligns with the rest of the page. 
If there are any issues, fix them.
```

**에이전트 작동**:
1. 🌐 **브라우저 접근 승인 요청**: "Allow in this session" 클릭
2. 📋 **검증**: 에이전트가 통합 브라우저에서 페이지 테스트
3. 🔧 **자동 수정**: 문제 발견 시 자동 수정
4. ✅ **결과**: 모든 변경사항 확인 및 적용

---

## 다음 단계

### 튜토리얼 완료

축하합니다! 🎉

다음을 배웠습니다:
- ✅ AI 에이전트를 사용한 개발
- ✅ 에이전트 우선 워크플로우 (Agents 창)
- ✅ 코드 우선 워크플로우 (Chat 뷰)
- ✅ 통합 브라우저를 사용한 미리보기 및 검증
- ✅ Git을 사용한 변경사항 관리

### 추가 학습 자료

#### 1. 에이전트 심화 학습
- 📖 [에이전트 튜토리얼](https://code.visualstudio.com/docs/agents/agents-tutorial)
- 다양한 에이전트 유형 탐색
- 복잡한 작업 위임 방법

#### 2. Agents 창 상세 가이드
- 📖 [Agents 창 문서](https://code.visualstudio.com/docs/agents/agents-window)
- 창 기능 및 설정 상세 설명
- 고급 워크플로우 구성

#### 3. Chat 뷰 상세 가이드
- 📖 [Chat 뷰 문서](https://code.visualstudio.com/docs/agents/chat-view)
- Chat 뷰 최적화 사용법
- 키보드 단축키 및 팁

#### 4. VS Code 편집기 기능
- 📖 [편집기 기본 튜토리얼](https://code.visualstudio.com/docs/editing/getting-started)
- 코드 편집, 디버깅, 언어 지원
- 생산성 도구 및 확장 프로그램

---

## 주요 개념 정리

### 에이전트 (Agent)

**정의**: 자연어 요청을 받아 코드 생성, 수정, 테스트를 자동으로 수행하는 AI

**능력**:
- 📝 파일 생성 및 편집
- 🔧 오류 자동 수정
- 🌐 브라우저를 통한 테스트 및 검증
- 💾 Git 커밋
- 🔄 반복적 개선

### Agents 창

**목적**: 에이전트 중심 워크플로우 최적화

**기능**:
- 여러 워크스페이스 관리
- 세션 목록 및 추적
- 파일 변경사항 확인
- Diff 뷰를 통한 코드 검토
- Git 커밋 관리

### Chat 뷰

**목적**: 편집기에서 코드 작성 중 에이전트 지원

**특징**:
- 사이드바의 우측 패널
- 실시간 인라인 Diff
- 개별 편집 수락/취소 가능
- 인라인 피드백 작성 가능

### 통합 브라우저

**목적**: VS Code를 나가지 않고 웹 애플리케이션 미리보기

**용도**:
- 웹사이트 실시간 미리보기
- 에이전트 테스트 및 검증 지원
- 요소 선택 모드로 특정 부분 수정 요청

### Workspace Trust

**목적**: 폴더의 코드 실행 안전성 확인

**필요 이유**:
- 인터넷에서 다운로드한 코드 보안
- 악의적인 코드 실행 방지

---

## 팁과 트릭

### 💡 에이전트 작업 최적화

1. **명확한 요청**: 구체적이고 상세한 프롬프트 작성
2. **단계적 작업**: 큰 작업을 작은 단위로 분할
3. **피드백 제공**: 부분 코드에 인라인 피드백 작성
4. **브라우저 검증**: 에이전트에게 직접 검증 요청

### 🔧 워크플로우 선택 가이드

| 상황 | 추천 방법 | 이유 |
|------|---------|------|
| 새 기능 빌드 | Agents 창 | 작업 위임에 적합 |
| 기존 코드 수정 | Chat 뷰 | 세밀한 제어 가능 |
| 웹 앱 테스트 | 통합 브라우저 | 즉시 확인 가능 |
| 변경사항 검토 | Diff 뷰 | 상세 비교 가능 |

### ⚡ 단축키

- `Ctrl+Shift+P` / `Cmd+Shift+P`: 명령 팔레트
- `Chat: Open Agents Window`: Agents 창 열기
- `Ctrl+I` / `Cmd+I`: 인라인 편집
- `Ctrl+Shift+I` / `Cmd+Shift+I`: Chat 뷰 열기

---

## 트러블슈팅

### Q: Agents 창이 열리지 않습니다
**A**: 
1. GitHub 계정으로 로그인 확인
2. Copilot 구독 또는 Free 플랜 확인
3. VS Code 재시작 시도

### Q: 에이전트가 파일을 생성하지 않습니다
**A**:
1. 프롬프트가 충분히 구체적인지 확인
2. 폴더 신뢰 ("Yes, I trust") 확인
3. Git 저장소 초기화 확인

### Q: 통합 브라우저가 작동하지 않습니다
**A**:
1. 올바른 파일 형식인지 확인 (HTML 등)
2. "Open in Integrated Browser" 옵션 재확인
3. 파일을 먼저 저장한 후 시도

### Q: 변경사항이 저장되지 않습니다
**A**:
1. "Commit Changes" 버튼 클릭 확인
2. 파일 탭에서 수정 표시(점) 확인
3. "Keep" 버튼으로 변경사항 수락 확인

---

## 요약

### 학습 경로

```
1️⃣ 사전 조건 확인
   ↓
2️⃣ 프로젝트 폴더 생성
   ↓
3️⃣ Agents 창에서 포트폴리오 페이지 생성
   ↓
4️⃣ 통합 브라우저에서 미리보기 및 반복
   ↓
5️⃣ 변경사항 검토 및 커밋
   ↓
6️⃣ 편집기에서 추가 기능 구현
   ↓
7️⃣ Chat 뷰로 에이전트 지원 받으며 코드 작성
   ↓
8️⃣ 통합 브라우저에서 최종 검증
```

### 핵심 배운 점

✅ **두 가지 워크플로우의 강점**
- Agents 창: 작업 위임 및 자동화
- Chat 뷰: 세밀한 제어 및 반복 작업

✅ **통합 브라우저의 중요성**
- 즉시 결과 확인
- 에이전트 자체 검증 지원

✅ **Git 관리의 편의성**
- 변경사항 추적
- Diff 뷰를 통한 세밀한 검토
- 한 번에 모든 변경사항 커밋

---

**이 튜토리얼을 통해 VS Code의 현대적 AI 에이전트 기반 개발 워크플로우를 경험했습니다!**

**원본 페이지**: https://code.visualstudio.com/docs/getstarted/getting-started  
**마지막 수정**: 2026년 6월 14일
