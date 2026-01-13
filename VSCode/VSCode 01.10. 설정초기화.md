# VSCode - 설정 (SETUP) - 제거 (Uninstall Visual Studio Code)
> [from the Visual Studio Code documentation](https://code.visualstudio.com/docs/setup/uninstall)

## 깔끔한 제거 - 🧹 VS Code Clean Uninstall / 설정 초기화

### 📌 개요

- **Clean Uninstall**: VS Code 제거 후 사용자 데이터까지 삭제 → 완전 초기화  
- **설정 초기화**: VS Code는 그대로 두고 사용자 데이터 폴더만 삭제 → 설정/확장 초기화  

#### 📌 Windows

1. VS Code 종료 (Clean Uninstall 할 경우 삭제)
2. 아래 두 폴더 삭제
   - `%APPDATA%\Code`
   - `%USERPROFILE%\.vscode`

#### 명령 프롬프트(Command Prompt) 명령어

```cmd
rd /s /q "%APPDATA%\Code"
rd /s /q "%USERPROFILE%\.vscode"
```