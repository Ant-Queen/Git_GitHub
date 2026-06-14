# VS Code Copilot 서브에이전트 개요

## 개요

서브에이전트(Subagent)는 메인 에이전트의 하위 작업을 수행하는 독립적인 AI 에이전트입니다. 복잡한 작업을 분할하고, 격리된 컨텍스트에서 연구나 분석을 수행한 뒤 결과를 메인 에이전트에 요약해서 반환합니다.

## 사용자가 보는 모습

- 서브에이전트는 채팅에서 접을 수 있는 도구 호출 형태로 표시됩니다.
- 기본적으로 접혀 있으며, 이름과 현재 실행 중인 작업(예: "Reading file...")만 보입니다.
- 도구 호출을 확장하면 서브에이전트가 실행한 전체 도구 호출, 전달된 프롬프트, 반환된 결과를 확인할 수 있습니다.
- 이 방식은 메인 대화를 중복 없이 유지하면서 세부 작업을 추적할 수 있게 합니다.

## 사용 시나리오

서브에이전트는 다음과 같은 상황에서 유용합니다.

- 구현 전에 연구가 필요할 때
- 병렬 코드 분석이 필요할 때
- 여러 대안을 탐색할 때
- 특정 관점으로 코드 리뷰를 수행할 때
- 다중 모델 합의를 위해 여러 관점을 비교할 때

## 서브에이전트 호출

### 에이전트 주도 vs 사용자 호출

- 서브에이전트는 일반적으로 사용자가 직접 호출하기보다 메인 에이전트가 판단해 실행합니다.
- 메인 에이전트가 서브에이전트를 호출할 수 있도록 `runSubagent` 도구를 활성화해야 합니다.
- 기본적으로 서브에이전트는 다시 다른 서브에이전트를 호출할 수 없습니다. 재귀적 호출을 허용하려면 `chat.subagents.allowInvocationsFromSubagents` 설정을 켭니다.

### 호출 흐름

1. 사용자 또는 커스텀 에이전트 지침이 복잡한 작업을 설명합니다.
2. 메인 에이전트가 격리된 컨텍스트가 도움이 되는 하위 작업을 식별합니다.
3. 에이전트가 관련 하위 작업을 서브에이전트에 전달합니다.
4. 서브에이전트가 자율적으로 작업을 수행하고 요약을 반환합니다.
5. 메인 에이전트가 결과를 통합하고 작업을 계속합니다.

Tip: 일관된 서브에이전트 동작을 위해 커스텀 에이전트 지침에 서브에이전트 사용 규칙을 정의하는 것이 좋습니다.

### 프롬프트 파일에서 서브에이전트 호출

- `tools` frontmatter에 `runSubagent` 또는 `agent` 도구를 포함해야 합니다.
- 예:
  ```markdown
  ---
  name: document-feature
  tools: ['agent', 'read', 'search', 'edit']
  ---
  Run a subagent to research the new feature implementation details and return only information relevant for user documentation.
  Then update the docs/ folder with the new documentation.
  ```
- 프롬프트 설명에서 분리된 연구나 병렬 분석을 제안하면 서브에이전트 위임이 더 잘 활성화됩니다.

## 커스텀 에이전트를 서브에이전트로 실행

### 서브에이전트 호출 제어

- `user-invocable`: 에이전트가 채팅 드롭다운에 표시되는지를 제어합니다.
  - 기본값: `true`
  - `false`로 설정하면 서브에이전트 전용 에이전트를 만들 수 있습니다.
- `disable-model-invocation`: 다른 에이전트가 서브에이전트로 호출하지 못하도록 합니다.
  - 기본값: `false`

예:
```markdown
---
name: internal-helper
user-invocable: false
---

This agent can only be invoked as a subagent.
```

Note: `infer` 속성은 더 이상 권장되지 않으며, 대신 `user-invocable`과 `disable-model-invocation`을 사용하세요.

### 모델 선택

서브에이전트가 사용할 모델은 다음 우선순위로 결정됩니다.

1. `runSubagent` 도구에서 명시된 모델
2. 커스텀 에이전트의 `model` 속성
3. 메인 세션의 모델

- 프롬프트에서 특정 모델을 지정할 수 있습니다.
  - `Run a subagent with Claude Sonnet 4.6 to research authentication patterns in this codebase.`
  - `Use GPT-4o in a subagent to analyze the performance of this module.`
- 요청된 모델이 메인 모델의 비용 등급을 초과하면 메인 모델로 대체됩니다.

### 사용 가능한 서브에이전트 제한(실험적)

- 기본적으로 `disable-model-invocation: true`가 아닌 모든 커스텀 에이전트가 서브에이전트로 사용될 수 있습니다.
- `agents` 속성에 허용된 서브에이전트 목록을 지정하면 사용 가능한 에이전트를 제한할 수 있습니다.
- `agents: ['Edit', 'Search']`와 같이 특정 에이전트만 허용하거나 `[]`로 설정해 서브에이전트 사용을 금지할 수 있습니다.

