# VS Code에서 AI 보안

AI 기반 개발 기능은 다양한 작업을 자율적으로 수행할 수 있으므로 보안에 중요한 영향을 줄 수 있습니다. 이 문서는 VS Code의 내장 보안 보호 기능, 주의해야 할 위험, 그리고 안전한 AI 지원 개발을 위한 환경 구성 방법을 설명합니다.

> 참고: 이 문서는 VS Code 편집기의 AI 보안 제어를 다룹니다. GitHub Copilot의 데이터, 개인정보 및 규정 준수는 [GitHub Copilot Trust Center](https://resources.github.com/copilot-trust-center/)를 참조하세요. 조직 전체 AI 정책과 제어는 [AI settings for your organization](https://code.visualstudio.com/docs/enterprise/ai-settings) 및 [enterprise policies](https://code.visualstudio.com/docs/enterprise/policies)를 확인하세요.

## 권장 보안 기준

안전한 AI 지원 개발을 위해 다음 체크리스트를 따르세요.

1. 검증되지 않은 프로젝트는 제한된 모드로 엽니다. 악성 콘텐츠 검토 전까지는 워크스페이스 트러스트 경계를 활용하세요. 제한된 모드는 해당 워크스페이스에서 에이전트를 비활성화합니다.
2. 에이전트 샌드박싱을 활성화합니다. macOS와 Linux(Windows의 WSL2 포함)에서 `chat.tools.terminal.sandbox.enabled`를 활성화하여 에이전트가 실행하는 명령의 파일 시스템 및 네트워크 액세스를 제한하세요.
3. 모든 파일 편집은 수락 전에 검토합니다. [diff editor](https://code.visualstudio.com/docs/chat/review-code-edits)를 사용해 제안된 변경 사항을 검사하고 개별 변경을 유지하거나 되돌립니다.
4. 민감한 파일을 보호합니다. 예를 들어 `chat.tools.edits.autoApprove`에 `