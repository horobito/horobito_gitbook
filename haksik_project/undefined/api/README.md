# API 명세

* 
## 00. 참고사항

* Body 는 Json으로 받고 보낸다. 
* \[유저\] 와 \[친구\] 명세는 이전 프로젝트와 동일 
* \[친구 \] 명세 삭제 

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

## 02. 친구  - 삭

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



1. POST /menus/make/default - 메뉴 만들기
   * Request
     * title String required - 메뉴 이름 
     * price number required - 메뉴 가격 
     * descrption string required - 메뉴 설명
     * startTime LocalDateTime required - 판매 시작 시간 
     * endTime LocalDateTime required - 판매 종료 시간
     * amount number required - 초기 수량 
     * imageURL string required - 이미지 url 
   * 응답 코드
     * 201 Created
       * 정상적으로 메뉴가 생성되었을 때,
     * 400 Bad Request
       * 잘못된 시간 값이 입력되었을 때,
       * 해당 메뉴가 이미 등록되었을 때 

//////////////////////////////// 삭제됨 ////////////////////

1. POST /menus/limited - 한정 메뉴 만들기 
   * Request
     * menuName String required - 메뉴 이름 
     * price number required - 메뉴 가격 
     * descrption string required - 메뉴 설명 
     * startTime LocalDateTime required - 판매 시작 시간 
     * endTime LocalDateTime required - 판매 종료 시간
     * amount number required - 초기 수량 
     * imageURL string required - 이미지 url 
     * limitedTime LocalDateTime required - 한정판매 종료 날짜 
   * 응답 코드
     * 201 Created
       * 정상적으로 메뉴가 생성되었을 때,
     * 400 Bad Request
       * 잘못된 시간 값이 입력되었을 때,
       * 해당 메뉴가 이미 등록되었을 때 

///////////////////////// 삭제됨 ////////////////////////////////

2 . GET /menus/{menuId} - 메뉴 정보 조회

* Path variable
  * menuId number required - 메뉴 식별자
* response
  * id number required - 메뉴 식별자
  * title string required - 메뉴 이름
  * description string required - 메뉴 설명
  * image string required - 메뉴 이미지 url
  * price number required - 메뉴 가격 
  * startTime LocalDateTime required - 판매 시작 시간 
  * endTime LocalDateTime required - 판매 종료 시간
* 응답 코드
  * 200 OK
    * 정상적으로 응답이 전송된 경우
  * 400 Bad Request
    * 존재하지 않은 메뉴를 조회한 경우 

3 . PUT /menus/{menuId}/add/{amount} - 메뉴 수량 추가

* Path variable
  * menuId number required - 메뉴 식별자
  * amount number amount - 추가할 수량 
* Response
  * 200 OK
    * 수량 추가에 성공 
  * 400 Bad Request
    * 존재하지 않은 메뉴에 시도
    * 잘못된 수량\(0 이하의 수\) 입





4 . PUT /menus/{menuId}/subtract/{amount} - 메뉴 수량 차감

* Path variable
  * menuId number required - 메뉴 식별자
  * amount number amount - 차감할 수량
* Response
  * 200 OK
    * 수량 차감에 성공 
  * 400 Bad Request
    * 존재하지 않은 메뉴에 시도
    * 잘못된 수량\(메뉴의 현재 수량보다 많은 수\) 입력 

5 . PUT /menus/{menuId}/modify/{amount} - 메뉴 수량 변경

* Path variable
* menuId number required - 메뉴 식별자
* amount number amount - 변경할 수량
* Response
* 200 OK
  * 수량 변경에 성공 
* 400 Bad Request
  * 존재하지 않은 메뉴에 시도
  * 잘못된 수량\(음수 등 \) 입력 

6 . PUT /menus/{menuId}/limit - 기존 메뉴를 한정 메뉴로 바꾸기

* Path variable
  * menuId number required - 메뉴 식별자

    ////////// 삭제됨 ////////////////
* Request\(query\)
  * limitedTime LocalDateTime required - 한정판매 종료 날짜 

    ////////// 삭제됨 ////////////////
* Response
  * 200 OK
    * 한정 메뉴로 변경 성공 
  * 400 Bad Request
    * 존재하지 않은 메뉴에 시도
    * 이미 한정 메뉴 된 것에 시도 





