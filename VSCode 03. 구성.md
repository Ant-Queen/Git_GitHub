# VSCode - 구성 (CONFIGURE)
> [from the Visual Studio Code documentation](https://code.visualstudio.com/docs/configure/locales)

## 표시 언어 (Display Language)

<br>

### 표시 언어 변경 (Changing the Display Language)

명령팔레트 - "Configure Display Language" - "ko" 선택 - 재시작

> [!NOTE]  
> `.vscode` 폴더의 `argv.json` 파일에 기록 됩니다.

<br>

### 사용 가능한 지역 (Available locales)

<br>

### 마켓플레이스 언어 팩 (Marketplace Language Packs)

확장 - 마켓플레이스 - "Korean Language Pack for Visual Studio Code", Microsoft

<br>

### (X) 언어 설정 (Setting the Language)

VS Code 세션에서 특정 언어를 사용 (1회성)

```bash
code . --locale=kr
code . --locale=en
```
> [!NOTE]  
> 외부 터미널에서 사용할 수 있습니다.  
> (VS Code 내부 터미널에서는 작동하지 않습니다.)