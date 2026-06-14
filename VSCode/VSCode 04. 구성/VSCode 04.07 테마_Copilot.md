# VS Code 테마 정리

## 1. 테마 개요
- VS Code에서 테마는 UI 색상, 편집기 하이라이트, 파일 아이콘, 제품 아이콘 등을 변경합니다.
- 주요 테마 종류:
  - 색 테마(Color Theme)
  - 파일 아이콘 테마(File Icon Theme)
  - 제품 아이콘 테마(Product Icon Theme)

## 2. 색 테마(Color Themes)
### 2.1. 테마 선택 방법
1. `파일 > 기본 설정 > 테마 > 색 테마` 선택
2. `Preferences: Color Theme` 명령 실행 (`Ctrl+K Ctrl+T`)
3. 위/아래 화살표로 미리 보기 후 Enter로 선택

### 2.2. 설정 저장 위치
- 기본적으로 사용자 설정에 저장되어 모든 워크스페이스에서 적용됩니다.
- 설정 예시:
```json
"workbench.colorTheme": "Solarized Dark"
```

### 2.3. 워크스페이스별 테마
- 워크스페이스 설정으로 특정 폴더 전용 테마를 지정할 수 있습니다.
- 워크스페이스 설정은 `.vscode/settings.json`에 저장됩니다.

## 3. 마켓플레이스에서 색 테마 가져오기
- 기본 제공 테마 외에 확장에서 더 많은 테마를 설치할 수 있습니다.
- 색 테마 선택기에서 `Browse Additional Color Themes...` 선택
- 확장 뷰에서 `@category:"themes"`로 검색

## 4. OS 색상 모드에 따라 자동 전환
- Windows/macOS의 밝기/다크 모드를 감지하여 테마를 자동으로 바꿀 수 있습니다.
- 설정 항목:
  - `window.autoDetectColorScheme`
  - `window.autoDetectHighContrast`

### 4.1. 선호 테마 설정
- Workbench: Preferred Dark Color Theme
- Workbench: Preferred Light Color Theme
- Workbench: Preferred High Contrast Color Theme
- Workbench: Preferred High Contrast Light Color Theme

## 5. 색 테마 맞춤 설정
### 5.1. Workbench 색상 사용자 지정
- `workbench.colorCustomizations`를 사용하여 활성 테마의 UI 색상을 변경
- 예시:
```json
"workbench.colorCustomizations": {
    "[Monokai]": {
        "sideBar.background": "#347890"
    }
}
```
- 여러 테마를 지정하거나 와일드카드를 사용할 수 있습니다:
```json
"workbench.colorCustomizations": {
    "[Abyss][Red]": {
        "activityBar.background": "#ff0000"
    },
    "[Monokai*]": {
        "activityBar.background": "#ff0000"
    }
}
```
- 기본값으로 되돌리려면 `default`를 사용:
```json
"workbench.colorCustomizations": {
    "diffEditor.removedTextBorder": "default"
}
```

### 5.2. 편집기 문법 하이라이팅
- `editor.tokenColorCustomizations`로 구문 색상을 조정
- 일반 토큰 이름 사용 또는 TextMate 규칙 직접 지정
- 예시:
```json
"editor.tokenColorCustomizations": {
    "[Monokai]": {
        "comments": "#229977"
    },
    "[*Dark*]": {
        "variables": "#229977"
    },
    "[Abyss][Red]": {
        "keywords": "#f00"
    }
}
```
- TextMate 규칙을 직접 구성하는 것은 고급 설정입니다.

### 5.3. 의미론적 하이라이팅(Semantic Highlighting)
- 일부 언어(TypeScript, JavaScript, Java 등)는 의미론적 토큰을 지원
- `editor.semanticHighlighting.enabled` 값:
  - `true` : 항상 켬
  - `false` : 항상 끔
  - `configuredByTheme` : 테마 설정에 따름 (기본값)

- 테마별 설정을 오버라이드하려면:
```json
"editor.semanticTokenColorCustomizations": {
    "[Rouge]": {
        "enabled": true
n    }
}
```
- 추가 규칙 예시:
```json
"editor.semanticTokenColorCustomizations": {
    "[Rouge]": {
        "enabled": true,
        "rules": {
            "*.declaration": { "bold": true }
        }
    }
}
```
- 현재 커서 위치의 토큰 정보를 보려면 `Developer: Inspect Editor Tokens and Scopes` 사용

## 6. 나만의 색 테마 만들기
- 현재 설정에서 테마 정의 파일을 생성하려면 `Developer: Generate Color Theme From Current Settings` 실행
- 확장 생성 도구로 테마 확장 만들기 가능
- 참고 문서:
  - `Create a new Color Theme`
  - [Color Theme extension guide](https://code.visualstudio.com/api/extension-guides/color-theme)

## 7. 기본 색 테마 제거
- 기본 테마는 확장 뷰에서 `Built-in` 필터를 선택하여 확인
- 기본 테마 확장을 비활성화하면 색 테마 선택기에서 제거됨

## 8. 파일 아이콘 테마(File Icon Themes)
### 8.1. 변경 방법
1. `파일 > 기본 설정 > 테마 > 파일 아이콘 테마`
2. `Preferences: File Icon Theme` 명령 실행
3. 원하는 아이콘 테마 선택 후 Enter

### 8.2. 기본 제공 아이콘 테마
- 기본적으로 `Seti` 파일 아이콘 테마 사용
- VS Code는 `Minimal`과 `Seti` 두 가지를 기본 제공
- `None`을 선택하면 파일 아이콘을 사용하지 않음

### 8.3. 추가 아이콘 테마 설치
- 파일 아이콘 테마 선택기에서 `Install Additional File Icon Themes` 선택
- 마켓플레이스에서 아이콘 테마 검색
- 설정 예시:
```json
"workbench.iconTheme": "vs-seti"
```

## 9. 제품 아이콘 테마(Product Icon Themes)
- UI 전체의 아이콘(액티비티 바 등)을 변경할 수 있는 테마
- `파일 > 기본 설정 > 테마 > 제품 아이콘 테마`
- `Preferences: Product Icon Theme` 명령 실행
- 기본적으로 `Default` 하나가 제공되며, 추가 테마는 마켓플레이스에서 설치 가능

## 10. VS Code for the Web
- 웹 버전에서도 테마 미리보기 및 공유 가능
- URL 스키마:
  - `https://vscode.dev/editor/theme/<extensionId>`
- 예: `https://vscode.dev/editor/theme/sdras.night-owl`

## 11. 참고 자료
- [Settings](https://code.visualstudio.com/docs/configure/settings)
- [Snippets](https://code.visualstudio.com/docs/editing/userdefinedsnippets)
- [Extension API](https://code.visualstudio.com/api)
- [Color Theme guide](https://code.visualstudio.com/api/extension-guides/color-theme)
- [File Icon Theme guide](https://code.visualstudio.com/api/extension-guides/file-icon-theme)
