## 1. 주제
**전자책 서점 관리 시스템**   
구매를 통해 도서 이용이 가능하다.   
구매한 도서 가격의 3%를 포인트로 지급한다.
+ 도서 관리
  + 소장 도서와 대여 도서 구분
  + 소장: 모든 도서 가능, 대여: 일부 도서만 가능
+ 회원 관리
+ 판매 관리
+ 리뷰 관리
  + 구매자와 비구매자의 리뷰 구분
***
## 2. E-R 다이어그램
![ER](https://github.com/aaaawg/database/blob/main/ER%20Diagram.png)
***
## 3. 릴레이션
+ **고객(<ins>아이디</ins>, 이름, 나이, 포인트)**  
    **슈퍼키**: 아이디, (아이디, 이름/나이/포인트), (아이디, 이름, 나이/포인트), (아이디, 나이, 포인트), (아이디, 이름, 나이, 포인트)  
    **후보키**: 아이디  
    **기본키**: 아이디  
    
+ **도서(<ins>ISBN</ins>, 도서명, 출판사, 출간일, 가격, 할인율)**  
    **슈퍼키**: ISBN, (ISBN, 도서명/출판사/출간일/가격/할인율), (ISBN, 도서명, 출판사/출간일/가격/할인율), (ISBN, 출판사, 출간일/가격/할인율), (ISBN, 출간일, 가격/할인율), (ISBN, 가격, 할인율), (ISBN, 도서명, 출판사, 출간일/가격/할인율), (ISBN, 도서명, 출간일, 가격/할인율), (ISBN, 출판사, 출간일, 가격/할인율), (ISBN, 도서명/출판사/출간일, 가격, 할인율), (ISBN, 도서명, 출판사, 출간일, 가격/할인율), (ISBN, 도서명/출판사, 출간일, 가격, 할인율), (ISBN, 도서명, 출판사, 출간일, 가격, 할인율)  
    **후보키**: ISBN  
    **기본키**: ISBN  

+ **도서_구분(<ins>ISBN</ins>, <ins>구분</ins>)**  
    **슈퍼키**: (ISBN, 구분)  
    **후보키**: (ISBN, 구분)  
    **기본키**: (ISBN, 구분)  
    **외래키**: ISBN  

+ **도서_저자(<ins>ISBN</ins>, <ins>저자</ins>)**  
    **슈퍼키**: (ISBN, 저자)  
    **후보키**: (ISBN, 저자)  
    **기본키**: (ISBN, 저자)  
    **외래키**: ISBN  
    
+ **리뷰(<ins>아이디</ins>, <ins>ISBN</ins>, 점수, 작성일, 내용)**  
    **슈퍼키**: (아이디, ISBN), (아이디, ISBN, 점수/작성일/내용), (아이디, ISBN, 점수, 작성일/내용), (아이디, ISBN, 작성일, 내용), (아이디, ISBN, 점수, 작성일, 내용)  
    **후보키**: (아이디, ISBN)  
    **기본키**: (아이디, ISBN)  
    **외래키**: 아이디, ISBN  

+ **구매(<ins>아이디</ins>, <ins>ISBN</ins>, <ins>구분</ins>, 구매일, 사용포인트, 결제가격)**  
    **슈퍼키**: (아이디, ISBN, 구분), (아이디, ISBN, 구분, 구매일/사용포인트/결제가격), (아이디, ISBN, 구분, 구매일, 사용포인트/결제가격), (아이디, ISBN, 구분, 사용포인트, 결제가격), (아이디, ISBN, 구분, 구매일, 사용포인트, 결제가격)  
    **후보키**: (아이디, ISBN, 구분)  
    **기본키**: (아이디, ISBN, 구분)  
    **외래키**: 아이디, ISBN
***
