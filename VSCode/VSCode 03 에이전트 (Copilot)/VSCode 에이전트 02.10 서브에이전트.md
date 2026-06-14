# VS Code에서 서브에이전트 사용하기

복잡한 작업을 처리할 때 서브에이전트를 사용하여 하위 작업을 위임할 수 있습니다. 서브에이전트는 독립적으로 실행되는 AI 에이전트로, 특정 작업(조사, 코드 분석, 검토 등)에 집중하고 결과를 메인 에이전트에 반환합니다.

더 깊이 있는 독립 보고서가 필요하면 Copilot CLI 세션에서 내장 [research agent](https://code.visualstudio.com/docs/agents/agent-types/copilot-cli#_run-deep-research-with-the-research-agent)를 사용하는 것이 좋습니다.

서브에이전트 개념(컨텍스트 분리, 동기 및 병렬 실행)에 대해서는 [Agents concepts](https://code.visualstudio.com/docs/agents/concepts/agents#_subagents)를 참고하세요.

이 문서는 VS Code에서 서브에이전트를 사용하는 방법, 호출 패턴, 사용자 지정 에이전트를 서브에이전트로 실행하는 방법을 설명합니다.

## 사용자 인터페이스

서브에이전트가 실행되면 채팅에서 접을 수 있는 도구 호출 형태로 표시됩니다. 기본적으로 서브에이전트는 접혀 있으며 다음 정보를 보여줍니다:

- 커스텀 에이전트 이름(지정한 경우)
- 현재 실행 중인 도구(예: "Reading file...", "Searching codebase...")

서브에이전트 도구 호출을 선택하면 전체 세부 정보가 표시됩니다. 여기에는 서브에이전트가 실행한 모든 도구 호출, 서브에이전트에 전달된 프롬프트, 반환된 결과가 포함됩니다.

이 방식은 중간 단계를 메인 대화를 어지럽히지 않으면서도 필요한 세부 수준을 제어할 수 있게 해줍니다.

## 서브에이전트 사용 사례

서브에이전트는 다음과 같은 상황에서 개발 워크플로우를 개선할 수 있습니다.

- 구현 전에 조사 실행
- 병렬 코드 분석
- 여러 솔루션 탐색
- 전문 관점을 가진 코드 리뷰
- 다중 모델 합의


## 서브에이전트 호출하기

### 에이전트가 시작하는 경우와 사용자가 직접 호출하는 경우

서브에이전트는 일반적으로 사용자가 채팅에서 직접 호출하는 대신 메인 에이전트에 의해 시작됩니다. 메인 에이전트가 서브에이전트를 호출하려면 `runSubagent` 도구가 활성화되어 있어야 합니다.

기본적으로 서브에이전트는 자체적으로 추가 서브에이전트를 호출할 수 없습니다. 재귀적 중첩을 허용하려면 `chat.subagents.allowInvocationsFromSubagents` 설정을 활성화하세요. 자세한 내용은 "Nested subagents" 섹션을 참고하세요.

메인 에이전트는 다음과 같은 패턴으로 동작합니다:

1. 사용자 또는 커스텀 에이전트 지침이 복잡한 작업을 설명합니다.
2. 메인 에이전트가 분리된 컨텍스트가 도움이 되는 하위 작업을 인식합니다.
3. 에이전트가 관련 하위 작업만 전달하여 서브에이전트를 시작합니다.
4. 서브에이전트가 자율적으로 작업하고 요약 결과를 반환합니다.
5. 메인 에이전트가 결과를 통합하여 계속 진행합니다.

프롬프트에서 서브에이전트 위임을 유도하려면 분리된 조사나 병렬 분석을 제안하는 방식으로 설명하세요.

> Tip: 일관성 있는 서브에이전트 동작을 위해서는 매번 직접 프롬프트에 지시하기보다는 커스텀 에이전트 지침에서 언제 서브에이전트를 사용할지 정의하는 것이 좋습니다.

서브에이전트 성능을 최적화하려면 작업과 기대 출력물을 명확히 정의하세요. 이렇게 하면 서브에이전트가 불필요한 컨텍스트를 메인 에이전트에 전달하지 않고 특정 목표에 집중할 수 있습니다.


### 프롬프트 파일에서 서브에이전트 호출하기

프롬프트 파일에서 서브에이전트를 호출하려면 `tools` frontmatter에 `runSubagent` 또는 `agent` 도구가 포함되어야 합니다.

```markdown
---
name: document-feature
tools: ['agent', 'read', 'search', 'edit']
---
Run a subagent to research the new feature implementation details and return only information relevant for user documentation.
Then update the docs/ folder with the new documentation.
```

프롬프트 지침에서 서브에이전트를 사용하도록 유도하려면 특정 하위 작업에 대해 분리된 조사나 병렬 분석을 제안하세요.


## 사용자 지정 에이전트를 서브에이전트로 실행하기

### 서브에이전트 호출 제어

커스텀 에이전트가 어떻게 호출될지 제어하려면 두 가지 frontmatter 속성을 사용합니다:

- `user-invocable`: 해당 에이전트가 채팅의 에이전트 드롭다운에 표시되는지 제어합니다. 기본값은 `true`입니다. `false`로 설정하면 서브에이전트로만 사용할 수 있습니다.
- `disable-model-invocation`: 다른 에이전트가 이 에이전트를 서브에이전트로 호출하지 못하게 합니다. 기본값은 `false`입니다. 일부 에이전트는 사용자만 명시적으로 호출하도록 제한해야 할 때 `true`로 설정하세요.

예: 서브에이전트로만 사용할 수 있는 에이전트

```markdown
---
name: internal-helper
user-invocable: false
---

This agent can only be invoked as a subagent.
```

> 주의: `infer` 속성은 더 이상 권장되지 않습니다. 더 세분화된 제어를 위해 `user-invocable`과 `disable-model-invocation`을 사용하세요.

### 특정 커스텀 에이전트를 서브에이전트로 실행하기

메인 에이전트가 서브에이전트로 커스텀 에이전트 또는 내장 에이전트를 사용하도록 요청할 수 있습니다. 예:

- `Run the Research agent as a subagent to research the best auth methods for this project.`
- `Use the Plan agent in a subagent to create an implementation plan for myfeature. Then save the plan in plans/myfeature.plan.md`


### 서브에이전트 모델 선택

서브에이전트가 실행될 때 모델은 다음 우선순위로 결정됩니다:

1. 메인 에이전트가 `runSubagent` 도구 호출 시 명시한 모델
2. 커스텀 에이전트 `.agent.md` frontmatter의 `model` 속성
3. 메인 세션의 모델

서브에이전트에 특정 모델을 요청하려면 프롬프트에 모델 선호도를 포함하세요.

- `Run a subagent with Claude Sonnet 4.6 to research authentication patterns in this codebase.`
- `Use GPT-4o in a subagent to analyze the performance of this module.`

또는 커스텀 에이전트 지침에 모델 선호도를 정의하여 일관되게 특정 모델로 서브에이전트를 실행할 수 있습니다.

> 주의: 요청한 모델이 메인 모델보다 비용 등급이 높으면 서브에이전트는 메인 모델로 대체됩니다.


### 사용 가능한 서브에이전트 제한하기(실험적)

기본적으로 `disable-model-invocation: true`가 없는 모든 커스텀 에이전트는 서브에이전트로 사용 가능합니다. 이름이나 설명이 비슷한 에이전트가 여러 개 있으면 AI가 의도하지 않은 에이전트를 선택할 수 있습니다.

메인 에이전트 frontmatter에 `agents` 속성을 지정하여 사용할 수 있는 커스텀 에이전트를 제한할 수 있습니다.

- 에이전트 이름 목록(`['Edit', 'Search']`)으로 특정 에이전트만 허용
- `*`로 모든 사용 가능 에이전트 허용(기본)
- `[]`로 서브에이전트 사용 금지

> 주의: `agents` 배열에 에이전트를 명시적으로 나열하면 `disable-model-invocation: true`를 무시합니다. 특정 코디네이터 에이전트가 명시적으로 접근을 허용한 에이전트만 사용할 수 있게 할 때 유용합니다.

예: TDD 워크플로우에서 특정 서브에이전트만 허용

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


## 중첩 서브에이전트

### 재귀 에이전트 예시

재귀 에이전트는 자신을 `agents` 속성에 포함하여 스스로에게 작업을 위임할 수 있습니다. 이 방법은 큰 작업을 분할하여 각 부분을 새로운 인스턴스에게 위임하는 분할 정복 패턴에 유용합니다.

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

기본적으로 서브에이전트는 추가 서브에이전트를 생성할 수 없습니다. 이는 에이전트가 무한 루프에 빠지는 것을 방지합니다. 그러나 일부 워크플로우에서는 재귀 위임이 도움이 됩니다.

`chat.subagents.allowInvocationsFromSubagents` 설정을 활성화하면 서브에이전트가 최대 5단계 깊이까지 자체 서브에이전트를 생성할 수 있습니다.


## 오케스트레이션 패턴

서브에이전트는 코디네이터 에이전트가 전문화된 워커 에이전트에게 작업을 위임하는 오케스트레이션 패턴에도 적합합니다. 이 방식은 각 에이전트를 해당 작업에 집중시키고 전체 워크플로우를 명확하게 유지할 수 있습니다.

### 코디네이터와 워커 패턴

코디네이터 에이전트는 전체 작업을 관리하고 전문 워커 에이전트에 하위 작업을 위임합니다. 각 워커 에이전트는 적절한 도구만 갖추고 더 빠르거나 비용 효율적인 모델을 사용할 수 있습니다.

예시:

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

각 워커 에이전트는 다음처럼 정의할 수 있습니다:

```markdown
---
name: Planner
user-invocable: false
tools: ['read', 'search']
---
Break down feature requests into implementation tasks. Incorporate feedback from the Plan Architect.
```

```markdown
---
name: Plan Architect
user-invocable: false
tools: ['read', 'search']
---
Validate plans against the codebase. Identify existing patterns, utilities, and libraries that should be reused. Flag any plan steps that duplicate existing functionality.
```

```markdown
---
name: Implementer
user-invocable: false
model: ['Claude Haiku 4.5 (copilot)', 'Gemini 3 Flash (Preview) (copilot)']
---
Write code to complete assigned tasks.
```

이 패턴은 코디네이터의 컨텍스트를 고수준 워크플로우에 집중시키고, 각 워커가 고유한 권한과 적절한 도구를 가진 깔끔한 컨텍스트에서 작업하게 합니다.


### 다중 관점 코드 리뷰

코드 리뷰는 여러 관점에서 병렬로 실행할 때 더욱 효과적입니다. 단일 리뷰 패스는 다른 시각에서 보면 놓치기 쉬운 문제를 발견하지 못할 수 있습니다.

서브에이전트를 사용하여 각 리뷰 관점을 병렬로 실행한 다음, 결과를 종합하여 우선순위가 매겨진 요약을 만드세요.

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

이 패턴은 각 서브에이전트가 다른 관점을 독립적으로 유지하면서 코드를 검토하게 합니다.

> Tip: 더 세밀한 제어를 원한다면 각 리뷰 관점을 전문화된 도구 액세스를 가진 별도의 커스텀 에이전트로 만들 수 있습니다.


## 관련 자료

- [Agents overview](https://code.visualstudio.com/docs/agents/overview)
- [Custom agents](https://code.visualstudio.com/docs/agent-customization/custom-agents)
- [Chat sessions](https://code.visualstudio.com/docs/agents/sessions/chat-sessions)
