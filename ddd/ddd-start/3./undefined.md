# 애그리거트 관련 궁금증

## 내가 작성한 질문

### 질문 주소

*  [https://stackoverflow.com/questions/67061492/in-ddd-is-comment-included-in-post-aggregate](https://stackoverflow.com/questions/67061492/in-ddd-is-comment-included-in-post-aggregate)



## 질문 내용

### **1 .가정**

* Board 도메인에 Post 와 Comment 가  존재

\*\*\*\*

### **2 . 헷갈리는 내**

* Comment 는 Post 없이 존재할 수 없으므로, 이에 따라 Comment는 Post Aggregate 에 존재해야 함 따라서 Board는 Post를 root aggregate 로 가지는 1개의 aggregate 를 가짐 
* 그러나 다른 관점으로는, aggregate 안에 존재하는 entity 들은 같은 생명주기를 가져야 함, 그러나 comment 와 post는 생명주기가 다름,  또한 Post의 변화가 comment에 영향을 끼치지 못하고, 그 반대도 마찬가지. 이렇게 본다면, Board 는 2개의 aggregate 를 가지고 있고 각각의 root aggregate는 Post 와 Comment  

### **3. 문제** 

*  **Comment는 Post 애그리거트에 포함되는가 포함되지 않는가**
  * 이 결과에 따라  하나의 도메인 안에 존재할 수 있는 aggregate 의 숫자도 결정됨  \[1개\] vs \[2개 이상 가능\]



## 4. 답변

### 1 . 결론

* 요구사항에 따라 달라질 수 있지만 가능하다. → 2개 이상 가능

### 2 . 이유

* **요구사항에 따른 이**

  * 1 . post 를 삭제해도 comment 를 유지하고 싶은 경우

    * Post 안에 존재한다면 같이 삭제되어서 안됨

  * 2. Comment 끼리의 상호작용을 하고 싶을 경우가 있다.
    * comment 가 시스템적으로 독립적으로 존재하는 편이 더 쉽기 때문

* 성능적 이
  * 1. 특정 유저의 모든 댓글을 보고싶은 경우
    * Post 안에 존재한다면 조회 시간이 굉장히 많이 걸림 
  * 2.  post가 comment 를 많이 가지게 되면,    즉리 로딩 시, 이러한 post 를 가지고 올 때마다   대량의 comment 도 같이 가져오게 되므로, 부하가 많이 걸리게 된다. 



