# API 명세

* 
## 00. 참고사항

* Body 는 Json으로 받고 보낸다. 
* \[유저\] 와 \[친구\] 명세는 이전 프로젝트와 동일 

## 01. 유저

1. POST /account/signup - 회원가입
   * request
     * username string required - 닉네임
     * password string required - 패스워드
   * response
     * userId number required - 사용자 식별자
     * username string required - 닉네임
   * 응답 코드
     * 201 Created 
       * 정상적으로 회원가입이 완료된 경우
     * 400 Bad Request
       * 중복된 닉네임으로 회원가입을 시도한 경우
2. POST /account/login - 로그인
   * request
     * username string required - 닉네임
     * password string required - 패스워드
   * response
     * userId number required - 사용자 식별자
     * username string required - 닉네임
     * 응답 코드
       * 200 OK
         * 정상적으로 로그인이 완료된 경우
       * 400 Bad Request
         * 로그인에 실패한 경우

## 02. 친구 

1. GET /friends - 친구 리스트
   * request\(query\)
     * page number required - 페이지
     * size number required - 페이지당 사이즈
   * response
     * friends array\[\] required
       * userId number required 친구의 식별자
       * username string required 닉네임
   * 응답 코드
     * 200 OK
       * 친구를 정상적으로 받은 경우
     * 400 Bad Request
       * page나 size를 이상하게 전송한 경우
     * 403 Forbidden
       * 인증에 실패한 경우 
2. POST /friends/{friendId} - 해당 사용자에게 친구 요청 혹은 수락하기
   * path variable
     * friendId number required - 상대방 아이디
   * 응답 코드
     * 200 OK
       * 친구 요청에 성공한 경우
       * 서로 친구가 된 경우
     * 400 Bad Request
       * 이미 친구 요청한 사용자에게 중복으로 친구 요청을 한 경우
     * 403 Forbidden
       * 인증에 실패한 경우
3. DELETE /friends/{friendId} - 친구 요청 삭제하기
   * pathVariable
     * friendId number required - 상대방 식별자
   * 응답 코드
     * 200 OK
       * 친구 요청 삭제에 성공한 경우
     * 400 Bad Request
       * 친구 요청되지 않은 상대방에 삭제를 시도한 경우
     * 403 Forbidden

       * 인증에 실패한 경우
4. GET /friends/request - 내게 들어온 친구 요청 확인하기
   * request\(query\)
     * page number required - 페이지
     * size number required - 페이지 크기
   * response
     * requests array\[\] required - 친구 요청 리스트
       * userId number required - 요청한 사용자 id
       * username string required - 요청한 사용자 닉네임
   * 응답 코드
     * 200 OK
       * 응답에 성공한 경우
     * 400 Bad Request
       * page나 size를 잘못 전송한 경우
     * 403 Forbidden
       * 인증에 실패한 경우

### 

### 

## 02. 메

### 1 . 상시판매 메뉴 생

* POST /menu/make/normal 
  * Request
    * foodName string required - 음식 이름
    * price number required - 가격
    * startHour number required - 판매 시작 시간 
    * startMinute number required - 판매 시작 분 
    * endHour number required - 판매 종료 시간 
    * endMinute  number required - 판매 종료 분 
  * 응답코드
    * 200 ok
      * 메뉴 생성에 성공
    * 400 Bad Request
      * 잘못된 시간 입력했을 경우 

### 2. 메뉴 한정판매 기간 설정  

* POST /menu/{menuId}/limit
  * Path Variable
    * menuId number required - 한정판매를 설정할 메뉴의 아이디 
  * Request

    * limitedMonth number required - 한정 판매 종료 월
    * limitedDayOfMonth number required - 한정 판매 종료 일 



    * 응답코드
      * 200 OK
        * 한정판매 기간 설정에 성공한 경우
      * 400 Bad Request
        * 존재하지 않은 메뉴에 설정 시도한 경우
        * 이미 기간한정이 설정된 메뉴에 시도한 경우 

### 3 . 메뉴 한정판매  해제

* GET /menu/{menuId}/unlimit
  * Path Variable
    * menuId number required -  한정판매를 해제할 메뉴의 아이디 
  * 응답코드
    * 200 OK
      * 한정판매 해제에 성공한 경우
    * 400 Bad Request
      * 존재하지 않은 메뉴에 시도한 경우
      * 한정판매가 설정되지 않은 메뉴에 시도한 경우 





### 4. 메뉴 삭제

* DELETE /menu/{menuId}/delete
  * Path Variable
    * menuId number required - 삭제할 메뉴의 아이디 
  * 응답코드
    * 200 OK
      * 삭제에 성공한 경우
    * 400 Bad Request
      * 존재하지 않은 메뉴를 삭제 시도 경우
      * 이미 삭제된 메뉴를 삭제 시도한 경우



### 5. 메뉴 품절 설정

* GET /menu/{menuId}/soldout
  * Path Variable
    * menuId number required - 품절 설정할 메뉴의 아이디 



## 03. 주

## 04. 관심

## 05. 기프티콘

## 06. 결제



