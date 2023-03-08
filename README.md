<h1 align='center'>📚 GITHUB BASIC SYNTAX 📚</h1>

<details><summary><h4>refer</h4></summary>

- [**Git - 간편 안내서**](https://rogerdudler.github.io/git-guide/index.ko.html)

- [**누구나 쉽게 이해할 수 있는 Git 입문**](https://backlog.com/git-tutorial/kr/)

</details>

---

## Git & GitHub

- **Git 과 GitHub 의 차이점**

  - **Git** : 분산형 버전 관리 시스템(**D**istributed **V**ersion **C**ontrol **S**ystem; DVCS) 의 일종
  - **GitHub** : 분산형 버전 관리 시스템 Git 을 지원하는 원격 저장소 제공 서비스

- **데이터 분산 저장 방식**

  - **데이터 저장 방식**
    - **중앙 집중 방식** : 중앙 서버에 최종본 한 벌을 두고, 개별 네트워크가 서버에 접근하는 방식
    - **분산 저장 방식** : 서버와 네트워크가 확정본을 공동으로 저장하는 방식

  - **분산 저장 방식의 장점**
    - 참여자들이 병렬로 작업할 수 있으므로 작업 속도가 빠름
    - 서버 데이터가 훼손되더라도 네트워크에 다운로드한 데이터는 잔존하므로 데이터 보존에 유리함
    
  - **분산 저장 방식의 단점**
    - 참여자들이 병렬로 작업할 수 있으므로 각각의 네트워크에 저장된 데이터가 상이할 수 있음
    - 따라서 서버에서 개별 네트워크로 분기된 후 발생한 변경 내역들을 관리할 필요가 있음


- **버전 관리 시스템**
  - **정의** : 확정본과 확정본으로부터 분기되어 변경된 사항을 관리하는 시스템
  
  - **버전(확정본) 관리**
    - 특정 분기에 꼬리표를 달아 버전임을 명시함
    - 해당 분기로부터 흐름을 나누어 여러 버전을 개발할 수 있도록 지원함
  
  - **변경점 관리**
    - 확정본의 변경 내역을 확인할 수 있도록 지원함
    - 확정본을 특정 분기로 복구할 수 있도록 지원함

---

## Distributed Repository

<details><summary><h4>Concept</h4></summary>

- **Local 과 Remote**
  - **GitHub 에서는 원격 저장소를 중앙 서버로, 지역 저장소를 개별 네트워크로 사용함**
    - 원격 저장소 : GitHub 에서 제공하는 클라우드 저장소
    - 지역 저장소 : 개별 참여자의 컴퓨터 저장소
  
  - **Local Repository** : 지역 저장소
    - **Working Directory** : Local Repository 에서 Remote Repository 와 연동된 공간
    - **Stage** : Branch 에 변경 사항을 기록하기 위한 프로젝트 파일들을 모아두는 가상 공간
    - **Branch** : 확정된 변경 사항들을, 혹은 Version 들을 기록한 공간

  - **Remote Repository** : 원격 저장소
    - 자료 및 연산 자원을 저장하는 온라인 공간으로서, 클라우드(Cloud) 라고도 함
    - 구체적으로는 Working Directory 와 연동된 GitHub 의 Repository 를 가리킴

- **UpStream 과 DownStream**
  - **UpStream 과 DownStream 은 상대적 개념임**
    - 프로젝트의 중앙 서버에 가까울수록 `UpStream` 이라고 함
    - 프로젝트의 분산 네트워크에 가까울수록 `DownStream` 이라고 함
    
  - **지역 저장소와 원격 저장소의 구분**
    - 통상적으로는 원격 저장소가 중앙 서버로서 기능함
    - 통상적으로는 지역 저장소가 분산 네이트워크로서 기능함
    - 따라서 원격 저장소를 `UpStream` , 지역 저장소를 `DownStream` 이라고 함
    - 혹은 원격 저장소를 `origin` 이라고 이름하기도 함
    
  - **원격 저장소끼리의 구분**
    - 중앙 서버로서 기능하지는 않으나, 중앙 서버와 지역 저장소를 매개하는 원격 저장소가 존재할 수 있음
    - 해당 저장소는 중앙 서버에 대해서는 DownStream 이지만, 지역 저장소에 대해서는 UpStream 임
    - 이러한 경우에는 중앙 원격 저장소를 `UpStream` , 중간 원격 저장소를 `origin` 이라고 함
    - 중간 원격 저장소 `origin` 과 지역 저장소 `DownStream` 사이를 매개하는 원격 저장소가 추가로 존재할 수 있음
    - 이러한 경우에는 해당 원격 저장소를 `alt` 라고 함

![UpStream 과 DownStream](https://user-images.githubusercontent.com/116495744/211154052-2ff95f43-2a95-4422-8a5e-c9061134726c.jpg)

</details>

<details><summary><h4>Local Repository 생성하기</h4></summary>

- [**Git DownLoad & Install**](https://git-scm.com/downloads)

- **Working Directory 로 이동하여 `git bash` 창 열기**

- **해당 작업 공간을 Local Repository 로 지정하기**

  ~~~
  git init
  ~~~

  - `init`

    - 해당 경로가 Local Repository 가 아닌 경우 Local Repository 로 지정함
    - 해당 경로가 Local Repository 인 경우 기존 내역을 초기화함

</details>
 
<details><summary><h4>Local Repository 에 GitHub 계정 연결하기</h4></summary> 
  
- **속성 확인하기**

  ~~~
  git config --list
  ~~~

  - `config` : Git 과 관련된 사항을 저장하고 있는 폴더 `.git` 의 환경설정 담당 파일 `config` 에 대하여 기능함
    
    - `--list` : 파일 config 에 기입된 속성 및 값의 목록을 조회함

- **속성 `user.name` , `user.email` 에 값 설정하기**

  ~~~
  git config --global user.name <깃허브 계정 이름>
  git config --global user.email <깃허브 계정 이메일>
  ~~~

  - `config` : Git 과 관련된 사항을 저장하고 있는 폴더 `.git` 의 환경설정 담당 파일 `config` 에 대하여 기능함
  
    - `--global` : 기입할 설정값을 해당 경로 및 하위 폴더에 대하여 모두 적용되는 전역변수로 지정함
    - `--local` : 기입할 설정값을 지역변수로 지정하는 옵션으로서, 프로젝트마다 다른 계정을 사용하고 싶을 때 사용함

</details>
    
<details><summary><h4>Local Repository 에 Remote Repository 연동하기</h4></summary> 
  
- **Local Repository 에 연동되어 있는 Remote Repository 내역 조회하기**

  ~~~
  git remote -v
  ~~~

  - `remote` : 해당 Local Repository 와 연동된 Remote Repositories 에 관하여 동작함
    
    - `-v` : 해당 Local Repository 와 연동된 Remote Repositories 내역을 조회함

- **Local Repository 에 특정 Remote Repository 연동하기**

  ~~~
  git remote add <원격 저장소 이름> <원격 저장소 주소>
  ~~~

  - `remote` : 해당 Local Repository 와 연동된 Remote Repositories 에 관하여 동작함

  - `add` : 해당 Local Repository 와 연동된 Remote Repositories 에 대하여 후술할 사항을 추가함

  - `원격 저장소 이름` : 현재 연동할 Remote Repository 호출 시 주소 대신 사용할 이름
    - 관례상 주 원격 저장소를 `origin` 으로 사용함
    - `origin` 으로 설정된 주 원격 저장소 외에 다른 원격 저장소를 추가할 경우, 관례상 해당 원격 저장소를 `alt` 라고 이름함
  
- **Local Repository 와 특정 Remote Repository 간 연동 해제하기**
  
  ~~~
  git remote remove <원격 저장소 이름>
  ~~~
  
  - `remote` : 해당 Local Repository 와 연동된 Remote Repositories 에 대하여 동작함
  - `remove` : 해당 Local Repository 와 연동된 Remote Repositories 에 대하여 후술할 사항을 삭제함

</details>  

<details><summary><h4>Remote Repository DownLoad</h4></summary>

- **주의**
  - Remote Repository 의 모든 branch 를 내려받지 않음
  - default 로 설정되어 있는 branch `main` 의 내역만 내려받음
  - 특정 branch 를 내려받는 방법은 후술함
  
- **덮어쓰기**

  ~~~
  git clone <내려받을 원격 저장소 주소> <원격 저장소 이름>
  ~~~
  
  - `clone` : Remote Repository 의 내역을 가져와서 Local Repository 의 내역을 무시하고 덮어씀
  
- **가져와서 병합하기**
  
  ~~~
  git pull <내려받을 원격 저장소 주소> <원격 저장소 이름>
  ~~~
  
  - `pull` : Remote Repository 의 내역을 가져와서 Local Repository 의 내역과 병합함
    
    - Local Repository 의 변경 사항을 commit 하지 않은 상태에서 수행할 경우 덮어쓰기 오류가 발생할 수 있음

- **가져오기** 
  
  ~~~
  git fetch <내려받을 원격 저장소 주소> <원격 저장소 이름>
  ~~~
  
  - `fetch` : Remote Repository 의 내역을 가져와서 브랜치명 `FETCH_HEAD` 으로 임시 분기한 상태로 열람함

</details>

<details><summary><h4>Local Repository UpLoad</h4></summary>

- **Local Repository 의 변경 내역 올려주기**  
  
~~~
git push <원격 저장소 이름> <원격 브랜치 이름>
~~~

- `push` : Local Repository 의 변경 내역을 Remote Repository 에 올려줌

</details>
  
<details><summary><h4>Repository 병합하기</h4></summary>

</details>
  
---

## Version Control

<details><summary><h4>Concept</h4></summary>

- **Version Control Tools**
  - **Commit** : 데이터 변경 내역 혹은 확정본(Version)
  - **Tag** : 데이터 변경 내역에 다는 꼬리표로서, 통상적으로는 변경 내역 중 확정본에 사용됨
  - **Branch** : 데이터 변경 내역의 흐름
  
- **가지치기**
  - 특정 변경 내역에서 분기하여 새로운 흐름을 생성하는 작업
  - 기존 흐름을 훼손하지 않으면서 각기 분리된 작업 흐름을 생성할 수 있음
  - 통상적으로는 `Main Branch` 에서 `Sub Branch` 로 가지치기함

    - `Main` : 확정본 내역을 기록하는 브랜치
    - `Sub` : 확정본으로부터 분기되어 변경된 사항들을 기록하는 브랜치

  - 가지치기의 핵심은 확정본 내역을 기록하는 브랜치에 확정본 내역 이외의 내역을 남기지 않는 것임
  - 따라서 `Main Branch` 에는 확정본 내역만을 기록하고, `Sub Branch` 에는 작업 내역을 기록함
  
- **가지치기 기법**
  - **Two Branch** : `Main` 과 `Develop` 을 구분하지 않음
    - `Integration` : `Main` 과 `Develop` 을 겸하는 브랜치
      - `Main` : 확정본 내역을 기록하는 브랜치
      - `Develop` : `Sub` 들을 병합하는 작업을 수행하는 브랜치

    - `Topic` : `Integration` 에서 분기하어 작업 주제에 따라 구분된 `Sub`

    ![My First Board (3)](https://user-images.githubusercontent.com/116495744/211156449-5cfe37b7-0a27-4ea0-818b-090af87ffff7.jpg)

  - **Five Branch** : `Main` 과 `Develop` 을 구분함
    - `Main` : 확정본 내역을 기록하는 브랜치
    - `Develop` : `Sub` 들을 병합하는 작업을 수행하는 브랜치
    - `Feature` : `Develop` 에서 분기하어 작업 주제에 따라 구분된 `Sub`
    - `Release` : `Develop` 에서 확정된 내역을 `Main` 으로 배포하는 작업을 수행하는 브랜치
    - `Hot-Fix` : `Develop` 을 거치지 않고 신속하게 수정하고 싶을 때 `Main` 에서 임시 분기하는 브랜치

    ![My First Board (2)](https://user-images.githubusercontent.com/116495744/211156467-bc227f66-d40a-40da-9624-d29f43382fdc.jpg)

</details>


</details>

<details><summary><h4>Branch</h4></summary>

- **지역 저장소에서 Branch 생성하기**
  

  - Remote Repository 의 특정 Branch 를 추적하는 지역 저장소 브랜치 생성하기
  
    ~~~
    git checkout -track <지역 저장소 브랜치 이름> <원격 저장소 이름>/<내려받을 브랜치 이름>
    ~~~
  
  -
  
git checkout --track -branch <지역 저장소에서 이름할 브랜치 이름> <원격 저장소 이름>/<내려받을 브랜치 이름>
  
- 각 로컬 브랜치들이 어느 원격 브랜치들을 추적하고 있는지 확인
  
  ~~~
  git branch -vv
  ~~~

</details>

---

## Version

<details><summary><h4>Concept</h4></summary>

- **Version Control Tools**

  - **Commit** : 데이터 변경 내역 혹은 확정본(Version)
  - **Tag** : 데이터 변경 내역에 다는 꼬리표로서, 통상적으로는 변경 내역 중 확정본에 사용됨
  - **Branch** : 데이터 변경 내역의 흐름

- File Status

  

</details>

<details><summary><h4>변경 내역 Commit 하기</h4></summary>

- Commit 
  
</details>

<details><summary><h4>변경 내역 임시저장하기</h4></summary>

- **임시저장 목록 조회하기**

  ~~~
  git stash list
  ~~~

  - `stash` : 임시저장 목록에 대하여 기능함
  - `list` : 임시저장 목록을 조회함


- **Staged 된 파일 임시저장하기**

  ~~~
  git stash save
  ~~~
  
  - `stash` : 임시저장 목록에 대하여 기능함
  - `save` : 현재 Staged 된 파일을 임시저장하여 목록에 추가함

- **임시저장한 항목 불러와서 적용하기**

  ~~~
  git stash apply <Stash 이름>
  git stash show -p
  ~~~
  
  - `stash` : 임시저장 목록에 대하여 기능함
  - `apply` : 임시저장 목족 중 특정 항목을 현재 위치한 브랜치 커밋에 불러와서 적용함
  - `show -p` : 현재 위치한 브랜치 커밋과 불러와서 적용한 임시저장 항목 간 변경 내역을 확인함

- **임시저장한 항목 불러와서 적용하기**

  ~~~
  git stash apply <Stash 이름> --index
  ~~~
  
  - `stash` : 임시저장 목록에 대하여 기능함
  - `apply` : 임시저장 목족 중 특정 항목을 현재 위치한 브랜치 커밋에 불러와서 적용함
  - `--index` : 충돌 사항이 존재하면 알리고, 존재하지 않으면 적용 후 `add` 하여 stage 에 업로드함  
  
- **임시저장한 항목 삭제하기**

  ~~~
  git stash drop <Stash 이름>
  git stash clear
  ~~~
  
  - `stash` : 임시저장 목록에 대하여 기능함
  - `drop` : 임시저장한 특정 항목을 목록에서 삭제함
  - `clear` : 임시저장한 모든 항목을 목록에서 삭제함

  
</details>

<details><summary><h4>Commit 조회하기</h4></summary>

- Commit 
  
</details>

<details><summary><h4>Commit 되돌리기</h4></summary>

- **특정 Commit 으로 이동하기**

  ~~~
  git checkout <커밋 주소>
  ~~~

  - `checkout` : 해당 Commit 으로 이동함
  
  - `<커밋 주소>` : 취소하고 싶은 Commit 의 주소
    - 해당 Commit 의 주소값 앞 다섯 자리를 기입함
    - 최신 Commit `HEAD` 로부터 n 이전 시점으로 이동하고 싶을 경우 `HEAD~n` 를 기입함

- **Commit 취소하기**

  ~~~
  git revert <커밋>
  ~~~

  - `revert` : 해당 Commit 내역을 취소함
    - Commit 내역을 삭제하지 않음
    - 해당 Commit 직전 Commit 으로 되돌리는 새로운 Commit 을 생성함
    
  - `<커밋 주소>` : 이동하고 싶은 Commit 의 주소
    - 해당 Commit 의 주소값 앞 다섯 자리를 기입함
    - 최신 Commit `HEAD` 로부터 n 이전 시점으로 이동하고 싶을 경우 `HEAD~n` 를 기입함  

- 
git reset --option <복귀하고 싶은 commit hash>
reset : 되돌리고자 하는 commit 이후의 모든 commit을 삭제함
option
--soft : HEAD의 상태는 되돌리되, 워킹 디렉토리의 상태는 유지하고, stage area 에 변경된 내역에 대해서 add 함
--mixed : HEAD의 상태는 되돌리되, Stage Area 와 워킹 디렉토리의 상태는 유지함
--hard : HEAD, Stage Area, Working Directory 의 상태를 모두 되돌림  
  
</details>  
  
<details><summary><h4>Tag</h4></summary>

- **지역 저장소에서 태그 생성하기**
  - `git tag <Tag Name>` : 현재 위치한 commit 에 LightWeight Tag 생성
  - `git tag -a <Tag Name> -m "Tag Description"` : 현재 위치한 commit 에 Annotated Tag 생성

- **지역 저장소에서 태그 삭제하기**
  - `git tag -d <Tag Name>` : 태그명 Tag Name 삭제

- **지역 저장소의 태그 조회하기**
  - `git tag` : 전체 태그 조회
  - `git tag -1 <condition.*>` : condition 을 포함하는 태그 조회
  
  - `git tag show <Tag Name>` : 태그명 Tag Name 의 상세 정보 조회
    - 해당 태그의 Tag Dscription
    - 해당 태그 작성자
    - 해당 태그 생성일
    - 해당 태그가 설정된 commit 상세 정보

- 지역 저장소에서 태그를 통해 특정 coomit 으로 이동하기
  - `git checkout tags/<Tag Name>

- **지역 저장소의 태그 변동 내역을 원격 저장소에 반영하기**
  - `git push origin --tags` : 원격 저장소에 지역 저장소의 전체 태그를 반영
  - `git push origin <Branch Name> --tags` : 원격 저장소에 지역 저장소의 브랜치명 Branch Name 의 전체 태그를 반영
  - `git push origin <Tag Name>` : 원격 저장소에 태그명 Tag Name 을 반영 

</details>
