# VS Code 에이전트 커스터마이징 - Custom Instructions

원문: https://code.visualstudio.com/docs/agent-customization/custom-instructions

---

## 1. 한 줄 요약

Custom Instructions는 프로젝트나 파일 유형별로 AI에게 일관된 규칙을 자동으로 알려주는 기능입니다.

---

## 2. 무엇을 위해 쓰나?

다음 같은 내용을 넣을 때 유용합니다.

- 코드 스타일 규칙
- 네이밍 규칙
- 아키텍처 원칙
- 보안 요구사항
- 문서 작성 기준

즉, 매번 프롬프트에 같은 지시를 반복하지 않아도 됩니다.

---

## 3. 주요 유형

### Always-on Instructions
- 항상 적용되는 규칙입니다.
- 예: 프로젝트 전역 스타일 규칙

### File-based Instructions
- 특정 파일 패턴이나 폴더에만 적용됩니다.
- 예: Python, React, 테스트 파일만 다른 규칙 적용

### AGENTS.md / CLAUDE.md
- 여러 AI 에이전트나 Claude 계열 도구와 공통 규칙을 공유할 때 사용합니다.

---

## 4. 흔히 쓰는 파일 위치

- 워크스페이스 수준: `.github/copilot-instructions.md`
- 특정 파일 규칙: `.github/instructions/*.instructions.md`
- 사용자 수준: 개인 프로필 기준으로 공유되는 지시사항

---

## 5. 예시 구조

```md
---
name: Python Standards
applyTo: '**/*.py'
---
- Use PEP 8
- Add type hints
- Write docstrings
```

이처럼 YAML frontmatter로 언제 적용할지 지정할 수 있습니다.

---

## 6. 실무 팁

- 규칙은 짧고 핵심적으로 쓰는 것이 좋습니다.
- 이유까지 함께 적으면 AI가 더 잘 따라갑니다.
- 팀 공통 규칙은 workspace 수준으로 저장하면 공유에 좋습니다.

---

## 7. 핵심 정리

Custom Instructions는 “AI에게 내 프로젝트의 룰을 미리 알려주는 설정”입니다. 반복 설명을 줄이고, 결과의 일관성을 높이는 데 매우 유용합니다.

---

> 이 문서는 VS Code 공식 Custom instructions 페이지를 기반으로 한국어로 요약 정리한 내용입니다.
