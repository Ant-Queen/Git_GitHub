# VSCode 에디터 03.01 로케일 (Locales)

## 한줄 요약
VS Code의 표시 언어(로케일)를 변경하고 언어팩을 설치/관리하는 방법을 안내합니다.

## 핵심 개념
- 표시 언어는 VS Code UI(메뉴, 커맨드 등)의 언어를 결정합니다.
- 언어팩(Language Pack) 확장으로 다양한 언어를 지원합니다.
- 로케일 설정은 `locale.json` 또는 명령 팔레트의 `Configure Display Language`로 변경합니다.

## 주요 기능
- `Configure Display Language` 명령: 현재 사용 가능한 언어 목록에서 선택 후 재시작으로 적용.
- `locale.json`(또는 argv.json의 `locale` 옵션)로 직접 설정 가능(특수한 환경이나 자동화에 유용).
- Marketplace에서 언어팩을 찾아 설치하면 해당 언어로 UI가 번역됩니다.

## 실무 팁
- 팀에서 동일한 UI 언어를 권장할 경우, 개발 문서에 설정 방법을 안내해 두면 신규 구성원이 빠르게 환경을 맞출 수 있습니다.
- 일부 번역이 불완전하거나 확장에 따라 달라질 수 있으니, 중요한 문구는 영어 원문도 병행해서 안내하세요.

## 핵심 정리
UI 언어는 간단히 변경 가능하며, `Configure Display Language`를 통해 직관적으로 관리할 수 있습니다. 자동화가 필요하면 설정 파일(`locale.json`)을 편집하세요.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/configure/locales
