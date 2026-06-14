# VS Code 에이전트에서 메모리 사용하기

Visual Studio Code의 에이전트는 대화를 통해 메모리를 사용하여 컨텍스트를 유지합니다. 매번 세션을 처음부터 시작하는 대신, 에이전트는 사용자의 선호도를 기억하고 이전 작업에서 배운 내용을 적용하며 코드베이스에 대한 지식을 쌓아갑니다.

메모리가 에이전트 아키텍처에 어떻게 맞는지 보려면 [Agents concepts](https://code.visualstudio.com/docs/agents/concepts/agents#_memory)를 참조하세요.

이 문서는 VS Code에서 메모리 도구를 사용하는 방법, 메모리 파일을 관리하는 방법, Copilot Memory가 개발 워크플로우 전체에서 메모리를 확장하는 방법을 설명합니다.

## 메모리 도구

메모리 도구는 VS Code의 내장 에이전트 도구로, 에이전트가 작업 중에 메모를 저장하고 불러올 수 있게 합니다. 에이전트에 명시적으로 무언가를 기억하도록 요청할 수도 있습니다. 모든 데이터는 로컬 컴퓨터에 저장됩니다. 메모리 도구는 기본적으로 활성화되어 있습니다.

> 참고: 메모리 도구는 현재 미리보기 상태입니다. `github.copilot.chat.tools.memory.enabled` 설정으로 활성화 또는 비활성화할 수 있습니다.

### 메모리 범위

각 범위는 정보가 얼마나 오래 유지되어야 하는지와 어디에 적용되는지에 따라 다르게 사용됩니다.

| 범위 | 파일 경로 | 세션 간 지속 | 작업공간 간 지속 | 용도 |
|---|---|---|---|---|
| 사용자 | `/memories/` | 예 | 예 | 일반적인 선호도, 패턴, 자주 사용하는 명령 |
| 리포지토리 | `/memories/repo/` | 예 | 아니요 (워크스페이스 범위) | 특정 코드베이스의 아키텍처 결정, 명명 규칙, 빌드 명령 |
| 세션 | `/memories/session/` | 아니요 (대화 종료 시 삭제) | 아니요 | 작업별 컨텍스트, 진행 중인 계획 |

#### 사용자 메모리

사용자 메모리는 모든 워크스페이스와 대화에 걸쳐 지속됩니다. 세션이 시작될 때 첫 200줄이 자동으로 에이전트 컨텍스트에 로드됩니다. 프로젝트와 관계없이 적용되는 일반적인 선호도와 통찰을 위해 사용자 메모리를 사용하세요.

예:

```text
Remember that I prefer tabs over spaces and always use single quotes in JavaScript
```

나중 대화에서 다른 워크스페이스에서도 에이전트가 이 선호도를 기억하고 생성한 코드에 적용합니다.

#### 리포지토리 메모리

리포지토리 메모리는 현재 워크스페이스에 범위가 지정되며 해당 워크스페이스의 대화 간에 지속됩니다. 데이터 액세스 패턴, 명명 규칙, 빌드 명령 같은 특정 코드베이스 관련 사실에 리포지토리 메모리를 사용하세요.

예:

```text
Remember that this project uses the repository pattern for data access and all API endpoints require authentication
```

#### 세션 메모리

세션 메모리는 현재 대화에 범위가 지정되며 대화가 종료되면 삭제됩니다. 다단계 작업을 진행하는 동안 임시 작업 노트나 작업별 컨텍스트를 위해 세션 메모리를 사용하세요.

Plan 에이전트는 구현 계획을 `plan.md` 파일로 세션 메모리에 저장합니다. 이 계획은 세션 동안 사용할 수 있으며 `Chat: Show Memory Files` 명령으로 볼 수 있지만 이후 세션에서는 사용할 수 없습니다. [에이전트로 계획 세우기](https://code.visualstudio.com/docs/agents/planning)를 참고하세요.

### 메모리 저장 및 검색

메모리를 저장하려면 자연어로 에이전트에게 무언가를 기억하도록 요청합니다. 에이전트가 적절한 범위를 판단하고 해당 메모리 파일을 생성하거나 업데이트합니다.

```text
Remember that our team uses conventional commits for all commit messages
```

메모리를 검색하려면 새 대화에서 해당 내용을 물어보세요. 에이전트는 메모리 파일을 확인하고 관련 정보를 기억합니다.

```text
What are our commit message conventions?
```

에이전트 채팅 응답에 메모리 파일 참조가 표시되면 클릭하여 파일 내용을 직접 볼 수 있습니다.

### 메모리 파일 관리

VS Code는 메모리 파일을 보고 관리하는 명령을 제공합니다:

- `Chat: Show Memory Files`: 모든 범위의 메모리 파일 목록을 열고 파일 내용을 선택하여 확인합니다.
- `Chat: Clear All Memory Files`: 모든 범위의 메모리 파일을 제거합니다.

> 참고: 개별 메모리 파일 삭제는 아직 지원되지 않습니다. 모든 메모리를 제거하려면 `Chat: Clear All Memory Files`를 사용하거나, 오래된 정보를 제거하려면 에이전트에게 특정 메모리 파일을 업데이트하도록 요청하세요.

## Copilot Memory

Copilot Memory는 로컬 메모리 도구와 별개로 GitHub에서 호스팅되는 메모리 시스템입니다. Copilot 에이전트가 작업할 때 저장소 범위의 통찰을 자동으로 캡처합니다.

### Copilot Memory 작동 방식

Copilot Memory는 다음과 같은 특징이 있습니다:

- 저장소 범위: 메모리는 특정 저장소에 연결되며 쓰기 권한이 있는 기여자만 생성할 수 있습니다.
- 에이전트 간 공유: 하나의 Copilot 에이전트가 학습한 내용은 다른 에이전트에서도 사용할 수 있습니다.
- 사용 전 검증: 에이전트는 현재 코드베이스에 대해 메모리를 검증한 후 적용하여 오래된 정보가 결과에 영향을 주지 않도록 합니다.
- 자동 만료: 정보가 오래된 메모리는 28일 후에 삭제됩니다.

### Copilot Memory 활성화

Copilot Memory는 기본적으로 꺼져 있으며 GitHub 설정에서 활성화해야 합니다.

- 개인 사용자(Copilot Pro 또는 Pro+): GitHub의 [개인 Copilot 설정](https://github.com/settings/copilot)에서 Copilot Memory를 활성화합니다.
- 조직 및 엔터프라이즈: 조직 또는 엔터프라이즈 설정에서 정책으로 활성화합니다.

또한 VS Code에서 `github.copilot.chat.copilotMemory.enabled` 설정으로 Copilot Memory 통합을 활성화해야 합니다.

저장소 소유자는 Repository Settings > Copilot > Memory에서 저장된 메모리를 검토하고 삭제할 수 있습니다.

자세한 설정 방법은 GitHub 문서의 [Enabling and curating Copilot Memory](https://docs.github.com/copilot/how-tos/use-copilot-agents/copilot-memory)를 참조하세요.

### 메모리 도구와 Copilot Memory 비교

| 항목 | 메모리 도구 | Copilot Memory |
|---|---|---|
| 저장 위치 | 로컬(내 컴퓨터) | GitHub 호스팅(원격) |
| 범위 | 사용자, 리포지토리, 세션 | 리포지토리 전용 |
| Copilot 서비스 간 공유 | 아니요 (VS Code 전용) | 예 (코딩 에이전트, 코드 리뷰, CLI 등) |
| 생성 주체 | 사용자 또는 채팅 중 에이전트 | Copilot 에이전트가 자동 생성 |
| 기본 활성화 여부 | 예 | 아니요 (옵트인) |
| 만료 | 수동 관리 | 자동(28일) |

두 시스템은 상호 보완적입니다. 개인 선호도와 세션별 컨텍스트에는 로컬 메모리 도구를 사용하고, 저장소 지식은 개발 워크플로우 전반에 걸쳐 이점을 주는 Copilot Memory를 사용하세요.

> 참고: Copilot Memory는 미리보기 상태이며 위에서 설명한 로컬 메모리 도구와 별개입니다.

## 관련 자료

- [에이전트로 계획 세우기](https://code.visualstudio.com/docs/agents/planning)
- [에이전트 도구](https://code.visualstudio.com/docs/agents/agent-tools)
- [Enabling and curating Copilot Memory](https://docs.github.com/copilot/how-tos/use-copilot-agents/copilot-memory)
- [Building an agentic memory system for GitHub Copilot](https://github.blog/ai-and-ml/github-copilot/building-an-agentic-memory-system-for-github-copilot/)

## 도움말 및 지원

- 커뮤니티에 질문하기: https://stackoverflow.com/questions/tagged/vscode
- 기능 요청: https://go.microsoft.com/fwlink/?LinkID=533482
- 문제 보고: https://www.github.com/Microsoft/vscode/issues
