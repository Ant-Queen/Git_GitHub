# VS Code Copilot 가이드 및 튜토리얼

원문:
- Debug with Copilot: https://code.visualstudio.com/docs/copilot/guides/debug-with-copilot
- Browser Agent Testing Guide: https://code.visualstudio.com/docs/copilot/guides/browser-agent-testing-guide

## Copilot으로 디버깅하기

GitHub Copilot은 Visual Studio Code의 디버깅 워크플로우를 개선할 수 있습니다. Copilot은 프로젝트의 디버그 구성 설정을 돕고 디버깅 중 발견된 문제를 수정하는 제안을 제공합니다.

### Copilot으로 디버그 구성 설정

VS Code는 `launch.json` 파일을 사용하여 디버그 구성을 저장합니다. Copilot은 이 파일을 생성하고 커스터마이징하여 프로젝트 디버깅을 설정할 수 있습니다.

1. Chat 뷰 열기 (Ctrl+Alt+I)
2. `/startDebugging` 명령 입력
3. Copilot의 안내에 따라 프로젝트 디버깅 설정

또는 자연어 프롬프트 사용:
- "Django 앱의 디버그 구성 생성"
- "React Native 앱의 디버깅 설정"
- "Flask 애플리케이션의 디버깅 구성"

### Copilot으로 디버깅 시작

`copilot-debug` 터미널 명령은 디버그 구성 및 세션 시작 과정을 단순화합니다. 애플리케이션 시작 명령 앞에 `copilot-debug`를 붙여 Copilot이 자동으로 디버깅 세션을 구성하고 시작하도록 합니다.