7. PUT /menus/{menuId}/unlimit - 한정 메뉴를 기존 메뉴로 바꾸기

* Path variable
* menuId number required - 메뉴 식별자
* Response
* 200 OK
  * 한정 메뉴로 변경 성공 
* 400 Bad Request
  * 존재하지 않은 메뉴에 시도
  * 이미 한정 메뉴 된 것에 시도 

8. Delete /menus/{menuId} - 메뉴 삭제

* Path variable
  * menuId number required - 메뉴 식별자
* Response
  * 200 OK
    * 메뉴 삭제에 성공 
  * 400 Bad Request
    * 존재하지 않은 메뉴에 시도

## 

## 03. 카테고





1 .POST /categories - 카테고리 생성

* Request 
  * category string required - 카테고리 이름 
  * description string required - 카테고리 설명 
* 응답 코드 
  * 201 Created
    * 정상적으로 메뉴가 생성되었을 때

2 .POST /categories/{categoryId}/menu/ - 카테고리에 메뉴 추가

* Path variable
  * categoryId number required - 카테고리 식별자
* Request
  * menuId number required - 메뉴 식별자 
* 응답 코드
  * 201 Created
    * 정상적으로 카테고리에 메뉴가 추가되었을 때
  * 400 Bad Request
    * 해당 카테고리가 존재하지 않을 때,
    * 해당 메뉴가 존재하지 않을 때
    * 카테고리 내 이미 메뉴가 존재할 때 

3 . DELETE /categories/{categoryId}/menu/{menuId} - 카테고리 내 메뉴 제거

* Path variable
  * categoryId number required - 카테고리 식별자
  * menuId number required - 메뉴 식별자  
* 응답 코드
  * 200 OK
    * 정상적으로 카테고리에 메뉴가 제거되었을 때 
  * 400 Bad Request
    * 해당 카테고리가 존재하지 않을 때,
    * 해당 메뉴가 존재하지 않을 때
    * 카테고리 내 메뉴가 존재하지 않을 때 





4 .GET /categories/{categoryId} - 카테고리 정보 불러오기

* Path variable
  * categoryId number required - 카테고리 식별자
* Response
  * id number required - 카테고리 식별자
  * category string required - 카테고리 이름
  * description string required - 카테고리 설명 
  * menus array\[\] required - 메뉴
    * id number required - 메뉴 식별자
    * title string required - 메뉴 이름
    * description string required - 메뉴 설명
    * imageURL string required - 이미지 URL
    * price number required - 메뉴 가격 
* 응답 코드
  * 200 OK
    * 정상적으로 응답이 전달되었을 때 
  * 400 Bad Request
    * 해당 카테고리가 존재하지 않을 때,

5 .Delete /categories/{categoryId} - 카테고리 삭제

* Path variable
  * categoryId number required - 카테고리 식별자
* 응답 코드
  * 200 OK
    * 정상적으로 삭제되었을 때 
  * 400 Bad Request
    * 해당 카테고리가 존재하지 않을 때,

6 . GET /categories - 카테고리 세부정보 불러오기

* categories array\[\] required - 카테고리
  * id number required - 카테고리 식별자
  * category string required - 카테고리 이름
  * description string required - 카테고리 설명 
  * menus array\[\] required - 메뉴
    * id number required - 메뉴 식별자
    * title string required - 메뉴 이름
    * description string required - 메뉴 설명
    * imageURL string required - 이미지 URL
    * price number required - 메뉴 가격 



7 .GET /category/{cateogryId} - 카테고리 세부 조회 

* Request\(query\)
  * cursor string required - 다음 조회에 필요한 커서  
  * size number required - 한번 요청시 가져올 사이즈 
* Path variable
  * categoryId number required - 카테고리 식별자 
* Response
  * hasNext boolean required - 요청한 사이즈보다 더 많은 메뉴가 있을 경우, true
  * cursor string required 
  * menus array\[\] required 
    * id number required - 메뉴 식별자
    * title string required - 메뉴 이름
    * description string required - 메뉴 설명
    * imageURL string required - 이미지 URL
    * price number required - 메뉴 가격 

8 .PUT /categories/{categoryId}/ - 카테고리 제목 및 설명 변경 

