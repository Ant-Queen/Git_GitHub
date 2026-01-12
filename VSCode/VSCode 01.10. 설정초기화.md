# VSCode - 설정 (SETUP) - 제거 (Uninstall Visual Studio Code)
> [from the Visual Studio Code documentation](https://code.visualstudio.com/docs/setup/uninstall)

## 깔끔한 제거

# 🧹 VS Code Clean Uninstall / 설정 초기화

## 📌 개요
- **Clean Uninstall**: VS Code 제거 후 사용자 데이터까지 삭제 → 완전 초기화  
- **설정 초기화**: VS Code는 그대로 두고 사용자 데이터 폴더만 삭제 → 설정/확장 초기화  

---

## 📂 삭제해야 할 폴더 위치

### 🔹 Windows
- `%APPDATA%\Code`  
- `%USERPROFILE%\.vscode`  

#### PowerShell 명령어
```powershell
rd /s /q "%APPDATA%\Code"
rd /s /q "%USERPROFILE%\.vscode"
```



# VS Code 설정 초기화 (Clean Uninstall)

VS Code를 완전히 제거하지 않고도 **설정 초기화**만 할 수 있습니다.  
사용자 데이터 폴더를 삭제하면 확장, 테마, 사용자 설정 등이 모두 기본 상태로 돌아갑니다.

---

## 🧹 초기화 방법

### 📌 Windows
1. VS Code 종료
2. 아래 두 폴더 삭제
   - `%APPDATA%\Code`
   - `%USERPROFILE%\.vscode`

#### PowerShell 명령어
```powershell
rd /s /q "%APPDATA%\Code"
rd /s /q "%USERPROFILE%\.vscode"
```