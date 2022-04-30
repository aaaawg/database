## 1. 주제
**전자책 서점 관리 시스템**   
구매를 통해 도서 이용이 가능하다.   
구매한 도서 가격의 3%를 포인트로 지급한다.
+ 도서 관리
  + 소장 도서와 대여 도서 구분
  + 소장: 모든 도서 가능, 대여: 일부 도서만 가능
+ 회원 관리
+ 주문 관리
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

+ **주문(<ins>아이디</ins>, <ins>ISBN</ins>, <ins>구분</ins>, 주문일, 사용포인트, 결제가격)**  
    **슈퍼키**: (아이디, ISBN, 구분), (아이디, ISBN, 구분, 주문일/사용포인트/결제가격), (아이디, ISBN, 구분, 주문일, 사용포인트/결제가격), (아이디, ISBN, 구분, 사용포인트, 결제가격), (아이디, ISBN, 구분, 주문일, 사용포인트, 결제가격)  
    **후보키**: (아이디, ISBN, 구분)  
    **기본키**: (아이디, ISBN, 구분)  
    **외래키**: 아이디, ISBN
***
## 4. 테이블 생성
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
