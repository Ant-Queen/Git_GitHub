# VS Code MCP 서버 추가 및 관리

## 개요

**Model Context Protocol (MCP)**는 AI 모델을 외부 도구와 서비스에 연결하기 위한 개방형 표준입니다. VS Code에서 MCP 서버는 파일 작업, 데이터베이스, 또는 외부 API와 상호작용하는 **도구**를 제공합니다.

### MCP 서버의 기능

| 기능 | 설명 | 사용 방법 |
|------|------|---------|
| **도구** | 작업 수행 (파일 편집, API 호출 등) | 채팅에서 직접 호출 |
| **리소스** | 읽기 전용 데이터 (파일, DB 테이블 등) | 채팅 컨텍스트로 추가 |
| **프롬프트** | 사전 설정 프롬프트 템플릿 | `/mcp-server.prompt` 입력 |
| **MCP Apps** | 상호작용식 UI (폼, 시각화 등) | 채팅에 인라인 렌더링 |

## 빠른 시작: MCP 서버 사용

### 예: Playwright MCP 서버

1. **설치**
   - 확장 보기에서 `@mcp playwright` 검색
   - 설치 버튼 클릭

2. **신뢰**
   - 서버 시작 확인 프롬프트 표시
   - 신뢰한다고 확인

3. **사용**
   - 챗 창에서 Playwright 도구 사용 가능
   ```
   code.visualstudio.com 방문, 쿠키 배너 거부, 홈페이지 스크린샷
   ```

4. **도구 확인**
   - 채팅에서 "도구 구성" 버튼으로 모든 도구 확인
   - 특정 도구 활성화/비활성화 가능

## MCP 서버 추가

### 방법 1: MCP 서버 갤러리에서 설치

1. 확장 보기 열기 (`Ctrl+Shift+X`)
2. `@mcp` 검색하여 사용 가능한 서버 확인
3. **설치 방법:**
   - 사용자 프로필에 설치: "설치" 버튼
   - 워크스페이스에 설치: 우클릭 → "워크스페이스에 설치"

**장점:** 쉬운 설치, 자동 관리

### 방법 2: mcp.json 파일로 수동 구성

**위치:**
- 워크스페이스: `.vscode/mcp.json`
- 사용자 프로필: MCP 열기 사용자 구성

**구성 예시:**

```json
{
  "servers": {
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp"
    },
    "playwright": {
      "command": "npx",
      "args": ["-y", "@microsoft/mcp-server-playwright"]
    }
  }
}
```

**필드:**
- `type`: 서버 타입 (http, stdio 등)
- `command`: 실행할 명령어
- `args`: 명령어 인수
- `url`: HTTP 서버의 URL
- `env`: 환경 변수

### 방법 3: 명령 팔레트로 추가

```
MCP: Add Server
```
- 가이드 과정 제공
- 워크스페이스 또는 글로벌 선택

### 방법 4: 개발 컨테이너에 추가

개발 컨테이너의 `devcontainer.json`에 MCP 서버 정의:

```json
{
  "customizations": {
    "vscode": {
      "settings": {
        "mcp.servers": {
          "myserver": {
            "type": "stdio",
            "command": "npm",
            "args": ["run", "mcp"]
          }
        }
      }
    }
  }
}
```

### 자동 MCP 서버 발견

일부 MCP 서버는 자동으로 발견될 수 있습니다:

**설정:**
```
chat.mcp.autoStart: true (실험적)
```

구성 변경 시 자동으로 서버 재시작됩니다.

## mcp.json 파일 구성 상세

### 기본 구조

```json
{
  "servers": {
    "server-name": {
      "type": "stdio|http|sse",
      "command": "...",
      "args": [...],
      "env": {...},
      "cwd": "...",
      "timeout": 30
    }
  },
  "sandbox": {
    "filesystem": {...},
    "network": {...}
  }
}
```

### 입력 변수 (민감 정보 보호)

API 키 같은 민감 정보 처리:

```json
{
  "servers": {
    "myapi": {
      "command": "node",
      "args": ["server.js"],
      "env": {
        "API_KEY": "${input:apiKey}",
        "API_URL": "${input:apiUrl}"
      }
    }
  }
}
```

VS Code가 입력을 요청합니다.

## MCP 서버 관리

### 확장 보기에서 관리

**위치:** MCP SERVERS - INSTALLED 섹션

**작업:**
- 우클릭하여 기어 아이콘 또는 메뉴로 관리
- 시작/중지, 로그 보기, 제거 등

### mcp.json 에디터에서 관리

1. `MCP: Open User Configuration` 또는 `MCP: Open Workspace Folder Configuration` 실행
2. 파일 편집 시 인라인 작업 (code lenses) 제공
3. 서버 시작/중지 가능

### 명령 팔레트에서 관리

```
MCP: List Servers
```
- 서버 목록 표시
- 서버 선택 후 작업 선택

## MCP 서버 활성화/비활성화

서버를 제거하지 않고 임시 비활성화:

**방법 1: 확장 보기**
- 우클릭 → 활성화/비활성화

**방법 2: 명령 팔레트**
```
MCP: List Servers
→ 서버 선택 → 활성화/비활성화
```

**방법 3: 에이전트 커스터마이징 에디터**
- 에디터에서 토글

**범위:**
- 글로벌: 모든 워크스페이스 적용
- 워크스페이스 특정: 현재 워크스페이스만

## 샌드박스 MCP 서버 (macOS/Linux)

### 개념

