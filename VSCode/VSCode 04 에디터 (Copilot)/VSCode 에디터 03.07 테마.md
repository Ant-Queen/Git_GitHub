# VSCode 에디터 03.07 테마 (Themes)

## 한줄 요약
테마는 에디터의 색상과 아이콘 스타일을 바꾸어 시인성과 작업 환경 분위기를 조절하는 시각 설정입니다.

## 핵심 개념
- 색상 테마(Color Theme): 편집기, 사이드바, 패널 등 UI 요소의 색 조합을 정의합니다.
- 아이콘 테마(File Icon Theme): 파일/폴더 아이콘의 시각 표현을 변경합니다.
- 테마는 Marketplace에서 설치하거나 직접 만들어 배포할 수 있습니다.

## 주요 기능
- `Preferences: Color Theme`로 색상 테마 변경 가능.
- `Preferences: File Icon Theme`로 아이콘 테마 선택.
- 개발자 도구(`Developer: Generate Color Theme From Current Settings`)로 현재 설정 기반 테마 생성 가능.
- 테마 확장은 `contributes.themes` 또는 `contributes.iconThemes`를 통해 기여 포인트를 사용합니다.

## 실무 팁
- 가독성이 중요한 작업(예: 장시간 코딩)에서는 콘트라스트가 높은 테마를 선택하세요.
- 팀에서 통일된 색상/아이콘 사용이 필요하면 테마 패키지를 공유하면 편리합니다.
- 자신만의 테마를 만들 때는 명도와 강조색을 기준으로 에디터, 구문 강조, UI 요소를 구분하세요.

## 핵심 정리
테마는 개발 환경의 시각적 일관성과 가독성을 높이는 도구입니다. 설치·선택이 간단하므로 자신의 작업 스타일에 맞는 테마를 찾아 적용하세요.

## 참고
- 공식 문서: https://code.visualstudio.com/docs/configure/themes
