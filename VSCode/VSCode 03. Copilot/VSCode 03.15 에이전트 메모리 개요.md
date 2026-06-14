# VS Code Copilot 에이전트 메모리 개요

## 개요

VS Code 에이전트는 메모리를 사용해 대화 간 컨텍스트를 유지합니다. 메모리를 통해 에이전트는 선호도, 코드베이스 정보, 작업별 임시 상태 등을 기억하고 더 일관된 결과를 제공합니다.

## 메모리 도구(Memory tool)

메모리 도구는 VS Code에 내장된 에이전트 도구로, 에이전트가 작업 도중에 메모를 저장하고 필요할 때 꺼내볼 수 있게 합니다. 모든 데이터는 로컬에 저장되며 기본적으로 활성화되어 있습니다.

### 메모리 범위

| 범위 | 저장 위치 | 유지 기간 | 공유 여부 | 사용 예시 |
|---|---|---|---|---|
| 사용자 메모리 | `/memories/` | 영구 | 예 | 탭 vs 스페이스, 코드 스타일 선호도 |
| 리포지토리 메모리 | `/memories/repo/` | 영구 (워크스페이스 한정) | 아니오 | 아키텍처 결정, 명명 규칙, 빌드 명령 |
| 세션 메모리 | `/memories/session/` | 대화 종료 시 삭제 | 아니오 | 작업별 임시 노트, 진행 중 계획 |

#### 사용자 메모리
- 모든 워크스페이스와 대화에 걸쳐 유지됩니다.
- 세션 시작 시 처음 200줄이 자동으로 에이전트 컨텍스트에 로드됩니다.
- 예: `Remember that I prefer tabs over spaces and always use single quotes in JavaScript`

#### 리포지토리 메모리
- 현재 워크스페이스에 국한됩니다.
- 해당 리포지토리의 대화 간에 유지됩니다.
- 예: `Remember that this project uses the repository pattern for data access and all API endpoints require authentication`

#### 세션 메모리
- 현재 대화에만 유효하며 대화 종료 시 삭제됩니다.
- 작업 진행 중 임시 노트를 저장하는 데 적합합니다.
- Plan 에이전트는 구현 계획을 `/memories/session/plan.md`에 저장합니다.
- 세션 중 `Chat: Show Memory Files` 명령으로 `plan.md`를 열 수 있습니다.

### 메모리 저장 및 조회

- 자연어로 에이전트에게 기억하도록 지시하면, 에이전트가 적절한 범위의 메모리 파일을 생성하거나 업데이트합니다.
  - 예: `Remember that our team uses conventional commits for all commit messages`
- 새로운 대화에서 관련 정보를 물으면, 에이전트는 메모리 파일을 확인하고 내용을 기억해 답변합니다.
  - 예: `What are our commit message conventions?`
- 에이전트가 참조하는 메모리 파일은 채팅 응답에 클릭 가능한 링크로 표시됩니다.

### 메모리 파일 관리

- `Chat: Show Memory Files`: 모든 메모리 파일 목록을 열어 내용을 확인합니다.
- `Chat: Clear All Memory Files`: 모든 메모리 파일을 삭제합니다.
- 개별 메모리 파일 삭제는 아직 지원되지 않습니다.
- 오래된 정보를 지우려면 에이전트에게 해당 메모리를 업데이트하도록 요청하거나 전체 메모리를 삭제합니다.

## Copilot Memory

Copilot Memory는 GitHub에서 호스팅되는 별도의 저장소 기반 메모리 시스템입니다. VS Code 메모리 도구와는 다르며 Copilot의 여러 서비스에서 공유됩니다.

### Copilot Memory 작동 방식

- 리포지토리 범위로 저장됩니다.
- 저장소 기여자의 쓰기 권한이 있는 사람만 생성할 수 있습니다.
- 여러 Copilot 에이전트 간에 공유됩니다.
- 사용 전에 현재 코드베이스와 검증되어 stale한 정보 사용을 방지합니다.
- 28일 후 자동 만료됩니다.

### Copilot Memory 활성화

- 기본적으로 꺼져 있으며 GitHub 설정에서 활성화해야 합니다.
- 개인 사용자(Copilot Pro/Pro+): GitHub 개인 Copilot 설정에서 활성화합니다.
- 조직/엔터프라이즈: 정책 설정을 통해 활성화합니다.
- VS Code에서는 `github.copilot.chat.copilotMemory.enabled` 설정을 켜야 합니다.
- 리포지토리 소유자는 GitHub 리포지토리 설정 > Copilot > Memory에서 저장된 메모리를 검토 및 삭제할 수 있습니다.
- 자세한 설정은 GitHub 문서 `Enabling and curating Copilot Memory`를 참고합니다.

### 메모리 도구 vs Copilot Memory

| 항목 | 메모리 도구 | Copilot Memory |
|---|---|---|
| 저장 위치 | 로컬 | GitHub 호스팅 원격 |
| 범위 | 사용자, 리포지토리, 세션 | 리포지토리 전용 |
| Copilot 서비스 간 공유 | 아니오 (VS Code 전용) | 예 (클라우드 에이전트, 코드 리뷰, CLI 등) |
| 생성 주체 | 사용자 또는 에이전트 | Copilot 에이전트 자동 생성 |
| 기본 활성화 | 예 | 아니오 (옵트인) |
| 만료 | 수동 관리 | 자동 28일 |

두 시스템은 상호 보완적입니다.
- 로컬 메모리 도구는 개인 선호도와 세션 컨텍스트에 적합합니다.
- Copilot Memory는 리포지토리 지식과 협업에 적합합니다.

## 관련 리소스

- [에이전트 계획](https://code.visualstudio.com/docs/copilot/agents/planning)
- [에이전트 도구 구성](https://code.visualstudio.com/docs/copilot/agents/agent-tools)
- [Copilot Memory 활성화 및 관리](https://docs.github.com/copilot/how-tos/use-copilot-agents/copilot-memory)
- [GitHub Copilot 메모리 시스템 블로그](https://github.blog/ai-and-ml/github-copilot/building-an-agentic-memory-system-for-github-copilot/)

## 도움말 및 지원

- 커뮤니티에 질문하기
- 기능 요청 제출하기
- 이슈 보고하기