로컬 stdio MCP 서버를 격리된 환경에서 실행하여 파일시스템과 네트워크 접근 제한합니다.

**이점:**
- 악의적이거나 손상된 서버로부터 보호
- 정책 강제
- 도구 호출 자동 승인 (격리 환경이므로)

### 활성화

```json
{
  "servers": {
    "myServer": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@example/mcp-server"],
      "sandboxEnabled": true
    }
  }
}
```

### 샌드박스 규칙 설정

```json
{
  "servers": {
    "myServer": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@example/mcp-server"],
      "sandboxEnabled": true
    }
  },
  "sandbox": {
    "filesystem": {
      "allowRead": ["${workspaceFolder}", "${home}/documents"],
      "allowWrite": ["${workspaceFolder}"]
    },
    "network": {
      "allowedDomains": ["api.example.com", "data.example.com"]
    }
  }
}
```

### 지원되는 변수

- `${workspaceFolder}`: 워크스페이스 루트
- `${home}`: 사용자 홈 디렉토리

### 주의사항

- **Windows에서 미지원**
- 모든 파일시스템 및 네트워크 규칙 명시적 허가 필요

## MCP 리소스

### 개념

MCP 서버가 제공하는 읽기 전용 데이터입니다.

**예시:**
- 파일 콘텐츠
- 데이터베이스 테이블
- API 응답

### 사용 방법

채팅에서 MCP 리소스 추가:

```
"컨텍스트 추가" > "MCP 리소스" 또는
MCP: Browse Resources
```

리소스는 채팅 컨텍스트로 첨부되지만, 편집은 불가능합니다.

## MCP 프롬프트

### 개념

MCP 서버가 제공하는 사전 설정 프롬프트 템플릿입니다.

### 사용 방법

```
/<mcp-server>.<prompt-name>
```

예: `/github.create-issue`

각 MCP 서버는 자신의 프롬프트를 정의할 수 있습니다.

## 신뢰 및 보안

### 신뢰 모델

새 MCP 서버 추가 시:

1. 신뢰 프롬프트 표시
2. 서버 구성 검토 가능
3. 신뢰하지 않으면 시작되지 않음

### 신뢰 재설정

```
MCP: Reset Trust
```

모든 MCP 서버의 신뢰 상태 초기화

### 보안 고려사항

⚠️ **주의:**
- 로컬 MCP 서버는 머신의 권한으로 실행됨
- 신뢰할 수 있는 출처에서만 추가
- 구성 검토 후 시작

**권장사항:**
- 공식 제공자 서버 우선
- 커뮤니티 서버는 검토 후 사용
- 샌드박스 활성화 (사용 가능 시)

## 설정 동기화

### Settings Sync로 MCP 서버 동기화

여러 디바이스 간에 MCP 서버 구성 동기화:

1. Settings Sync 활성화
2. `Settings Sync: Configure` 실행
3. 동기화할 항목 선택
4. **MCP Servers** 확인

**결과:** 모든 디바이스에서 동일한 MCP 서버 사용 가능

## 문제 해결

### MCP 서버가 시작되지 않음

**원인과 해결:**

1. **구성 오류**
   - `mcp.json` 문법 확인
   - 명령어가 존재하는가?
   - 경로가 정확한가?

2. **권한 문제**
   - 스크립트 실행 권한 확인 (`chmod +x`)
   - 필수 도구 설치되었는가?

3. **의존성 누락**
   - npm 패키지 설치했는가?
   - Node.js 버전 확인

### 도구 호출 오류

**확인사항:**
1. 서버가 실행 중인가?
2. 도구 이름이 정확한가?
3. 도구가 필요한 파라미터를 받았는가?

### 로그 확인

**방법 1: 확장 보기**
- 우클릭 → "출력 표시"

**방법 2: 명령 팔레트**
```
MCP: List Servers
→ 서버 선택 → Show Output
```

**방법 3: Output 패널**
- Output 패널 열기
- 채널 목록에서 "MCP" 또는 서버명 선택

## 자주 묻는 질문

### Q: MCP 서버와 도구의 차이?

**A:** MCP 서버는 여러 도구를 제공하는 **컨테이너**입니다. 예를 들어 "Playwright MCP 서버"는 "웹 페이지 열기", "클릭", "스크린샷" 도구들을 제공합니다.

### Q: 여러 MCP 서버 동시 사용 가능?

**A:** 예. 여러 서버를 동시에 실행하고 모든 도구를 사용 가능합니다.

### Q: MCP 리소스와 프롬프트를 모두 제공하는 서버도 있나?

**A:** 예. 서버는 도구, 리소스, 프롬프트를 원하는 조합으로 제공할 수 있습니다.

### Q: 자신의 MCP 서버 만들 수 있나?

**A:** 예. [MCP 문서](https://modelcontextprotocol.io/)를 참조하세요.

### Q: Docker로 MCP 서버 사용 가능?

**A:** 예. Docker 명령으로 실행할 수 있습니다:
```json
{
  "servers": {
    "myserver": {
      "command": "docker",
      "args": ["run", "-i", "myimage"]
    }
  }
}
```

## 고급 팁

1. **비용 최적화**: 필요한 서버만 활성화
2. **성능**: 자주 사용하지 않는 서버는 비활성화
3. **보안**: 신뢰할 수 없는 서버 전에 샌드박스 활성화
4. **모니터링**: 서버 로그로 문제 디버깅
5. **구성 관리**: 팀 설정은 워크스페이스 `.vscode/mcp.json`에 저장
