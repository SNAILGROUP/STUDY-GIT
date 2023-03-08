<h1 align="center"> Distributed Repository </h1>

<details><summary><h4>Summary</h4></summary>
    
![UpStream 과 DownStream](https://user-images.githubusercontent.com/116495744/211154052-2ff95f43-2a95-4422-8a5e-c9061134726c.jpg)

</details>    
    
---

## Concept

- **Local 과 Remote**
    - **GitHub 에서는 원격 저장소를 중앙 서버로, 지역 저장소를 개별 네트워크로 사용함**
        - 원격 저장소 : GitHub 에서 제공하는 클라우드 저장소
        - 로컬 저장소 : 개별 참여자의 컴퓨터 저장소
  
    - **Local Repository** : 로컬 저장소
        - **Working Tree** : 분산형 버전 관리 프로그램 `Git` 의 관리를 받는 공간
        - **Stage** : Branch 에 변경 사항을 확정하여 하나의 버전으로 기록하기 위한 파일들을 모아두는 가상 공간
        - **Branch** : 확정된 변경 사항을 기록한 공간

    - **Remote Repository** : 원격 저장소
        - 자료 및 연산 자원을 저장하는 온라인 공간으로서, 클라우드(Cloud) 라고도 함
        - 구체적으로는 Working Directory 와 연동된 GitHub 의 Repository 를 가리킴

- **UpStream 과 DownStream**
    - **UpStream 과 DownStream 은 상대적 개념임**
        - 프로젝트의 중앙 서버에 가까울수록 `UpStream` 이라고 함
        - 프로젝트의 분산 네트워크에 가까울수록 `DownStream` 이라고 함
    
    - **로컬 저장소와 원격 저장소의 구분**
        - 통상적으로는 원격 저장소가 중앙 서버로서 기능함
        - 통상적으로는 로컬 저장소가 분산 네이트워크로서 기능함
        - 따라서 원격 저장소를 `UpStream` , 로컬 저장소를 `DownStream` 이라고 함
        - 혹은 원격 저장소를 `origin` 이라고 이름하기도 함
    
    - **원격 저장소끼리의 구분**
        - 중앙 서버로서 기능하지는 않으나, 중앙 서버와 로컬 저장소를 매개하는 원격 저장소가 존재할 수 있음
        - 해당 저장소는 중앙 서버에 대해서는 DownStream 이지만, 로컬 저장소에 대해서는 UpStream 임
        - 이러한 경우에는 중앙 원격 저장소를 `UpStream` , 중간 원격 저장소를 `origin` 이라고 함
        - 중간 원격 저장소 `origin` 과 로컬 저장소 `DownStream` 사이를 매개하는 원격 저장소가 추가로 존재할 수 있음
        - 이러한 경우에는 해당 원격 저장소를 `alt` 라고 함

---

## Local Repository

<details><summary><h4>Local Repository 생성하기</h4></summary>

- [**Git DownLoad & Install**](https://git-scm.com/downloads)
- **Working Directory 로 이동하여 `git bash` 창 열기**
- **해당 작업 공간을 로컬 저장소로 지정하기**

    ~~~
    git init
    ~~~

    - `init`

        - 해당 경로가 `Git` 의 관리를 받는 로컬 저장소가 아닌 경우 로컬 저장소로 지정함
        - 해당 경로가 `Git` 의 관리를 받는 로컬 저장소인 경우 기존 관리 내역을 초기화함

</details>

<details><summary><h4>Local Repository 내역 조회하기</h4></summary>

~~~
git ls <option>
~~~

- `ls` : 해당 위치의 하위 단위에 대하여 조회함
    
- `<option>`
    - `none` : 현재 디렉토리에 존재하는 파일 및 하위 디렉토리 조회
    - `-a` : 숨김파일 및 디렉토리를 포함하여 조회
    - `-l` : 파일 상세정보 출력
    - `-r` : 역순으로 정렬하여 출력
    - `-t` : 시간 내림차순으로 정렬하여 출력
    
</details>    

---

## Interlock
    
<details><summary><h4>Working Directory 에 GitHub 계정 연결하기</h4></summary> 

~~~
// 깃허브 계정 이름 및 이메일 등록
git config --global user.name <깃허브 계정 이름>
git config --global user.email <깃허브 계정 이메일>
~~~

- `config` : Git 과 관련된 사항을 저장하고 있는 폴더 `.git` 의 환경설정 담당 파일 `config` 에 대하여 기능함

- `<option>`
    - `--list` : 필드 및 값의 목록을 조회함
    - `<Field>` : 특정 필드에 설정된 값을 조회함
    - `--global <Field> <Value>` : 특정 필드에 대하여 전역 변수로 작동하는 값을 설정함
    - `--local <Field> <Value>` : 특정 필드에 대하여 지역 변수로 작동하는 값을 설정함
    - `--unset <Field>` : 특정 필드에 설정된 값을 삭제함

</details>
    
<details><summary><h4>특정 Remote Repository 와 연동된 Local Repository 생성하기</h4></summary> 

~~~
// 원격 저장소 내역 가져와서 덮어쓰기
git clone <원격 저장소 주소>

// 원격 저장소 내역이 저장된 폴더로 이동
cd <원격 저장소 내역이 저장된 폴더 경로>

// 해당 폴더를 원격 저장소와 연동
git remote add <원격 저장소 이름> <원격 저장소 주소>
~~~

- `remote add` : 해당 로컬 저장소와 연동된 원격 저장소 목록에 신규 항목을 추가함        
    - `원격 저장소 이름` : 현재 연동할 원격 저장소 호출 시 주소 대신 사용할 이름
        - 관례상 주 원격 저장소를 `origin` 으로 사용함
        - `origin` 으로 설정된 주 원격 저장소 외에 다른 원격 저장소를 추가할 경우, 관례상 해당 원격 저장소를 `alt` 라고 이름함    

    - `원격 저장소 주소` : 현재 연동할 원격 저장소의 주소(url)
        - 깃허브 레파지토리 우측 상단의 `<> Code` 를 클릭하여 확인
    
</details>    
    
<details><summary><h4>Local Repository 에 연동되어 있는 Remote Repository 내역 조회하기</h4></summary> 

~~~
git remote <option>
~~~

- `remote` : 해당 로컬 저장소와 연동된 원격 저장소에 관하여 동작함

- `<option>`
    - `none` : 해당 로컬 저장소와 연동된 원격 저장소 내역에 대하여 그 이름만 조회함
    - `-v` : 해당 로컬 저장소와 연동된 원격 저장소에 대하여 그 이름과 주소를 함께 조회함
    
</details>     
    
<details><summary><h4>Local Repository 에 Remote Repository 연동 해제하기</h4></summary>     
  
~~~
git remote remove <원격 저장소 이름>
~~~

- `remote remove` : 해당 로컬 저장소와 연동된 원격 저장소 목록에 대하여 후술할 사항을 삭제함

</details>  
    
---
    
## Up & Down
    
<details><summary><h4>UpLoad Local Repository</h4></summary>
  
~~~
// Modifed File 을 Staged 상태로 전환함
git add <Modified 파일 이름>
    
// Staged Files 를 변경 확정하여 로컬 브랜치에 기록함
git commit -m "커밋에 대한 설명"
    
// 변경 확정 내역을 원격 저장소의 브랜치에 반영함
git push <원격 저장소 이름> <원격 브랜치 이름>
~~~

- `add` : 워킹트리에서 수정된 파일을 스테이지에 추가하여 스테이지 상태로 전환함
    - 최신 커밋 이후 변경 사항이 존재하는 상태를 Modified(수정된) 라고 정의함
    - 변경 사항을 확정할 파일들을 모아두는 가상 공간 스테이지에 올라간 상태를 Staged(스테이지에 올라간) 라고 정의함
    - 특정 수정된 파일이 아니라 모든 수정된 파일을 선택하는 경우 전체 선택자 `*` 을 기입함

- `commit` : 스테이지에 추가된 변경 사항을 확정하여 현재 위치한 브랜치에 기록함

- `push` : 로컬 저장소의 변경 확정 내역을 연동된 원격 저장소의 브랜치에 올려줌
    - 현재 위치한 로컬 저장소의 브랜치의 변경 내역에 대하여,
    - 해당 브랜치가 추적하고 있는 브랜치에 반영함
    
</details>
    
<details><summary><h4>DownLoad Remote Repository</h4></summary>

- **주의**
    - 원격 저장소의 모든 브랜치를 내려받지 않음
    - 기본값으로 설정되어 있는 브랜치 `main` 의 내역만 내려받음
    - 특정 브랜치를 내려받는 방법은 후술함
  
- **가져와서 덮어쓰기**

    ~~~
    git clone <내려받을 원격 저장소 주소>
    ~~~
  
    - `clone` : 원격 저장소의 내역을 가져와서 로컬 저장소의 내역을 무시하고 덮어씀
  
- **가져와서 병합하기**
  
    ~~~
    git pull <내려받을 원격 저장소 주소>
    ~~~
  
    - `pull` : 원격 저장소의 내역을 가져와서 로컬 저장소의 내역과 병합함
    
        - 로컬 저장소의 변경 사항을 커밋하지 않은 상태에서 수행할 경우 덮어쓰기 오류가 발생할 수 있음

- **가져오기** 
  
    ~~~
    git fetch <내려받을 원격 저장소 주소>
    ~~~
  
    - `fetch` : 원격 저장소의 내역을 가져와서 브랜치명 `FETCH_HEAD` 으로 임시 분기한 상태로 열람함

</details>
    
---
    
## Intergrate
    
<details><summary><h4>Repository 병합하기</h4></summary>    
    
</details>    
    
---
    
## SubTree
    
<details><summary><h4>Concept</h4></summary>

- **주의**
    - **이 작업은 원격 저장소 간 위계를 설정하는 작업임**
    - 상위 저장소의 폴더에 하위 저장소의 메인 브랜치 `main` 의 내역을 연동함
    - 상위 저장소에 하위 저장소를 병합하는 작업이 아님
    - 하위 저장소를 삭제하지 않고 기존 위치에 유지함
    
- **용어 정리**
    - **상위 원격 저장소 `upstream`** : 하위 저장소의 내역을 포함할 저장소
    - **상위 로컬 저장소** : 상위 원격 저장소와 연동되어 있는 로컬 저장소
    - **하위 원격 저장소 `origin`** : 상위 저장소에 내역이 포함될 저장소
    - **하위 로컬 저장소** : 하위 원격 저장소와 연동되어 있는 로컬 저장소
    - **서브트리** : 하위 원격 저장소의 내역을 저장할 상위 원격 저장소의 폴더
    - **브랜치 `feature/subtree`** : 상위 저장소에서 서브트리 작업할 브랜치

- **초기 환경 설정**
    
    ~~~
    git clone <상위 원격 저장소 주소>

    cd <상위 원격 저장소 내역을 내려받은 저장소 root 경로>
    git remote add upstream <상위 원격 저장소 주소>
    
    git remote add origin <하위 원격 저장소 주소>
    
    git branch feature/subtree
    ~~~
    
![My First Board](https://user-images.githubusercontent.com/116495744/212480105-605d5f1a-4fb2-49b2-9c7d-11d2f4c428cb.jpg)

</details>    
    
<details><summary><h4>SubTree 만들기</h4></summary>
    
~~~
// 상위 로컬 저장소의 root 로 이동
cd <상위 로컬 저장소의 root 경로>

// 서브트리 작업 브랜치 feature/subtree 로 이동
git checkout feature/subtree

// 하위 원격 저장소를 상위 로컬 저장소의 하위 폴더로 저장
git subtree add --prefix <서브트리 이름> origin feature/subtree

// 해당 사항을 상위 원격 저장소 upstream 의 브랜치 feature/subtree 에 갱신
git push upstream feature/subtree
~~~

- `subtree add` : 현재 위치한 저장소에 하위 저장소의 내역을 추가함

- `--prefix` :  병합 세부 조건을 설정함

    - `<서브트리 이름>` : 하위 원격 저장소의 내역을 저장할 상위 원격 저장소의 폴더 이름
    - `origin` : 상위 로컬 저장소에서 설정한, 상위 원격 저장소에 저장할 하위 원격 저장소 이름
    - `feature/subtree` : 하위 원격 저장소를 병합한 내역을 기록할 로컬 저장소 브랜치 이름

</details>
    
<details><summary><h4>하위 원격 저장소의 변경 확정 내역 SubTree 에 갱신하기</h4></summary>
    
~~~
// 상위 로컬 저장소의 root 로 이동
cd <로컬 저장소의 root 경로>

// 서브트리 작업 브랜치 feature/subtree 로 이동
git checkout feature/subtree

// 하위 원격 저장소 origin 의 변경 확정 내역을 상위 로컬 저장소로 가져와서 병합하기
git subtree pull --prefix <서브트리 이름> origin feature/subtree

// 해당 내역을 상위 원격 저장소에 갱신
git push upstream feature/subtree
~~~

- `subtree pull` : 상위 저장소에 하위 저장소의 내역을 가져와서 병합함

- `--prefix` :  병합 세부 조건을 설정함

    - `<서브트리 이름>` : 하위 원격 저장소의 내역을 저장하고 있는 상위 원격 저장소의 폴더 이름
    - `origin` : 상위 로컬 저장소에서 설정한, 서브트리와 연동되어 갱신 예정인 하위 원격 저장소 이름
    - `feature/subtree` : 하위 원격 저장소를 병합한 내역을 기록할 로컬 저장소 브랜치 이름
    
</details>   
    
<details><summary><h4>상위 원격 저장소의 SubTree 변경 확정 내역 하위 원격 저장소에 갱신하기</h4></summary>
    
~~~    
// 상위 로컬 저장소의 서브트리 작업 브랜치 feature/subtree 로 이동
git checkout feature/subtree

// 서브트리 변경 사항 확정 후 해당 내역을 상위 원격 저장소에 반영
git add <서브트리 이름>
git commit -m "커밋에 대한 설명"
git push upstream feature/subtree

// 서브트리에 반영된 내역을 하위 원격 저장소에 갱신
// 하위 로컬 저장소에는 해당 내역이 자동으로 반영되지 않음
git subtree push --prefix <서브트리 이름> origin feature/subtree
~~~

- `subtree push` : 상위 저장소에서 갱신한 서브트리 내역을 하위 원격 저장소에 올려줌

- `--prefix` :  병합 세부 조건을 설정함

    - `<서브트리 이름>` : 하위 원격 저장소의 내역을 저장하고 있는 상위 원격 저장소의 폴더 이름
    - `origin` : 서브트리되어 갱신 예정인 하위 원격 저장소 이름
    - `feature/subtree` : 하위 원격 저장소를 병합한 내역을 기록할 로컬 저장소 브랜치 이름    
    
</details>
