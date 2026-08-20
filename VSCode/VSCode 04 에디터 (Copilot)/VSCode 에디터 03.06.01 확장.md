# VSCode 에디터 03.06.01 확장 (Extensions)

## 한줄 요약
확장은 VS Code의 기능을 확장하는 플러그인으로 언어 지원, 디버깅, 테마 등 다양한 기능을 제공합니다.

## 핵심 개념
- 확장은 기능(기능 추가, UI 확장, 언어 서버 등)을 패키지로 제공하며 Marketplace에서 설치됩니다.
- 확장은 `extension` API를 통해 에디터와 상호작용하며 활성화 이벤트(onStartupFinished, onLanguage 등)를 가집니다.
- 확장에는 권한, 실행 환경(Extension Host), 기여 포인트(contributions)를 명시합니다.

## 주요 기능
- 언어 지원: 문법 강조, IntelliSense, 포맷터 제공
- 디버깅: 런처 및 디버그 어댑터 추가
- UI 확장: 뷰, 패널, 명령, 설정 등 기여
- 테마 및 아이콘 팩: 시각적 변경 가능

## 실무 팁
- 필요 없는 확장은 비활성화해 성능 저하를 방지하세요.
- 확장 개발 시 `activationEvents`를 최소화해 Extension Host 부팅 시간을 줄이세요.
- 확장 설정과 권한을 문서화해 팀원에게 알려주세요.

## 핵심 정리
확장은 VS Code의 기능을 맞춤화하는 핵심 수단입니다. 설치와 관리가 쉽지만 과도한 확장 사용은 성능에 영향을 줄 수 있으므로 신중히 선택하세요.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/configure/extensions/extensions
