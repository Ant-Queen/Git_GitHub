# VSCode 에디터 02.09 리팩토링

## 한줄 요약
리팩토링은 코드의 동작은 유지하면서 구조를 더 명확하고 재사용 가능하게 바꾸는 작업이며, VS Code는 이를 편집기 안에서 직접 지원합니다.

## 핵심 개념
- Refactoring은 코드 구조를 개선하는 작업입니다.
- Code Action(Quick Fix)와 Refactor 기능을 통해 Extract Method, Extract Variable, Rename Symbol 등을 지원합니다.
- 리팩토링은 언어 서비스가 지원하는 경우에 더 잘 동작합니다.
- Refactor Preview를 통해 적용 전 변경 내용을 미리 확인할 수 있습니다.

## 주요 기능
- Ctrl+. 또는 lightbulb로 Code Action 열기
- Ctrl+Shift+R로 리팩토링 메뉴 열기
- Extract Method / Extract Variable
- Rename Symbol(F2)
- Refactor Preview로 변경 내용 미리 보기

## 실무 팁
- 리팩토링은 코드 중복을 줄이거나 가독성을 올릴 때 특히 유용합니다.
- 변경 전에는 Preview를 보고 적용 범위를 확인하는 것이 안전합니다.
- 언어별 확장 기능이 있으면 더 풍부한 리팩토링 지원을 받을 수 있습니다.

## 핵심 정리
리팩토링은 “코드를 더 좋게 만드는 작업”이며, VS Code는 이를 편집기 안에서 자연스럽게 수행할 수 있게 도와줍니다.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/editing/refactoring