예: TDD 워크플로에서 특정 에이전트만 사용하도록 제한
```markdown
---
name: TDD
tools: ['agent']
agents: ['Red', 'Green', 'Refactor']
---
Implement the following feature using test-driven development. Use subagents to guide the following steps:
1. Use the Red agent to write failing tests
2. Use the Green agent to implement code to pass the tests
3. Use the Refactor agent to improve the code quality
```

### 서브에이전트 동작 정의

- 서브에이전트는 기본적으로 메인 세션의 모델과 도구를 상속합니다.
- 커스텀 에이전트로 정의하면 해당 에이전트의 모델, 도구, 지침이 기본값을 덮어씁니다.
- 메인 에이전트가 특정 모델을 지정할 수도 있습니다.

## 중첩 서브에이전트

- 기본적으로 서브에이전트는 추가 서브에이전트를 호출할 수 없습니다.
- 재귀적 호출이 필요한 경우 `chat.subagents.allowInvocationsFromSubagents`를 활성화합니다.
- 최대 중첩 깊이는 5입니다.

### 재귀적 에이전트 예
```markdown
---
name: RecursiveProcessor
tools: ['agent', 'read', 'search']
agents: [RecursiveProcessor]
argument-hint: A list of items to process
---

You process a list of items by dividing and conquering:
- If the list has more than 4 items, split it in half and delegate each half to a RecursiveProcessor subagent.
- If the list has 4 or fewer items, process the items directly.
- Merge the results from each subagent into a final result.
```

## 오케스트레이션 패턴

### 코디네이터와 워커 패턴

- 코디네이터 에이전트는 전체 작업을 관리하고 전문화된 워커 서브에이전트에 하위 작업을 위임합니다.
- 워커 에이전트는 계획, 리뷰, 구현 등 특정 역할에 맞는 도구만 사용하도록 설계할 수 있습니다.
- 이렇게 하면 각각의 에이전트가 명확한 권한과 목적을 가지며 작업 효율이 향상됩니다.

예:
```markdown
---
name: Feature Builder
tools: ['agent', 'edit', 'search', 'read']
agents: ['Planner', 'Plan Architect', 'Implementer', 'Reviewer']
---
You are a feature development coordinator. For each feature request:
1. Use the Planner agent to break down the feature into tasks.
2. Use the Plan Architect agent to validate the plan against codebase patterns.
3. If the architect identifies reusable patterns or libraries, send feedback to the Planner to update the plan.
4. Use the Implementer agent to write the code for each task.
5. Use the Reviewer agent to check the implementation.
6. If the reviewer identifies issues, use the Implementer agent again to apply fixes.
```

- `Planner`, `Plan Architect`는 `read`, `search`와 같은 읽기 기반 도구를 사용합니다.
- `Implementer`는 실제 코드 작성을 담당하고 더 많은 도구를 사용할 수 있습니다.
- `Reviewer`는 구현 검토와 피드백을 담당합니다.

### 다중 관점 코드 리뷰

- 서로 다른 관점의 리뷰를 병렬로 수행하면 단일 리뷰에서 놓치기 쉬운 문제를 발견할 수 있습니다.
- 각 리뷰 관점을 서브에이전트로 실행한 뒤 결과를 종합합니다.

예:
```markdown
---
name: Thorough Reviewer
tools: ['agent', 'read', 'search']
---
You review code through multiple perspectives simultaneously. Run each perspective as a parallel subagent so findings are independent and unbiased.

When asked to review code, run these subagents in parallel:
- Correctness reviewer: logic errors, edge cases, type issues.
- Code quality reviewer: readability, naming, duplication.
- Security reviewer: input validation, injection risks, data exposure.
- Architecture reviewer: codebase patterns, design consistency, structural alignment.

After all subagents complete, synthesize findings into a prioritized summary. Note which issues are critical versus nice-to-have. Acknowledge what the code does well.
```

- 각 서브에이전트는 독립적인 컨텍스트를 사용하므로 다른 관점의 결과에 영향을 덜 받습니다.
- 보안 검토 에이전트는 보안 중심 도구를, 코드 품질 검토 에이전트는 린터/분석 도구를 각각 활용하면 좋습니다.

## 관련 리소스

- 에이전트 개요: https://code.visualstudio.com/docs/copilot/agents/overview
- 커스텀 에이전트: https://code.visualstudio.com/docs/copilot/customization/custom-agents
- 채팅 세션: https://code.visualstudio.com/docs/copilot/chat/chat-sessions

## 도움말 및 지원

- 커뮤니티에 질문하기
- 기능 요청 제출하기
- 이슈 보고하기
