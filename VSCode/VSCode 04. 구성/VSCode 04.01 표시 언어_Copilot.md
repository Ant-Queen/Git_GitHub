# VS Code 표시 언어 설정 가이드

원문: https://code.visualstudio.com/docs/configure/locales

## 1. 개요

Visual Studio Code는 기본적으로 영어 UI를 사용하며, 다른 언어는 Language Pack 확장을 통해 제공됩니다. 운영 체제의 UI 언어를 감지하여 적절한 Language Pack 설치를 권장합니다.

## 2. 표시 언어 변경하기

### Configure Display Language 명령 사용

1. `Ctrl+Shift+P`를 눌러 Command Palette 실행
2. "display"를 입력하여 `Configure Display Language` 명령 선택
3. 사용 가능한 로케일 목록에서 원하는 언어 선택
4. Language Pack이 설치되어 있지 않으면 자동으로 설치
5. 언어를 변경하면 VS Code를 재시작하라는 메시지가 나타남

### `argv.json` 파일 직접 편집

- `Preferences: Configure Runtime Arguments` 명령으로 `argv.json` 파일 열기
- 언어를 직접 설정할 수 있으며, 변경 후 VS Code를 재시작해야 적용됨

## 3. 사용 가능한 로케일

VS Code는 다음 로케일을 제공합니다:

- English (US): `en`
- Simplified Chinese: `zh-cn`
- Traditional Chinese: `zh-tw`
- French: `fr`
- German: `de`
- Italian: `it`
- Spanish: `es`
- Japanese: `ja`
- Korean: `ko`
- Russian: `ru`
- Portuguese (Brazil): `pt-br`
- Turkish: `tr`
- Polish: `pl`
- Czech: `cs`
- Hungarian: `hu`

## 4. Marketplace Language Packs

### Language Pack 설치 방법

- Extensions 뷰 (`Ctrl+Shift+X`) 열기
- 찾기 창에 언어 이름과 `category:"Language Packs"` 입력
- 원하는 Language Pack 설치

### 여러 Language Pack 설치

여러 Language Pack을 동시에 설치할 수 있으며, `Configure Display Language` 명령으로 현재 표시 언어를 선택할 수 있습니다.

## 5. 언어 설정 방법

### 명령줄에서 로케일 지정

VS Code를 특정 언어로 실행하려면 `--locale` 옵션을 사용합니다. 예:

```bash
code . --locale=fr
```

- 지정한 로케일에 해당하는 Language Pack이 설치되어 있어야 함
- 설치되지 않은 경우 영어로 표시됨

## 6. 자주 묻는 질문

### Q: `argv.json` 파일에 기록할 수 없습니다

- 이전 변경으로 `argv.json` 파일이 저장되지 않았을 수 있음
- `Preferences: Configure Runtime Arguments`를 열어 파일 오류를 확인하고 저장
- 저장 후 다시 Language Pack 설치 시도

### Q: Language Pack 번역에 기여할 수 있나요?

- 예, [Visual Studio Code Community Localization Project](https://aka.ms/vscodeloc)에서 번역을 기여하거나 투표할 수 있습니다.

### Q: Python 같은 프로그래밍 언어는 어떻게 활성화하나요?

- 표시 언어와는 별도로, 프로그래밍 언어 지원은 [Programming Languages](https://code.visualstudio.com/docs/languages/overview) 문서를 참고하세요.

## 7. 참고 사항

- 이 문서는 VS Code UI 표시 언어 변경에 대한 내용입니다.
- C++, Java 등 프로그래밍 언어 지원은 Language Pack이 아닌 확장으로 설치합니다.

---

**최종 업데이트**: 2026년 5월 10일