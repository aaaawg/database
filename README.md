# 1. 주제
**전자책 서점 관리 시스템 - YBook**   
구매를 통해 도서 이용이 가능하다.   
구매한 도서 가격의 3%를 포인트로 지급한다.
+ 도서 관리
  + 소장 도서와 대여 도서 구분
  + 소장: 모든 도서 가능, 대여: 일부 도서만 가능
+ 회원 관리
+ 주문 관리
+ 리뷰 관리
  + 구매자와 비구매자의 리뷰 구분
    
## 1.1. 요구 사항 명세서
1. YBook의 회원으로 가입하기 위해서는 아이디, 비밀번호, 이름, 나이를 입력해야 한다.    
2. 회원은 아이디로 식별한다.    
3. 도서에 대한 ISBN, 구분, 도서명, 출판사, 출간일, 저자, 가격, 할인율 정보를 유지해야 하며 판매가격은 가격과 할인율로 결정된다.    
4. 도서는 ISBN으로 식별한다.    
5. 도서의 구분에는 대여와 소장이 있으며 대여, 소장 둘 다 해당할 수 있다.    
6. 회원은 여러 도서를 주문할 수 있으며 하나의 도서를 여러 회원이 주문할 수 있다.    
7. 회원이 도서를 주문하면 구분, 주문일, 사용포인트, 결제가격 정보를 유지하며 구분이 대여인 경우 만료일은 주문일+30일로 결정된다.    
8. 이미 구매한 도서는 여러 번 주문할 수 없다.    
9. 대여로 구매했던 도서는 소장으로 주문할 수 있지만 소장으로 구매했던 도서는 대여로 주문할 수 없다.    
10. 대여한 도서는 주문일로부터 30일 동안 이용할 수 있다.    
11. 결제가격의 3%를 포인트로 지급한다.    
12. 회원은 여러 도서를 리뷰할 수 있으며 하나의 도서를 여러 회원이 리뷰할 수 있다.     
13. 회원이 도서를 리뷰하면 평점, 작성일, 내용 정보를 유지해야 한다.    
14. 대여 또는 소장 중인 구매자와 비구매자의 리뷰를 구분한다.    

개체 | 속성
-- | :--:
회원 | 아이디, 비밀번호, 이름, 나이, 포인트
도서 | ISBN, 구분, 도서명, 출판사, 출간일, 저자, 가격, 할인율, 판매가격
***
# 2. E-R 다이어그램
![ER](https://github.com/aaaawg/database/blob/main/ER%20Diagram.png)
***
# 3. 릴레이션
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
    
+ **리뷰(<ins>아이디</ins>, <ins>ISBN</ins>, 평점, 작성일, 내용)**  
    **슈퍼키**: (아이디, ISBN), (아이디, ISBN, 평점/작성일/내용), (아이디, ISBN, 평점, 작성일/내용), (아이디, ISBN, 작성일, 내용), (아이디, ISBN, 평점, 작성일, 내용)  
    **후보키**: (아이디, ISBN)  
    **기본키**: (아이디, ISBN)  
    **외래키**: 아이디, ISBN  

+ **주문(<ins>아이디</ins>, <ins>ISBN</ins>, <ins>구분</ins>, 주문일, 사용포인트, 결제가격)**  
    **슈퍼키**: (아이디, ISBN, 구분), (아이디, ISBN, 구분, 주문일/사용포인트/결제가격), (아이디, ISBN, 구분, 주문일, 사용포인트/결제가격), (아이디, ISBN, 구분, 사용포인트, 결제가격), (아이디, ISBN, 구분, 주문일, 사용포인트, 결제가격)  
    **후보키**: (아이디, ISBN, 구분)  
    **기본키**: (아이디, ISBN, 구분)  
    **외래키**: 아이디, ISBN
***
# 4. 테이블 생성
데이터베이스 생성
```
CREATE DATABASE ebook;
```

고객 테이블 생성
```
CREATE TABLE user (
    id VARCHAR(20) NOT NULL,
    name VARCHAR(5) NOT NULL,
    age INT NOT NULL,
    point INT DEFAULT 0,
    PRIMARY KEY(id)
);
```

도서 테이블 생성
```
CREATE TABLE book (
    isbn INT NOT NULL,
    title VARCHAR(20) NOT NULL,
    publisher VARCHAR(10) NOT NULL,
    publication_date DATE NOT NULL,
    price INT NOT NULL,
    discount INT DEFAULT 0,
    PRIMARY KEY(isbn)
);
```

도서_구분 테이블 생성
```
CREATE TABLE book_category (
    isbn INT NOT NULL,
    category char(2) NOT NULL,
    PRIMARY KEY(isbn, category),
    FOREIGN KEY(isbn) REFERENCES book(isbn)
    ON DELETE CASCADE
);
```

도서_저자 테이블 생성
```
CREATE TABLE book_author (
    isbn INT NOT NULL,
    author varchar(5) NOT NULL,
    PRIMARY KEY(isbn, author),
    FOREIGN KEY(isbn) REFERENCES book(isbn)
    ON DELETE CASCADE
);
```

주문 테이블 생성
```
CREATE TABLE orders (
    user_id VARCHAR(20) NOT NULL,
    book_isbn INT NOT NULL,
    book_category char(2) NOT NULL,
    order_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    use_point INT DEFAULT 0,
    payment INT NOT NULL,
    PRIMARY KEY(user_id, book_isbn, book_category),
    FOREIGN KEY(user_id) REFERENCES user(id)
    ON DELETE CASCADE,
    FOREIGN KEY(book_isbn) REFERENCES book(isbn)
    ON DELETE CASCADE
);
```

리뷰 테이블 생성
```
CREATE TABLE review (
    user_id VARCHAR(20) NOT NULL,
    book_isbn INT NOT NULL,
    rating DECIMAL(2, 1) NOT NULL,
    reg_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    content VARCHAR(100) NOT NULL,
    PRIMARY KEY(user_id, book_isbn),
    CONSTRAINT CHK_R CHECK (rating >= 0 AND rating <= 5),
    CONSTRAINT CHK_C CHECK (CHAR_LENGTH(content) >= 30),
    FOREIGN KEY(user_id) REFERENCES user(id)
    ON DELETE CASCADE,
    FOREIGN KEY(book_isbn) REFERENCES book(isbn)
    ON DELETE CASCADE
);
```
