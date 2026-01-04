# Git CLI (Git Command Line Interface)
> CRUD (Create, Read, Update, Delete) 흐름으로 정리

## Git 개념

분산 버전 관리 시스템(DVCS)  
핵심 기능 - 버전관리, 백업, 협업

### git - 명령어 확인
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

### 저장소 초기화
```bash
git init
```

### 현재 상태 확인
```bash
git status
```

| 줄 | 의미 |
|-----|------|
| `On branch main` | 현재 작업 중인 브랜치는 `main`입니다. (기본 브랜치) |
| `No commits yet` | 아직 커밋된 내용이 없습니다. 즉, 저장소에 기록된 변경 사항이 없음 |
| `Nothing to commit` | 스테이지에 올라간 파일이 없고, 작업트리에도 변경된 파일이 없음 |
| `Untracked files` | Git이 추적하지 않는 파일들이 존재함. 즉, 새로 생성된 파일이나 디렉터리가 있음 |
| `Changes to be committed` | 스테이지에 올라간 파일들이 존재함. 즉, 커밋할 준비가 된 변경 사항이 있음 |
| `Changes not staged for commit` | 작업트리에서 변경된 파일들이 있지만, 스테이지에는 올라가지 않은 상태임 |
| `nothing to commit, working tree clean` | 작업트리에 변경된 파일이 없고, 스테이지에도 커밋할 파일이 없음. 즉, 현재 상태가 깔끔함 |
| `modified: filename` | `filename` 파일이 수정되었음을 나타냄 |
| `new file: filename` | `filename` 파일이 새로 생성되었음을 나타냄 |
| `deleted: filename` | `filename` 파일이 삭제되었음을 나타냄 |


### 파일 스테이지에 추가
```bash
git add name    # name → 파일 이름
git add .       # 현재 디렉터리의 모든 변경 사항을 스테이지에 추가
```

### 커밋 생성
```bash
git commit -m "commit message"      # "commit message" → 커밋 메시지
git commit -am "commit message"     # 한 번이라도 커밋한 적이 있는 수정된 파일을 스테이지에 올리고 커밋 생성
```

### 커밋 기록 확인
```bash
git log
git log --stat          # 각 커밋에 대한 변경된 파일과 라인 수 요약 정보 포함
git log -p              # 각 커밋에 대한 상세한 변경 내용(패치) 포함
git log --oneline       # 각 커밋을 한 줄로 요약하여 표시
git log --oneline --branches            # 모든 브랜치의 커밋을 한 줄로 요약하여 표시
git log --oneline --branches --graph    # 브랜치 구조를 그래프로 시각화하여 표시
git log branch_name..other_branch_name  # branch_name 브랜치에만 있는 커밋 확인, 브랜치 비교
git reflog              # 모든 참조 변경 이력 확인
```

### 변경 사항 비교
```bash
git diff
```

| 구분 | 의미 | 커밋 포함 여부 |
|---|---|----|
| **Tracked Files** | Git이 추적하는 파일들. 이미 커밋에 포함되었거나 `git add`로 스테이징된 파일 | 포함 가능 |
| **Untracked Files** | Git이 추적하지 않는 파일들. 새로 생성했지만 아직 `git add`하지 않은 파일 | 포함되지 않음 |

> [!NOTE]  
> `.gitignore` 파일을 사용하여 Git이 추적하지 않도록 설정할 수 있습니다.

### 최근 커밋 메세지 수정
```bash
git commit --amend
```

### 작업트리에서 수정한 파일 되돌리기
```bash
git checkout -- file_name       # file_name → 파일
git restore file_name           # file_name → 파일 // Git 2.23 이후 권장
```
> [!CAUTION]  
> 되돌린 내용은 다시 복구할 수 없습니다.

### 스테이징된 파일 되돌리기
```bash
git reset HEAD file_name        # file_name → 파일 // 지정한 파일을 스테이징에서 제거, 작업트리의 수정 내용은 유지
git restore --staged file_name  # file_name → 파일 // Git 2.23 이후 권장
```

### 최신 커밋 되돌리기
```bash
git reset HEAD^         # 최신 커밋을 취소하고, 변경 사항을 스테이징에서 제거, 작업트리의 수정 내용은 유지
```

