# Git CLI (Git Command Line Interface)
> CRUD (Create, Read, Update, Delete) 흐름으로 정리

## Git 개념

분산 버전 관리 시스템(DVCS)  
핵심 기능 - 버전관리, 백업, 협업

### git - Git 명령어 확인
```bash
git
```

### Git 사용자 정보 설정
```bash
git config --global user.name ""
git config --global user.email "@naver.com"
```

### Git 기본 편집기 설정
```bash
git config --global core.editor ""
```

<br>
<br>
<br>

## 버전관리

| 영역 | 설명 | 예시 명령어 |
|---|---|---|
| 작업트리 (Working Tree) | 실제 파일이 존재하는 디렉터리. 사용자가 직접 수정·추가·삭제하는 공간 | `git status` |
| 스테이지 (Stage) | 커밋할 준비가 된 파일을 모아두는 임시 공간. "커밋 후보" 영역 | `git add file.txt` |
| 저장소 (Repository) | 커밋된 파일들이 기록되는 데이터베이스. `.git` 디렉터리에 존재 | `git commit -m "메시지"` |

### Git 저장소 초기화
```bash
git init
```

### Git 현재 상태 확인
```bash
git status
```

| 줄 | 의미 |
|-----|------|
| `On branch master` | 현재 작업 중인 브랜치는 `master`입니다. (기본 브랜치) |
| `No commits yet` | 아직 커밋된 내용이 없습니다. 즉, 저장소에 기록된 변경 사항이 없음 |
| `Nothing to commit` | 스테이지에 올라간 파일이 없고, 작업트리에도 변경된 파일이 없음 |
| `Untracked files` | Git이 추적하지 않는 파일들이 존재함. 즉, 새로 생성된 파일이나 디렉터리가 있음 |
| `Changes to be committed` | 스테이지에 올라간 파일들이 존재함. 즉, 커밋할 준비가 된 변경 사항이 있음 |
| `Changes not staged for commit` | 작업트리에서 변경된 파일들이 있지만, 스테이지에는 올라가지 않은 상태임 |
| `nothing to commit, working tree clean` | 작업트리에 변경된 파일이 없고, 스테이지에도 커밋할 파일이 없음. 즉, 현재 상태가 깔끔함 |
| `modified: filename` | `filename` 파일이 수정되었음을 나타냄 |
| `new file: filename` | `filename` 파일이 새로 생성되었음을 나타냄 |
| `deleted: filename` | `filename` 파일이 삭제되었음을 나타냄 |


### Git 파일 스테이지에 추가
```bash
git add name    # name → 파일 이름
```

### Git 커밋 생성
```bash
git commit -m "commit message"      # "commit message" → 커밋 메시지
git commit -am "commit message"     # 한 번이라도 커밋한 적이 있는 수정된 파일을 스테이지에 올리고 커밋 생성
```

### Git 커밋 기록 확인
```bash
git log
git log --stat          # 각 커밋에 대한 변경된 파일과 라인 수 요약 정보 포함
git log -p              # 각 커밋에 대한 상세한 변경 내용(패치) 포함
git log --oneline       # 각 커밋을 한 줄로 요약하여 표시
```

### Git 변경 사항 비교
```bash
git diff
```

| 구분 | 의미 | 커밋 포함 여부 |
|---|---|----|
| **Tracked Files** | Git이 추적하는 파일들. 이미 커밋에 포함되었거나 `git add`로 스테이징된 파일 | 포함 가능 |
| **Untracked Files** | Git이 추적하지 않는 파일들. 새로 생성했지만 아직 `git add`하지 않은 파일 | 포함되지 않음 |

> [!NOTE]  
> `.gitignore` 파일을 사용하여 Git이 추적하지 않도록 설정할 수 있습니다.

### Git 최근 커밋 메세지 수정
```bash
git commit --amend
```




p.68    작업트리 취소
        git checkout -- ""    // "" → 파일
p.69    스테이징 되돌리기
        git reset HEAD ?    // ? → 파일
p.71    최신 커밋 되돌리기
        git reset HEAD^
p.77    특정 커밋으로 되돌리기
        git reset --hard ?    // ? → 복사한 커밋 해시
p.80    커밋 삭제하지 않고 되돌리기
        git revert ?    // ? → 복사한 커밋 해시
    3장  깃과 브랜치
p.91    git branch
p.92    git branch ?    // ? → 브랜치 이름
p.95    git log --oneline
        git checkout ?    // ? → 브랜치 이름
p.97    git add .
p.98    git log --oneline --branches
p.99    git log --oneline --branches --graph
p.100   git log ?..!    // ? → 브랜치 이름, ! → 브랜치 이름