* Path variable
  * categoryId number required - 카테고리 식별자 
* Request
  * category string required - 변경할 이름
  * description string required - 변경할 내용 
* 응답 코드
  * 200 OK
    * 성공적으로 변경이 완료
  * 400 Bad Request
    * 존재하지 않은 카테고리에 시도
    * 잘못된 값 입력\(아무것도 없는 내용 또는 제목 \)

## 04. 주문



1 .POST /orders - 주문 생성 

* Request
  * orderLines array\[\] required - 주문 
    * menuId number required - 메뉴 식별자
    * count number required - 메뉴 수량 
* Response
  * orderId number required - 주문 식별자
  * ordererId - 유저 식별자
  * orderTime LocalDateTime required - 주문 시각 
  * orderLines array\[\] required - 각 주문 
    * orderLineId number required - 주문상세 식별자
    * menuId number required - 메뉴 식별자 
    * menuName string required - 메뉴 이름 
    * price number required - 메뉴 가격
    * count number required - 주문 수량
    * totalPrice number required - 해당 메뉴의 총 가격
  * totalPrice numbe required - 총 주문 비용
  * 주문QR 코드 \[QR코드 타입\] required - 주문 qr 코드 
* 응답 코드
  * 201 created
    * 주문 성공 
  * 400 Bad Request
    * 존재하지 않은 메뉴 주문 시도
  * 403 Forbidden
    * 인증 실패

2 .POST /orders/{orderId} - 주문에 메뉴 추가 

* Path variable
  * orderId number required - 주문 식별자  
* Request
  * orderLines array\[\] required - 추가 주문 
    * menuId number required - 메뉴 식별자
    * count number required - 메뉴 수량 
  * Response
  * orderId number required - 주문 식별자
  * ordererId - 유저 식별자
  * orderTime LocalDateTime required - 주문 시각 
  * orderLines array\[\] required - 각 주문 
    * orderLineId number required - 주문상세 식별자
    * menuId number required - 메뉴 식별자 
    * menuName string required - 메뉴 이름 
    * price number required - 메뉴 가격
    * count number required - 주문 수량  
    * totalPrice number required - 해당 메뉴의 총 가격
  * totalPrice numbe required - 총 주문 비용
  * 주문QR 코드 \[QR코드 타입\] required - 주문 qr 코드 
* 응답 코드
  * 201 created
    * 주문 추가 성공
  * 400 Bad Request
    * 존재하지 않은 메뉴 시도 또는 주문에 추가 시도
  * 403 Forbidden
    * 인증 실패



3 .PUT /orders/{orderId}/ - 주문 수량 변경

* Path variable
  * orderId number required - 주문 식별자  
* Request
  * orderLines array\[\] required - 변경할 주문 
    * menuId number required - 메뉴 식별자
    * count number required - 메뉴 수량 
    * Response
  * orderId number required - 주문 식별자
  * ordererId - 유저 식별자
  * orderTime LocalDateTime required - 주문 시각 
  * orderLines array\[\] required - 각 주문 
    * orderLineId number required - 주문상세 식별자
    * menuId number required - 메뉴 식별자 
    * menuName string required - 메뉴 이름 
    * price number required - 메뉴 가격
    * count number required - 주문 수량  
    * totalPrice number required - 해당 메뉴의 총 가격
  * totalPrice numbe required - 총 주문 비용
  * 주문QR 코드 \[QR코드 타입\] required - 주문 qr 코드 
* 응답 코드
  * 201 created
    * 주문 추가 성공
  * 400 Bad Request
    * 존재하지 않은 메뉴 시도 또는 주문에 추가 시도
  * 403 Forbidden
    * 인증 실패

4 .Delete /orders/{orderId}

* Path variable
  * orderId number required - 주문 식별자  
* 응답 코드
  * 200 OK
    * 성공적으로 주문 제거 
  * 400 Bad Request
    * 존재하지 않은 주문 제거 시도
  * 403 Forbidden
    * 인증 실패 



## 05. 관심



1. POST /interests/menu/{menuId} - 메뉴 좋아요 생성
   * Path variable
   * menuId number required - 메뉴 식별자
   * 응답코드
   * 200 OK
     * \[좋아요\] 가 성공적으로 반영됨 
   * 400 Bad Request
     * 존재하지 않은 메뉴에 시도 
   * 403 Bad Request 
     * 인증 실패 