| 명령어 | 되돌리는 대상 | 스테이징 영역(Index) | 작업트리(Working Directory) | 특징 |
|---|---|---|---|---|
| `git reset --soft HEAD^` | 커밋만 되돌림 | 유지됨 | 유지됨 | 커밋만 취소, 수정 내용과 스테이징은 그대로 |
| `git reset --mixed HEAD^` (기본값) | 커밋 + 스테이징 되돌림 | 스테이징 해제 | 유지됨 | 커밋과 스테이징 취소, 수정 내용은 남음 |
| `git reset --hard HEAD^` | 커밋 + 스테이징 + 작업트리 되돌림 | 되돌림 | 되돌림 | 모든 변경 사항 삭제, 완전히 이전 커밋 상태로 돌아감, 복구 불가 |


### 특정 커밋으로 되돌리기
```bash
git reset --hard commit_hash    # commit_hash → 복사한 커밋 해시
```

> [!NOTE]  
> C1 → C2 → C3 순서로 커밋이 쌓였을 때, `git reset --hard C2` 명령어를 실행하면 C3 커밋이 삭제되고, 작업트리와 스테이징이 C2 커밋 상태로 돌아갑니다.

### 커밋 삭제하지 않고 되돌리기
```bash
git revert commit_hash          # commit_hash → 복사한 커밋 해시
```
> [!NOTE]  
> C1 → C2 → C3 순서로 커밋이 쌓였을 때, `git revert C3` 명령어를 실행하면 C3 커밋의 변경 사항을 되돌리는(C2 커밋 상태) 새로운 커밋 C4가 생성됩니다. 기존 커밋들은 그대로 유지됩니다.  
> 즉, `git reset --hard`와 달리 커밋 기록이 보존됩니다.  


> [!IMPORTANT]  
> revert는 순차적으로 커밋을 되돌려야 합니다. 예를 들어, C1 커밋까지 되돌리려면 `git revert C3`를 먼저 실행한 후, `git revert C2`를 실행해야 합니다.  
> 그렇지 않으면 충돌이 발생할 수 있습니다.  
> C1 → C2 → C3 순서로 커밋이 쌓였을 때, C2만 단독으로 되돌리려고 하면 C3의 변경 사항과 충돌이 발생할 수 있습니다.

<br>
<br>
<br>

## 브랜치 (Branch)

### 브랜치 목록 확인
```bash
git branch              # 브랜치 목록 확인
```

### 브랜치 생성
```bash
git branch branch_name  # branch_name → 생성할 브랜치 이름
```

### 브랜치 전환
```bash
git checkout branch_name        # branch_name → 브랜치 이름
git checkout -b branch_name     # branch_name → 생성할 브랜치 이름 // 생성과 전환을 동시에
git checkout -                  # 이전에 있던 브랜치로 전환
git switch branch_name          # branch_name → 브랜치 이름 // Git 2.23 이후 권장
git switch -c branch_name       # branch_name → 생성할 브랜치 이름 // 생성과 전환을 동시에, Git 2.23 이후 권장
git switch -                    # 이전에 있던 브랜치로 전환, Git 2.23 이후 권장
```

### 브랜치 병합
```bash
git merge branch_name            # branch_name → 병합할 브랜치 이름
git merge branch_name --no-edit  # 자동 생성되는 병합 커밋 메시지 편집하지 않음
git merge branch_name --edit     # 자동 생성되는 병합 커밋 메시지 편집
```

### 브랜치 삭제
```bash
git branch -d branch_name     # branch_name → 삭제할 브랜치 이름
git branch -D branch_name     # branch_name → 강제 삭제할 브랜치 이름
```
> [!NOTE]  
> 브랜치를 삭제할 때, 해당 브랜치가 현재 체크아웃된 상태이거나 병합되지 않은 커밋이 있을 경우 오류가 발생합니다.  
> `-D` 옵션을 사용하면 강제로 브랜치를 삭제할 수 있습니다.  
> 그러나 이 경우 병합되지 않은 커밋이 손실될 수 있으므로 주의해야 합니다.  
> -d 옵션은 안전하게 삭제할 때 사용하고, -D 옵션은 정말 필요할 때만 사용하세요.  
> -d 옵션으로 삭제한 경우 해당 브랜치가 완전 삭제되는것이 아니라, 브랜치명만 감춰지는 것이므로 git reflog 명령어로 복구할 수 있습니다.

