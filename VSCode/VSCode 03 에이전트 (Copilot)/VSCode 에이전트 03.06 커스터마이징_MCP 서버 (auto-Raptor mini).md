# VS Code MCP 서버(MCP Servers)

## 개요
MCP 서버(Model Context Protocol server)는 AI가 외부 도구, 데이터, 리소스와 통합할 수 있도록 지원하는 표준 서버입니다. VS Code에서는 MCP 서버를 추가해 채팅 내에서 파일, API, 데이터베이스, 브라우저 등을 제어할 수 있습니다.

## 빠른 시작

1. 확장 보기에서 `@mcp playwright` 등 MCP 서버를 검색합니다.
2. 설치 후 신뢰 여부를 확인하고 서버를 시작합니다.
3. Chat 보기에서 도구를 사용하거나 `Configure Tools`를 통해 활성화합니다.
4. 예: `Go to code.visualstudio.com, decline the cookie banner, and give me a screenshot of the homepage.`

## MCP 서버 추가

### `mcp.json` 구성

워크스페이스나 사용자 프로필에 `mcp.json` 파일을 만들어 서버를 등록합니다.

- 워크스페이스: `.vscode/mcp.json`
- 사용자: MCP: Open User Configuration 명령으로 열기

예시:

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

> 원격 환경에서는 워크스페이스나 원격 사용자 설정에 서버를 정의해야 서버가 해당 머신에서 실행됩니다.

### `mcp.json` 편집

- VS Code는 `mcp.json`에 대한 IntelliSense를 제공합니다.
- 민감한 정보는 입력 변수 또는 환경 파일을 사용해 하드코딩을 피해야 합니다.

## 다른 추가 방법

- **MCP 서버 갤러리**: `@mcp` 검색어로 설치
- **개발 컨테이너**: 컨테이너 내 MCP 서버 설치
- **자동 검색**: VS Code가 서버를 자동으로 발견
- **명령줄**: Copilot CLI 등을 통해 설치

## MCP의 추가 기능

MCP 서버는 단순한 도구 외에도 다음을 제공합니다.

- **리소스**: 서버에서 제공되는 데이터나 파일을 채팅 컨텍스트로 첨부
- **프롬프트**: 서버가 제공하는 미리 정의된 템플릿 프롬프트
- **MCP 앱**: 양식, 시각화, 드래그 앤 드롭 UI 등 인터랙티브 컴포넌트

## 샌드박스 MCP 서버

- macOS 및 Linux에서 로컬 stdio MCP 서버에 샌드박스를 적용할 수 있습니다.
- `sandboxEnabled`: true로 설정하면 파일 시스템과 네트워크 접근을 제한합니다.
- 예:

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
      "allowWrite": ["${workspaceFolder}"]
    },
    "network": {
      "allowedDomains": ["api.example.com"]
    }
  }
}
```

> Windows에서는 샌드박스 기능이 아직 지원되지 않습니다.

## MCP 서버 관리

- **Extensions 뷰**: MCP SERVERS - INSTALLED에서 서버를 우클릭하여 시작, 중지, 로그 보기, 비활성화
- **mcp.json 편집기**: 코드 렌즈로 서버 관리
- **명령 팔레트**: `MCP: List Servers`로 서버 선택 및 작업 수행

## 활성화/비활성화

- 서버를 비활성화하면 시작되지 않고 도구/리소스가 채팅에 나타나지 않습니다.
- 서버 상태는 `mcp.json`과 별도로 저장됩니다.
- 워크스페이스별 또는 전역으로 관리할 수 있습니다.

## 중앙 관리

- 조직은 정책을 통해 MCP 서버 접근을 중앙에서 관리할 수 있습니다.
- `chat.mcp.autoStart`(실험적) 설정을 사용하면 구성 변경 시 자동으로 서버를 재시작할 수 있습니다.

## MCP 서버 신뢰

- 새로운 MCP 서버를 추가하거나 구성 변경 시 초기 신뢰 확인 대화상자가 표시됩니다.
- 신뢰하지 않으면 서버를 시작할 수 없습니다.
- `MCP: Reset Trust` 명령으로 신뢰를 재설정할 수 있습니다.

> `mcp.json`에서 직접 서버를 시작하면 신뢰 대화상자가 표시되지 않을 수 있습니다.

## 동기화

- Settings Sync를 사용하면 MCP 서버 구성과 관련 설정을 여러 기기 간에 동기화할 수 있습니다.
- `MCP Servers` 옵션을 동기화 대상에 포함시키세요.

## 문제 해결

- 서버 시작 실패: 출력 로그를 확인하고 `MCP: List Servers`에서 오류를 확인합니다.
- 도구가 보이지 않음: 서버가 시작되었는지와 신뢰 여부를 점검합니다.
- Docker에서 시작되지 않음: 서버 구성과 Docker 환경을 확인합니다.

## 요약

MCP 서버는 VS Code AI를 외부 데이터, 도구, 앱과 연결하는 확장점입니다. `mcp.json` 구성, 확장 갤러리 설치, 신뢰 관리, 샌드박스 설정 등을 통해 안전하고 유연하게 서버를 운영하세요.
