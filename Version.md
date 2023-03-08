<h1 align="center"> Version </h1>

<details><summary><h4>Summary</h4></summary>
    
![My First Board](https://user-images.githubusercontent.com/116495744/212557289-8b230e0d-f8ee-4479-bd60-e4f3cec83448.jpg)

</details>    

---

## Concept

- **Version Control Tools**

  - **Commit** : 데이터 변경 확정 내역 혹은 최종본
  - **Tag** : 데이터 변경 확정 내역에 다는 꼬리표로서, 통상적으로는 변경 확정 내역 중 최종본에 사용됨
  - **Branch** : 데이터 변경 확정 내역의 흐름

- **Area**

  - **Working Tree** : 분산형 버전 관리 프로그램 `Git` 의 관리를 받는 공간
  - **Stage** : Branch 에 변경 사항을 확정하여 하나의 버전으로 기록하기 위한 파일들을 모아두는 가상 공간
  - **Branch** : 확정된 변경 사항을 기록한 공간

- **File Status**

  - **Untracked** : 한번도 커밋되지 않아 `git` 이 수정 여부를 추적할 수 없는 상태
  
  - **Tracked**
    - `Unmodified` : 마지막 커밋 후 변경 사항이 없는 상태
    - `Modified` : 마지막 커밋 후 변경 사항이 존재하는 상태
    - `Staged` : 변경 사항을 확정하여 기록하기 위해 대기하는 상태
    - `Committed` : 변경 사항이 확정되어 브랜치에 기록된 상태

- **Commit Process**

  - `add`
    - 변경 사항이 존재하는 파일들을 스테이지에 올려줌
    - 즉, 파일의 상태를 `Modified` 에서  `Staged` 상태로 전환함

  - `commit`
    - **스테이지에 위치하는 파일들의 변경 사항을 확정하여 브랜치에 기록함**
      - 커밋 시 스테이지에 위치했던 파일들의 변경 사항은 하나의 버전으로서 기록됨

    - **즉, 파일의 상태를 `Staged` 에서 `Unmodified` 상태로 전환함**
      - 마지막 커밋이 발생하였음
      - 우선 파일의 상태가 `Staged` 에서 `Committed` 상태로 전환됨
      - 모든 파일은 마지막 커밋 후 변경 사항이 존재하지 않게 됨
      - 최종으로는 파일의 상태가 `Committed` 에서 `Unmodified` 상태로 전환됨

    - **단, 원격 브랜치에 반영하기 위해서는 UPLOAD 작업을 추가로 수행해야 함**
---

## Search

<details><summary><h4>Git Status 조회하기</h4></summary>

~~~
git status
~~~

- `status` : 현재 위치한 브랜치의 커밋에서 깃이 관리하는 파일들의 상태를 조회함
  
  - Branch Name
  - Untracked Files
  - Modified Files
  - Staged Files
  - Committed Files

</details>

<details><summary><h4>Commit History 조회하기</h4></summary>

~~~
git log <option>
~~~

- **`log` : 현재 위치한 브랜치의 커밋 내역을 조회함**
    
- `option`
    - `none` : 현재 위치한 브랜치의 커밋 히스토리 조회
    - `--stat` : 파일별 변경 사항 히스토리 조회
    - `--oneline` : 커밋 주소와 설명 목록 조회  
  
</details>

<details><summary><h4>Commit 상세조회하기</h4></summary>

~~~
git show <Commit Hash>
~~~

- **`show <Commit Hash>` : 특정 커밋의 정보를 상세조회함**
    
    - `<Commit Hash>` 의 기본값은 `HEAD` 임

</details>

<details><summary><h4>Commit 변경 사항 조회하기</h4></summary>

- **특정 파일의 변경 사항 조회하기**

    ~~~
    git diff <option> <File Name>
    ~~~

    - **`diff <File Name>` : 특정 파일에 대하여 워킹트리, 스테이지, 브랜치 `HEAD` 간 변경 사항을 조회함**
        - 파일을 특정하지 않을 경우 모든 파일의 변경 사항을 조회함
    
    - `option`
        - `none` : 특정 파일의 working directory 와 stage area 간 변경 사항 조회
        - `HEAD` : 특정 파일의 working directory 와 최신 커밋 `HEAD` 간 변경 사항 조회
        - `--staged` : 특정 파일의 stage area 와 최신 커밋 `HEAD` 간 변경 사항 조회

---
    
- **특정 브랜치 간 변경 사항 조회하기**    

    ~~~
    git diff <branch1>..<branch2>
    ~~~

    - **`diff <branch1>..<branch2>`**
    
        - 임의의 커밋 `commit` 에서 분기한 브랜치 `branch1` , `branch2` 에 대하여,
        - 두 브랜치 간 변경 사항을 조회함

---
    
- **특정 커밋 간 변경 사항 조회하기**
    
    ~~~
    git diff <commit1>..<commit2>
    ~~~

    - **`diff <commit1>..<commit2>`**
    
        - 임의의 브랜치 `branch` 의 변경 확정 내역 `commit1` , `commit2` 에 대하여,
        - 두 커밋 간 변경 사항을 조회함

</details>
    
---
    
## Commit

<details><summary><h4>Commit 생성하기</h4></summary>

~~~
// 수정된 파일들을 스테이지에 올리기
git add <Modified File Name>
    
// 스테이지에 올라온 변경 사항들을 확정하여 현재 위치한 로컬 브랜치에 기록하기
git commit -m "Description"
    
// 현재 위치한 로컬 브랜치에 연동되어 있는 원격 저장소의 브랜치에 반영하기
git push <Remote Repository Name> <Remote Branch Name>
~~~

- **`add <Modified File Name>` : 워킹트리에서 수정된 파일을 스테이지에 올려줌**
    - 해당 파일의 상태를 수정 상태(Modified)에서 스테이지 상태(Staged)로 전환함
    - 수정 상태인 파일들을 모두 선택하는 경우 `<Modified File Name>` 에 전체 선택자 `*` 을 기입함

- **`commit` : 스테이지에 올라온 변경 사항들을 확정하여 현재 위치한 로컬 브랜치에 기록함**
    - 우선 스테이지 상태에 있는 모든 파일들을 커밋 상태(Committed)로 전환함
    - 이후 자동으로 해당 파일들을 수정되지 않은 상태(Unmodified)로 전환함

- **`push <Remote Repository Name> <Remote Branch Name>` : 로컬 브랜치에 기록된 변경 확정 내역을 원격 브랜치에 반영함**
    - `<Remote Repository Name>` 의 기본값은 현재 위치한 로컬 브랜치에 연동되어 있는 원격 저장소임
    - `<Remote Branch Name>` 의 기본값은 현재 위치한 로컬 브랜치에 연동되어 있는 원격 브랜치임
    
</details>
    
<details><summary><h4>Commit 개정하기</h4></summary>
    
~~~
// 마지막 커밋 이후 수정된 파일들을 스테이지에 올리기
git add <New Modified File Name>
    
// 해당 변경 사항들을 마지막 커밋에 확정하여 기록하기
git commit --amend -m "Renewal Description"
    
// 개정한 커밋을 원격 저장소의 브랜치에 반영하기
git push <Remote Repository Name> <Remote Branch Name>
~~~
    
- **`commit --amend` : 현재 스테이지에 올라온 변경 사항을 마지막 커밋에 추가함**

- **주의**
    - 기존 커밋을 개정하는 작업이 아님
    - **기존 커밋의 내용을 개정한 새로운 커밋을 생성하는 작업임**
    - 개정 확정 시, 로컬 브랜치에 존재하는 기존 커밋은 자동으로 삭제됨
    - 원격에 반영한 커밋을 개정하는 경우, 원격에 재반영하는 과정에서 충돌이 발생할 수 있음

</details>
    
<details><summary><h4>Commit 붙여넣기</h4></summary>
    
- **Commit 붙여넣기**
    
    ~~~
    // 커밋을 붙여넣고 싶은 브랜치로 이동
    git switch <Local Branch Name>

    // 현재 위치한 브랜치에 커밋 붙여넣기
    git cherry-pick <Commit Hash>
    ~~~

    - **`cherry-pick <Commit Hash>` : 현재 위치한 브랜치에 특정 커밋을 기록함**
    
---
    
- **Commit 을 붙여넣는 과정에서 충돌이 발생할 경우**
    
    ~~~
    // 충돌 사항 수정 후 해당 파일들을 스테이지에 올려주기
    git add <conflict files>

    // 커밋 붙여넣기 재개
    git cherry-pick --continue

    // 커밋 붙여넣기 중단하고 기존 커밋으로 복원
    git cherry-pick --abort
    ~~~
    
    - **`cherry-pick <option>` : 일시중지 상태인 커밋 붙여넣기 작업에 대하여 기능함**
    
        - `--continue` : 커밋 붙여넣기 작업을 재개함
        - `--abort` : 커밋 붙여넣기 작업을 중단함
    
</details>
    
<details><summary><h4>Commit 복원하기</h4></summary>
   
~~~
git restore <option> <File Name>
~~~
    
- **`restore <File Name>` : 수정 상태에 있는 파일을 수정 이전 상태로 복원함**
    
- `option`
    - `none` : 특정 파일을 `HEAD` 에 기록되어 있는 상태로 복원함
    - `--staged` : 스테이지 상태에 있는 특정 파일을 스테이지 상태 이전으로 복원함
    - `--source <commit hash>` : 특정 파일을 특정 커밋에 기록되어 있는 상태로 복원함

</details>
    
<details><summary><h4>Commit 취소하기</h4></summary>
    
~~~
git revert <Commit Hash>
~~~
    
- **`revert <Commit Hash>` : 특정 커밋을 취소함**
    
- **주의**
    - 해당 커밋을 히스토리에서 삭제하지 않음
    - 다만 해당 커밋 이전의 커밋을 복원하여 해당 커밋 이후에 추가함

</details>
    
<details><summary><h4>Commit 되돌리기</h4></summary>
    
~~~
git reset <option> <Commit Hash>
~~~
    
- **`reset <Commit Hash>` : 특정 커밋 이후에 추가 기록된 커밋들을 모두 삭제하고 해당 커밋으로 되돌림**

- `option`
    - `--hard` : HEAD, 스테이지, 워킹트리의 상태를 모두 되돌림
    - `--mixed` : HEAD 의 상태는 되돌리되, 워킹트리와 스테이지의 상태는 유지함???
    - `--soft` : HEAD 의 상태는 되돌리되, 워킹트리와 스테이지의 상태는 유지함???
    
</details>
    
---
   
## Stash
    
<details><summary><h4>임시저장 목록 조회하기</h4></summary>

~~~
git stash list
~~~

- **`stash list` : 임시저장 목록을 조회함**
    
</details>
    
<details><summary><h4>변경 사항 임시저장하기</h4></summary>

~~~
git stash save
~~~

- **`stash save` : 현재 스테이지 상태인 파일들을 확정하지 않고 임시저장함**
    
</details>
    
<details><summary><h4>임시저장 항목 불러와서 적용하기</h4></summary>

~~~
git stash apply <Stash Name> <option>
~~~
  
- **`stash apply <Stash Name>` : 특정 임시저장 항목을 현재 위치한 커밋에 불러와서 적용함**
    - 임시저장한 브랜치나 커밋이 아닌 위치에서 불러올 수 있음
    
- `option`
    - `none` : 특정 임시저장 항목을 불러와서 현재 위치한 커밋과 병합 후 스테이지 상태로 전환함
    - `--index` : 스테이지 상태로 전환하기 전 충돌 사항을 조회함

</details>
  
<details><summary><h4>임시저장 항목 삭제하기</h4></summary>

- **특정 항목 삭제하기**
    
  ~~~
  git stash drop <Stash Name>
  ~~~
  
  - **`stash drop <Stash Name>` : 특정 항목을 임시저장 목록에서 삭제함**
    
---
    
- **전체 항목 삭제하기**
    
    ~~~
    git stash clear
    ~~~
    
    - **`stash clear` : 임시저장 목록을 초기화함**
  
</details>
    
---
    
## Tag
    
<details><summary><h4>Tag 조회하기</h4></summary>
    
- **로컬 저장소 태그 목록 조회하기**
    
    ~~~
    git tag
    ~~~
    
    - `tag` : 로컬 저장소의 전체 태그 목록을 조회함
    
---
    
- **로컬 저장소 태그 조건부 조회하기**
    
    ~~~
    git tag --list <condition.*>
    ~~~
    
    - `tag --list <condition.*>` : 로컬 저장소의 태그 중 키워드 `condition` 을 포함하는 태그만 조회함
    
---
    
- **로컬 저장소 특정 태그 상세조회하기**
  
    ~~~
    git show <Tag Name>
    ~~~
    
    - `show <Tag Name>` : 특정 태그의 정보를 상세조회함
    
        - Tag Annotation
        - Tagger
        - Date
        - Commit
    
</details>
    
<details><summary><h4>Tag 생성하기</h4></summary>
    
~~~
// 태그 생성
git tag <option> <Tag Name> <Commit Hash>
    
// 태그 생성 내역을 원격 저장소에 반영
// 1. 특정 태그만 반영함
git push <Remote Repository Name> <Tag Name>
    
// 2. 특정 브랜치의 태그들만 반영함
git push <Remote Repository Name> <Branch Name> --tags
    
// 3. 특정 원격 저장소의 태그들을 반영함
git push <Remote Repository Name> --tags
~~~

- **`tag <Tag Name>` : 특정 커밋에 태그를 생성함**

- `option`
    - `none` : LightWeight Tag 를 생성함
    - `-a` : Annotated Tag 를 생성함
    
</details>

<details><summary><h4>Tag 삭제하기</h4></summary>

- **로컬 저장소 태그 삭제하기**
  
    ~~~
    git tag -d <Tag Name>
    ~~~
    
    - **`tag -d <Tag Name>` : 로컬 저장소의 특정 태그를 삭제함**
    
    - 로컬 저장소의 모든 태그를 삭제할 경우 `<Tag Name>` 에 `$(git tag -l)` 를 기입함
    
---
    
- **원격 저장소 태그 삭제하기**
    
    ~~~
    git push <Remote Repository Name> --delete <Tag Name>
    ~~~
    
    - **`push <Remote Repository Name> --delete <Tag Name>` : 원격 저장소의 특정 태그를 삭제함**
    
    - 원격 저장소의 모든 태그를 삭제할 경우 `<Tag Name>` 에 `$(git tag -l)` 를 기입함

</details>
    
---
    
## Move
    
<details><summary><h4>DETACHED HEAD</h4></summary>

- **DETACHED HEAD**
    - 커밋이 브랜치에서 벗어나 단독으로 존재하는 상태
    - 모든 커밋은 브랜치를 벗어나 단독으로 존재할 수 없음
    - 커밋을 가리킬 때는 브랜치를 참조해야 하기 때문임

- **`HEAD` : 현재 위치한 커밋을 가리키는 변수**
    - `HEAD` 는 현재 위치한 브랜치를 가리킴
    - 현재 위치한 브랜치는 마지막 커밋을 가리킴
    - 즉, `HEAD` 는 커밋을 직접 가리키지 않음
    - `HEAD` 는 브랜치를 참조하여 우회적으로 커밋을 가리킴

- **커밋을 이동하는 작업은 커밋을 직접 가리키는 작업임**
    - 이동한 커밋에서 새로운 커밋을 생성하는 경우 해당 커밋을 가리킬 방법이 없음
    - 해당 커밋을 가리키기 위해 참조할 브랜치가 없기 때문임
    - 이러한 경우 새로운 커밋을 시작으로 하는 새로운 브랜치를 생성하여 해결함
    
</details>
    
<details><summary><h4>Commit Hash 를 참조하여 이동하기</h4></summary>
    
~~~
git checkout <Commit Hash>
~~~
    
- **`checkout <Commit Hash>` : 해당 커밋 주소로 이동함**

- `HEAD` 로부터 n 이전 시점으로 이동하는 경우 `<Commit Hash>` 에 `HEAD~n` 를 기입함
    
</details>
    
<details><summary><h4>Tag 를 참조하여 이동하기</h4></summary>
    
~~~
git checkout tags/<Tag Name>
~~~

- **`checkout tags/<Tag Name>` : 해당 태그가 가리키는 커밋 주소로 이동함**
    
</details>