2. POST /interests/category/{categoryId} - 카테고리 좋아요 생성
   * Path variable
   * cagegoryId number required - 메뉴 식별자
   * 응답코드
   * 200 OK
     * \[좋아요\] 가 성공적으로 반영됨 
   * 400 Bad Request
     * 존재하지 않은 메뉴에 시도 
   * 403 Bad Request 
     * 인증 실패 
3. PUT /interests/{interestId}category/{categoryId}/delete
   * 관심사항 중 특정 카테고리 좋아요 취소 
   * Path variable
     * interestId number required - 좋아요 식별자 
     * categoryId number required - 카테고리 식별자
   * 응답코드  
     * 200 OK
       * 성공적으로 해당 카테고리 좋아요 취소 
     * 400 Bad Request
       * 좋아요 하지 않은 카테고리에 시도 
       * 존재하지 않은 카테고리에 시도 
     * 403 Forbidden
       * 인증 실패
4. PUT /interests/{interestId}/menu/{menuId}/delete
5. 관심사항 중 특정 메뉴 삭제
   * Path variable
     * interestId number required - 좋아요 식별자 
     * categoryId number required - 카테고리 식별자
   * 응답코드  
     * 200 OK
       * 성공적으로 해당 메뉴 좋아요 취소 
     * 400 Bad Request
       * 좋아요 하지 않은 메뉴에 시도 
       * 존재하지 않은 메뉴 시도 
     * 403 Forbidden
       * 인증 실패
6. Delete /interest/{interestId} - 관심사항 삭제
   * Path variable
     * interestId number required - 좋아요 식별자
   * 응답코드  
     * 200 OK
       * 성공적으로 \[좋아요\] 삭제
     * 400 Bad Request
       * \[좋아요\] 정보가 없을 때 시도 
     * 403 Forbidden
       * 인증 실패





7. GET /interests/{interestId} - 관심사항 전체 정보 조회

* Path variable
  * interestId number required - 좋아요 식별자
* Response
  * interestId number required
  * user User required - 좋아요 소유 유저
    * userId
    * username
  * categorys array\[\] required
    * id number required - 카테고리 식별자
    * category string required - 카테고리 이름
    * description string required - 카테고리 설명 
  * menus array\[\] required 
    * id number required - 메뉴 식별자
    * title string required - 메뉴 이름
    * description string required - 메뉴 설명
    * imageURL string required - 이미지 URL
    * price number required - 메뉴 가격 
* 응답 코드
  * 200 OK
    * 성공적으로 응답 반환
  * 400 Bad Request
    * 해당 유저에 좋아요 정보가 없는 경우
  * 403 Forbidden
    * 인증 실패 

8. GET /interests/{interestId}/menus - 메뉴 좋아요 정보 요구

* Path variable
  * interestId number required - 좋아요 식별자 
* Response
  * interestId number required
  * user User required - 좋아요 소유 유저
    * userId
    * username
  * menus array\[\] required 
    * id number required - 메뉴 식별자
    * title string required - 메뉴 이름
    * description string required - 메뉴 설명
    * imageURL string required - 이미지 URL
    * price number required - 메뉴 가격 
* 응답 코드
  * 200 OK
    * 성공적으로 응답 반환
  * 400 Bad Request
    * 해당 유저에 좋아요 정보가 없는 경우
  * 403 Forbidden
    * 인증 실패 

9. GET /interests/{interestId}/categories - 카테고리 좋아요 정보 요구 

* Path variable
  * interestId number required - 좋아요 식별자 
* Response
  * interestId number required
  * user User required - 좋아요 소유 유저
    * userId
    * username
  * categorys array\[\] required
    * id number required - 카테고리 식별자
    * category string required - 카테고리 이름
    * description string required - 카테고리 설명 
* 응답 코드
  * 200 OK
    * 성공적으로 응답 반환
  * 400 Bad Request
    * 해당 유저에 좋아요 정보가 없는 경우
  * 403 Forbidden
    * 인증 실패 



## 6 . 기프티콘 요구사항

1 .POST /gifticons - 결제 후 결제 메뉴들에 대한 기프티콘 생성

* Request
  * paymentId number required -  결제 식별자 
