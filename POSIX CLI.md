# POSIX CLI

> [!TIP]
> 맨 끝에 물결 표시(~)는 현재 홈 디렉터리에 있다는 의미


## pwd (Print Working Directory) - 현재 디렉터리 경로 확인
```bash
pwd
```


## ls (List) - 디렉터리 목록 확인
```bash
ls
```

```bash
ls -la
```

```bash
ls -a           # 숨김 파일 포함 목록
ls -l           # 상세 목록
ls -r           # 역순 목록
ls -t           # 수정 시간 순 목록
```

> [!TIP]
> 숨김파일 (`.`으로 시작하는 파일)

```bash
ls -la          # 상세 + 숨김 파일 포함 목록
ls -al          # 상세 + 숨김 파일 포함 목록
```

> [!TIP]
> 옵션은 순서와 상관없이 조합해서 사용할 수 있습니다.  


## cd (Change Directory) - 디렉터리 이동
```bash
cd dir_name     # dir_name → 이동 할 하위 디렉터리 이름
cd ..           # 상위 디렉터리로 이동
cd ~            # 홈 디렉터리로 이동
```

| 기호 | 설명 |
|---|---|
| ~ | 홈 디렉터리 |
| . | 현재 디렉터리 |
| .. | 상위 디렉터리 |


## mkdir (Make Directory) - 디렉터리 생성
```bash
mkdir dir_name  # dir_name → 생성할 디렉터리 이름
```
## rm (Remove) - 파일 및 디렉터리 삭제
```bash
rm name         # name → 삭제할 파일 또는 디렉터리 이름
rm -r name      # name → 삭제할 디렉터리 이름 (디렉터리 내의 모든 내용 삭제)
```

rm filename        # 파일 삭제
rm -r dirname      # 디렉터리와 그 안의 내용까지 삭제


## vim - 텍스트 편집기
```bash
vim file_name  # file_name이 존대하면 해당 파일을 열어 편집, 없으면 새 파일 생성
```

`A` 또는 `I` - 편집 모드로 전환  
`Esc` - ex 모드로 전환  

* ex 모드  
`w` - 저장   
`q` - 종료  
`:wq` - 저장 후 종료  
`:q!` - 저장하지 않고 종료  



p.36    git config --global core.editor ""
p.36    cat ?    // ? → 파일
    2장  깃으로 버전 관리하기
p.40    git init
p.43    작업트리(working tree)
        스테이지(stage)
        저장소(repository)
p.45    git status
p.47    git add    // ? → 파일
p.49    git commit -m ""
        git commit -am ""
p.50    git log
        git log --stat
p.55    git diff
p.65    git commit --amend
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