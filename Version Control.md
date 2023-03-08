<h1 align='center'> Version Control </h1>

<details><summary><h4>Summary</h4></summary>

![My First Board (2)](https://user-images.githubusercontent.com/116495744/211156467-bc227f66-d40a-40da-9624-d29f43382fdc.jpg)

![My First Board (3)](https://user-images.githubusercontent.com/116495744/211156449-5cfe37b7-0a27-4ea0-818b-090af87ffff7.jpg)

</details>

---

## Concept

- **Version Control Tools**
    - **Commit** : 데이터 변경 확정 내역 혹은 최종본
    - **Tag** : 데이터 변경 확정 내역에 다는 꼬리표로서, 통상적으로는 커밋 중 최종본에 사용됨
    - **Branch** : 데이터 변경 확정 내역의 흐름
    
- **가지치기**
    - **특정 커밋에서 분기하여 새로운 흐름을 생성하는 작업**
      - 기존 흐름을 훼손하지 않으면서 각기 분리된 작업 흐름을 생성할 수 있음
   
    - **통상적으로는 `Main Branch` 의 커밋에서 `Sub Branch` 로 가지치기함**

        - `Main` : 최종본 내역을 기록하는 브랜치로서 기본값으로 설정되어 있음
        - `Sub` : 특정 최종본으로부터 분기되어 변경된 사항들을 기록하는 브랜치
    
- **가지치기 기법**
    - **가지치기의 핵심은 최종본 내역을 기록하는 브랜치에 최종본 내역 이외의 내역을 남기지 않는 것임**
      - `Main Branch` 에는 최종본 내역만을 기록함
      - `Sub Branch` 에는 작업 내역을 기록함

    - **Five Branch** : `Main` 과 `Develop` 을 구분함
        - `Main` : 최종본 내역을 기록하는 브랜치
        - `Develop` : `Sub` 들을 병합하는 작업을 수행하는 브랜치
        - `Feature` : `Develop` 에서 분기하어 작업 주제에 따라 구분된 `Sub`
        - `Release` : `Develop` 에서 확정된 내역을 `Main` 으로 배포하는 작업을 수행하는 브랜치
        - `Hot-Fix` : `Develop` 을 거치지 않고 신속하게 수정하고 싶을 때 `Main` 에서 임시 분기하는 브랜치

    - **Two Branch** : `Main` 과 `Develop` 을 구분하지 않음
        - `Integration` : `Main` 과 `Develop` 을 겸하는 브랜치
        - `Topic` : `Integration` 에서 분기하어 작업 주제에 따라 구분된 `Sub`



---