### 병합 방식 비교
| 구분 | 2-way Merge (양방향 병합) | 3-way Merge (삼방향 병합) - 효율적 |
|---|---|---|
| 비교 대상 | 두 버전만 비교 (현재 브랜치 vs 병합할 브랜치) | 세 버전 비교 (공통 조상 + 현재 브랜치 + 병합할 브랜치) |
| 장점 | 단순함, 빠른 병합 | 충돌 해결 정확도 높음, 자동 병합 성공률 높음 |
| 단점 | 공통 조상 정보가 없어 충돌 발생 시 해결이 어렵고 오류 가능성 ↑ | 상대적으로 복잡하지만 안정적 |
| 사용 예시 | 단순한 변경, 공통 조상 불필요한 경우 | 대부분의 Git 병합 상황에서 기본적으로 사용 |
| 결과 | 충돌 발생 시 수동 해결 필요성이 큼 | 충돌 발생 시 Git이 더 많은 정보를 제공해 해결 용이 |

### 작업 내용 임시 저장 (Stash)
```bash
git stash                     # 현재 작업 내용을 임시로 저장하고 작업트리를 깨끗한 상태로 만듦
git stash pop                 # 가장 최근에 저장한 작업 내용을 복원하고 스택에서 제거
git stash apply               # 가장 최근에 저장한 작업 내용을 복원하지만 스택에는 남겨둠
git stash list                # 저장된 작업 내용 목록을 확인
git stash drop stash@{0}      # 특정 저장된 작업 내용을 스택에서 제거
git stash clear               # 모든 저장된 작업 내용을 스택에서 제거
```

### 특정 커밋을 현재 브랜치에 적용 (Cherry-pick)
```bash
git cherry-pick commit_hash      # commit_hash → 복사한 커밋 해시
```
> [!WARNING]  
> Cherry-pick은 커밋 히스토리를 변경하므로, 이미 원격 저장소에 푸시된 커밋에 대해 cherry-pick을 수행하는 것은 피해야 합니다.  
> 협업 중인 브랜치에서 cherry-pick을 사용하면 다른 사람들의 작업에 영향을 줄 수 있습니다.  
> Cherry-pick을 사용할 때는 항상 신중하게 고려하고, 가능하면 개인 작업 브랜치에서만 사용하는 것이 좋습니다.

### 브랜치 재배치 (Rebase)
```bash
git rebase branch_name        # branch_name → 기준이 될 브랜치 이름
```
> [!WARNING]  
> Rebase는 커밋 히스토리를 변경하므로, 이미 원격 저장소에 푸시된 커밋에 대해 rebase를 수행하는 것은 피해야 합니다.  
> 협업 중인 브랜치에서 rebase를 사용하면 다른 사람들의 작업에 영향을 줄 수 있습니다.  
> Rebase를 사용할 때는 항상 신중하게 고려하고, 가능하면 개인 작업 브랜치에서만 사용하는 것이 좋습니다.

<br>
<br>
<br>

## 백업 및 원격 저장소

### 원격 저장소 추가
```bash
git remote add origin remote_repository_URL    # remote_repository_URL → 원격 저장소 URL
```

### 원격 저장소 목록 확인
```bash
git remote -v               # 원격 저장소 목록 확인
```

### 원격 저장소로 최초 푸시
```bash
git push -u origin main     # branch_name → 로컬 브랜치 이름 // 원격 저장소에 브랜치 최초 푸시, -u 옵션은 지역 저장소의 브랜치를 원격 저장소의 브랜치와 연결, 처음에 한 번만 사용하면 됨
```

### 원격 저장소로 현재 브랜치 푸시
```bash
git push                    # 원격 저장소에 현재 브랜치 푸시
```

### 원격 저장소에서 변경 사항 가져오기
```bash
git pull                    # 원격 저장소에서 현재 브랜치의 변경 사항을 가져와 병합
```

<br>
<br>
<br>

## 깃허브에 SSH 원격 접속하기

### SSH 키 생성
```bash
ssh-keygen
```
> [!NOTE]  
> 생성된 SSH 키는 기본적으로 `~/.ssh/id_rsa` (개인 키)와 `~/.ssh/id_rsa.pub` (공개 키) 파일에 저장됩니다.