* Response
  * userId number required - 유저 식별자
  * lockerId number requried - 기프티콘 보관함 식별자 
  * gifticons array\[\] required 
    * gifticonId number required - 기프티콘 식별자
    * createTime LocalDateTime required - 기프티콘 생성 시각 
    * menuId number required - 메뉴 식별자
    * count number required - 메뉴 수량
    * 기프티콘 QR코드 \[QR코드\] required - qr 코드 생성을 위한 값 
* 응답 코드
  * 201 create 
    * 기프티콘 생성
  * 400 Bad Request
    * 존재하지 않은 메뉴에 대해 기프티콘 생성 요청
  * 403 Forbidden
    * 인증 오류 

2 .GET /gifticons -  기프티콘 전체 정보 가져오기 

* Response
  * gifticons array\[\] required 
    * gifticonId number required - 기프티콘 식별자
    * createTime LocalDateTime required - 기프티콘 생성 시각 
    * menuId number required - 메뉴 식별자
    * count number required - 메뉴 수량
    * 기프티콘 QR코드 \[QR코드\] required - qr 코드 생성을 위한 값 
* 응답 코드
  * 201 create 
    * 기프티콘 생성
  * 400 Bad Request
    * 존재하지 않은 메뉴에 대해 기프티콘 생성 요청
  * 403 Forbidden
    * 인증 오류 

3 .GET /gifticons/{gifticonId} - 기프티콘 상세 정보 가져오기

* Path variable
  * gifticonId number requried - 기프티콘 식별자
* Response
  * gifticonId number required - 기프티콘 식별자
  * createTime LocalDateTime required - 기프티콘 생성 시각 
  * menuId number required - 메뉴 식별자
  * count number required - 메뉴 수량
  * 기프티콘 QR코드 \[QR코드\] required - qr 코드 생성을 위한 값 
* 응답코드
  * 200 OK
    * 성공적으로 응답 반환 
  * 400 Bad Request
    * 존재하지 않은 기프티콘 조회 요청 
  * 403 Forbidden
    * 인증 오류 



POST 를 제외한 메소드들은 멱등성이 보장되어야 한다. 4. POST 4 .4 .gifticons/{gifticonId}/present - 기프티콘 선물

* Path Variable
  * gifticonId number requried - 기프티콘 식별자
* Request
  * username string required - 유저 식별자 
  * count number required - 보낼 수량 
* Response 
  * 200 OK
    * 성공적으로 기프티콘 전송 
  * 400 Bad Request
    * 존재하지 않은 기프티콘 선물
  * 401 unauthorized
    * 친구관계가 아닌 이에게 선물 
  * 403 Forbidden
    * 인증 오류 





## 7. 결제 요구사항 





1 POST /payments/ - 결제 시도

* Request
  * orderId number required - 주문 식별자
* Response
  * paymentId number required - 결제 식별자
  * payerId number required - 지불자 식별자
  * paymentTime LocalDateTime required - 결제 시각  
  * payInfos arrays\[\] required 
    * menuId number required - 메뉴 식별자
    * count number required - 메뉴 갯수 
    * total price - 메뉴 총 가격 
  * totalCount number required - 전체 총 수량 
  * totalPrice number required - 전체 총 가격 
  * 결제 QR코드 \[QR코드\] required - qr 코드 생성을 위한 값 
* 응답 코드
  * 200 OK
    * 결제 성공
  * 400 Bad Request

    -존재하지 않은 주문에 대한 결제 시도 

  * 403 Forbidden
    * 인증 실패 

1. Delete /payments/{paymentId} - 결제 취소
   * Path variable
     * paymentId number required - 결제 정보
   * 응답코드
     * 200 OK
       * 정상적으로 취소
     * 400 Bad Request
       * 존재하지 않은 결제에 시도
     * 403 Forbidden
       * 인증 실패 
2. GET /payments/{paymentId} - 결제 상세정보
   * Path variable
     * paymentId number required - 지불 정보
   * Response
     * userId number required - 유저 식별자
     * paymentTime LocalDateTime required - 결제 시각  
     * gifticons array\[\] required 
       * gifticonId number required - 기프티콘 식별자
       * menuId number required - 메뉴 식별자
       * count number required - 메뉴 수량

