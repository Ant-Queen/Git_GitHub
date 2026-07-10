# VSCode 에이전트 06.04 Copilot 커스터마이징 가이드

## 한줄 요약
VS Code에서는 프로젝트별 규칙, 파일별 지침, 프롬프트 파일, 커스텀 에이전트, 스킬을 조합해 Copilot의 동작을 맞춤화할 수 있습니다.

## 핵심 개념
- .github/copilot-instructions.md: 프로젝트 전체에 공통으로 적용되는 규칙
- *.instructions.md: 특정 파일 타입이나 폴더에만 적용되는 지침
- *.prompt.md: 자주 쓰는 작업을 슬래시 명령으로 재사용
- *.agent.md: 역할이 명확한 커스텀 에이전트
- SKILL.md: 특정 워크플로우를 반복적으로 수행하는 스킬

## 실무 흐름
1. 프로젝트 코딩 규칙을 정리한다.
2. 파일별 지침을 추가한다.
3. 반복 작업용 프롬프트를 만든다.
4. 역할별 에이전트를 만든다.
5. 전문 워크플로우용 스킬을 붙인다.

## 핵심 정리
커스터마이징은 “AI가 내 프로젝트에 맞게 동작하도록 만드는 설정”입니다.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/agents/guides/customize-copilot-guide