1. 통합 터미널 열기 (Ctrl+`)
2. `copilot-debug` 뒤에 애플리케이션 시작 명령 입력:

   ```bash
   copilot-debug node app.js
   ```

   또는

   ```bash
   copilot-debug python manage.py
   ```

3. Copilot이 애플리케이션의 디버깅 세션을 시작합니다. 이제 VS Code의 내장 디버깅 기능을 사용할 수 있습니다.

더 자세한 내용: https://code.visualstudio.com/docs/debugtest/debugging

### Copilot으로 코딩 문제 수정

Copilot Chat을 사용하여 코딩 문제를 수정하거나 코드를 개선할 수 있습니다.

#### 채팅 프롬프트 사용

1. 애플리케이션 코드 파일 열기
2. 다음 뷰 중 하나 열기:
   - Chat 뷰 (Ctrl+Alt+I)
   - 인라인 채팅 (Ctrl+I)
3. 다음과 같은 프롬프트 입력:
   - "/fix"
   - "Fix this #selection"
   - "Validate input for this function"
   - "Refactor this code"
   - "Improve the performance of this code"

더 자세한 내용: https://code.visualstudio.com/docs/copilot/chat/copilot-chat

#### 편집기 스마트 액션 사용

프롬프트를 작성하지 않고 애플리케이션 코드의 코딩 문제를 수정할 수 있습니다.

1. 애플리케이션 코드 파일 열기
2. 수정할 코드 선택
3. 우클릭 > Generate Code > Fix 선택

VS Code가 코드 수정 제안을 제공합니다.
4. 선택사항: 채팅 프롬프트에서 추가 컨텍스트 제공하여 생성된 코드 개선

## 브라우저 에이전트 도구로 웹 앱 구축 및 테스트

브라우저 에이전트 도구를 통해 AI가 통합 브라우저에서 웹 애플리케이션을 자율적으로 구축하고 검증할 수 있습니다. 에이전트는 HTML, CSS, JavaScript를 생성하고, 앱을 통합 브라우저에서 열고, 기능을 검증하기 위해 상호작용하며, 콘솔 오류와 시각적 검사를 통해 문제를 식별하고 수동 개입 없이 수정합니다.

**참고**: 브라우저 에이전트 도구는 현재 실험적이며 향후 릴리스에서 변경될 수 있습니다.

### 사전 요구사항

- 컴퓨터에 [Visual Studio Code 설치](https://code.visualstudio.com/download)
- [GitHub Copilot 구독](https://code.visualstudio.com/docs/copilot/setup)
- `workbench.browser.enableChatTools` 설정으로 브라우저 에이전트 도구 활성화 (조직 수준에서 관리되므로 관리자에게 문의)

### 브라우저 에이전트 도구 작동 방식

브라우저 에이전트 도구를 활성화하면 에이전트는 통합 브라우저의 페이지 읽기 및 상호작용을 위한 도구에 액세스할 수 있습니다. 이러한 도구에는 다음이 포함됩니다:

- 페이지 탐색: `openBrowserPage`, `navigatePage`
- 페이지 콘텐츠 및 모양: `readPage`, `screenshotPage`
- 사용자 상호작용: `clickElement`, `hoverElement`, `dragElement`, `typeInPage`, `handleDialog`
- 커스텀 브라우저 자동화: `runPlaywrightCode`

기본적으로 에이전트가 연 페이지는 다른 브라우저 탭과 쿠키나 저장소를 공유하지 않는 프라이빗 인메모리 세션에서 실행됩니다. 이를 통해 에이전트가 액세스할 수 있는 브라우징 데이터를 제어할 수 있습니다.

더 자세한 내용: https://code.visualstudio.com/docs/debugtest/integrated-browser

### 단계별 가이드: 계산기 앱 구축 및 테스트

#### 1단계: 에이전트용 브라우저 도구 활성화

에이전트가 브라우저 도구를 사용하기 전에 채팅 도구 선택기에서 명시적으로 활성화해야 합니다.

1. Chat 뷰 열기 (Ctrl+Alt+I) 및 Agents 드롭다운에서 Agent 선택
2. 채팅 입력 영역의 Tools 버튼 선택하여 도구 선택기 열기
3. 모든 브라우저 도구가 활성화되었는지 확인 (Built-in > Browser 아래 그룹화됨)

이제 에이전트가 웹 페이지와 상호작용하기 위해 이러한 도구를 사용할 수 있습니다.

#### 2단계: 에이전트에게 계산기 구축 요청

브라우저 도구가 활성화된 상태에서 에이전트에게 간단한 계산기 애플리케이션을 생성하도록 요청합니다.

1. 새 프로젝트 폴더 생성 및 VS Code에서 열기
2. Chat 뷰에서 다음 프롬프트 입력:

   ```
   Create a calculator with buttons for digits 0-9, operations (add, subtract, multiply, divide), clear, and equals. Use HTML, CSS, and JavaScript. Style it with a clean, modern design.
   ```

3. 에이전트가 `index.html`, `styles.css`, `script.js` 파일을 생성하는 동안 검토
4. Keep 선택하여 파일을 워크스페이스에 저장

에이전트가 계산기 애플리케이션의 기본 구조를 구축했습니다.

#### 3단계: 에이전트에게 계산기 테스트 요청

이제 에이전트에게 통합 브라우저에서 계산기를 열고 모든 연산이 올바르게 작동하는지 확인하도록 요청합니다.

1. Chat 뷰에서 다음 프롬프트 입력:

   ```
   Open the calculator in the browser and test if all the operations work correctly.
   ```

2. 에이전트가 `index.html`을 통합 브라우저에서 열고, 페이지 콘텐츠를 파싱하여 구조를 이해하고, 클릭을 시뮬레이션하여 각 버튼과 연산을 체계적으로 테스트하는 것을 관찰합니다.

에이전트가 올바르게 작동하는 연산을 보고하고 발견한 문제를 식별합니다.

#### 4단계: 에이전트가 문제 디버깅 및 수정하는 것 관찰

테스트 중 에이전트가 버그를 발견하면 자동으로 문제를 분석하고 수정을 구현합니다.

1. 0으로 나누기 검사를 제거하여 버그를 도입:

   ```javascript
   function calculate() {
       if (!operator || shouldReset) return;

       const a = parseFloat(previous);
       const b = parseFloat(current);
       let result;

       switch (operator) {
       case '+': result = a + b; break;
       case '-': result = a - b; break;
       case '*': result = a * b; break;
       case '/': result = a / b; break;
   }
   ```

2. 에이전트에게 나누기 연산을 확인하고 발견한 문제가 있으면 수정하도록 요청:

   ```
   Verify the division operation works correctly. If you find any issues, fix them.
   ```

3. 에이전트가 0으로 나누기 시 오류를 만나면 코드를 분석하고 수정한 후 버그 수정을 검증하는 것을 관찰합니다.

에이전트가 브라우저 자동화를 사용하여 완전한 개발 주기(구축, 테스트, 디버깅, 수정)를 완료했습니다.

#### 5단계: 브라우저 페이지를 에이전트와 공유 (선택사항)

수동으로 웹 페이지를 열고 분석이나 상호작용을 위해 에이전트와 명시적으로 공유할 수도 있습니다. 기본적으로 에이전트는 자신이 연 웹 페이지에만 상호작용할 수 있습니다.

1. Command Palette (Ctrl+Shift+P)에서 Browser: Open Integrated Browser 명령 실행하여 통합 브라우저 열기
2. 에이전트가 분석하거나 상호작용할 웹 페이지로 이동
3. 브라우저 툴바에서 Share with Agent 버튼 선택

브라우저 탭의 시각적 표시기가 페이지가 에이전트와 적극적으로 공유되고 있음을 보여줍니다.
4. 공유된 페이지에서 에이전트에게 작업 수행 요청:

   ```
   What is the main heading on this page? Click the first link and tell me where it goes.
   ```

이제 에이전트가 공유된 페이지에 액세스하고 귀하를 대신하여 상호작용을 수행할 수 있습니다. 완료되면 Share with Agent 버튼을 다시 선택하여 액세스를 취소합니다.

**팁**: 공유된 페이지는 기존 브라우저 세션을 사용하므로 쿠키와 로그인 상태를 포함합니다. 에이전트가 연 페이지는 격리된 임시 세션을 사용하므로 다른 브라우저 탭과 쿠키나 저장소를 공유하지 않습니다.

### 시도할 시나리오

브라우저 에이전트 도구 작동 방식을 이해했으므로 다른 사용 사례를 탐색하기 위해 이러한 시나리오를 시도해보세요:

- **폼 검증 테스트**: 연락처 폼을 구축하고 테스트하여 검증 규칙, 오류 메시지, 성공 제출 확인
- **반응형 레이아웃 검증**: 랜딩 페이지의 다양한 뷰포트 크기에서 스크린샷을 찍고 반응형 동작 확인 (예: 탐색 메뉴가 있는 랜딩 페이지)
- **인증 플로우 테스트**: 로그인 페이지에서 자격 증명 검증, 오류 처리, 성공 리디렉션 테스트
- **대화형 기능 테스트**: 사용자 상호작용 및 상태 관리 검증
- **접근성 감사**: 누락된 alt 텍스트, 제목 계층 구조, 키보드 탐색, 색상 대비 문제 확인

### 관련 리소스

- [통합 브라우저](https://code.visualstudio.com/docs/debugtest/integrated-browser)
- [VS Code의 AI 핵심 개념](https://code.visualstudio.com/docs/copilot/concepts/overview)
- [에이전트 개요](https://code.visualstudio.com/docs/copilot/agents/overview)
- [Copilot으로 테스트](https://code.visualstudio.com/docs/copilot/guides/test-with-copilot)

---

**최종 업데이트**: 2026년 5월 6일