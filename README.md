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
+ 오디오북 관리
+ 이용권 관리
+ 문의글 관리
    
## 1.1. 요구 사항 명세서
1. YBook의 회원으로 가입하기 위해서는 아이디, 비밀번호, 이름, 나이를 입력해야 한다.
2. 회원은 아이디로 식별한다.
3. YBook의 관리자에 대한 이름, 사원번호, 비밀번호 정보를 저장한다.
4. 관리자는 사원번호로 식별한다.
5. 도서에 대한 ISBN, 구분, 도서명, 출판사, 출간일, 저자, 가격, 할인율 정보를 저장해야 하며 판매가격은 가격과 할인율로 결정된다.
6. 도서는 ISBN으로 식별한다.
7. 도서의 구분에는 대여와 소장이 있으며 대여, 소장 둘 다 해당할 수 있다.
8. 회원은 여러 도서를 주문할 수 있으며 하나의 도서를 여러 회원이 주문할 수 있다.
9. 대여한 도서는 주문일로부터 50일 동안 이용할 수 있다.
10. 회원이 도서를 주문하면 구분, 주문일, 사용포인트, 결제가격 정보를 저장하며 구분이 대여인 경우 만료일은 주문일+50일로 결정된다.
11. 이미 구매한 도서는 여러 번 주문할 수 없으며 대여로 구매했던 도서만 소장으로 다시 주문할 수 있다.
12. 회원이 결제한 가격의 3%를 포인트로 지급한다.
13. 도서 하나에는 하나의 오디오북이 존재할 수 있고 오디오북 하나는 하나의 도서에만 존재해야 한다.
14. 오디오북에 대한 오디오북번호, 낭독자, 재생시간 정보를 유지해야 하며 오디오북번호는 ISBN+회차이다.
15. 오디오북은 오디오북번호로 식별한다.
16. 회원은 여러 도서를 리뷰할 수 있으며 하나의 도서를 여러 회원이 리뷰할 수 있다.
17. 회원이 도서를 리뷰하면 점수, 내용, 작성일 정보를 유지해야 한다.
18. 이용권에 대한 종류, 가격 정보를 유지해야 한다.
19. 회원은 이용권을 주문해야 오디오북을 이용할 수 있는데, 이용권은 여러 회원이 주문할 수 있으며 회원은 이용권 한 개만 주문해야 한다.
20. 회원이 이용권을 주문하면 주문에 대한 주문일이 저장되며 만료일은 주문일과 주문한 이용권의 종류로 결정된다.
21. 문의글에 대한 글번호, 제목, 내용, 작성일, 답변 정보를 저장하며 답변은 내용, 작성일로 나눠서 저장한다.
22. 문의글은 글번호로 식별한다. 
23. 회원은 여러 개의 문의글을 작성할 수 있으며 문의글 하나는 회원 한 명이 작성해야 한다.
24. 문의글 하나는 관리자 한 명이 처리해야 하며 관리자 한 명은 여러 개의 문의글을 처리할 수 있다.

개체 | 속성
:--: | :--:
회원 | 아이디, 비밀번호, 이름, 나이, 포인트
관리자 | 사원번호, 비밀번호, 이름
도서 | ISBN, 구분, 도서명, 출판사, 출간일, 저자, 가격, 할인율, 판매가격
오디오북 | 오디오북번호(ISBN, 회차), 낭독자, 재생시간 
이용권 | 종류, 가격
문의글 | 글번호, 제목, 내용, 작성일, 답변(내용, 작성일)

관계 | 관계에 참여하는 개체 | 관계 유형 | 속성
:--: | :--: | :--: | :--:
주문(도서) | 회원(선택), 도서(선택) | 다대다 | 구분, 주문일, 만료일, 사용포인트, 결제가격
주문(이용권) | 회원(선택), 이용권(필수) | 일대다 | 주문일, 만료일
리뷰 | 회원(선택), 도서(선택) | 다대다 | 점수, 내용, 작성일
존재 | 도서(선택), 오디오북(필수) | 일대일
작성 | 회원(선택), 문의글(필수) | 일대다
처리 | 관리자(선택), 문의글(필수) | 일대다

***
# 2. E-R 다이어그램
![ER](https://github.com/aaaawg/database/blob/main/ER_Diagram.png)

## 2.1. 릴레이션
+ 회원(<ins>아이디</ins>, 비밀번호, 이름, 나이, 포인트, 종류, 주문일) 
+ 관리자(이름, <ins>사원번호</ins>, 비밀번호)
+ 도서(<ins>ISBN</ins>, 도서명, 출판사, 출간일, 가격, 할인율)
+ 도서_구분(<ins>ISBN</ins>, <ins>구분</ins>)
+ 도서_저자(<ins>ISBN</ins>, <ins>저자</ins>)
+ 주문(<ins>아이디</ins>, <ins>ISBN</ins>, <ins>구분</ins>, 주문일, 사용포인트, 결제가격)
+ 리뷰(<ins>아이디</ins>, <ins>ISBN</ins>, 점수, 내용, 작성일)
+ 오디오북(<ins>ISBN</ins>, <ins>회차</ins>, 낭독자, 재생시간)
+ 문의글(<ins>글번호</ins>, 아이디, 제목, 내용, 작성일, 답변_내용, 답변_작성일, 사원번호)

## 2.2. 테이블 명세서
테이블 이름: 회원
필드 이름 | 데이터 타입 | 널 허용 여부 | 키 | 기본값 | 제약조건
:--: | :--: | :--: | :--: | :--: | :--: 
아이디 | VARCHAR(20) | N | PK
비밀번호 | VARCHAR(20) | N 
이름 | VARCHAR(10) | N
나이 | INT | N | | | 0 이상
포인트 | INT | N | | 0 | 0 이상
이용권_종류 | INT | Y | FK
이용권_주문일 | DATE | Y

테이블 이름: 관리자
필드 이름 | 데이터 타입 | 널 허용 여부 | 키 | 기본값 | 제약조건
:--: | :--: | :--: | :--: | :--: | :--: 
사원번호 | INT | N | PK
비밀번호 | VARCHAR(20) | N 
이름 | VARCHAR(10) | N

테이블 이름: 도서
필드 이름 | 데이터 타입 | 널 허용 여부 | 키 | 기본값 | 제약조건
:--: | :--: | :--: | :--: | :--: | :--: 
ISBN | INT | N | PK
도서명 | VARCHAR(20) | N 
출판사 | VARCHAR(10) | N 
출간일 | DATE | N
가격 | INT | N | | | 0 이상
할인율 | INT | N | | 0 | 0 이상

테이블 이름: 도서_구분
필드 이름 | 데이터 타입 | 널 허용 여부 | 키 | 기본값 | 제약조건
:--: | :--: | :--: | :--: | :--: | :--: 
ISBN | INT | N | PK, FK
구분 | CHAR(2) | N | PK 

테이블 이름: 도서_저자
필드 이름 | 데이터 타입 | 널 허용 여부 | 키 | 기본값 | 제약조건
:--: | :--: | :--: | :--: | :--: | :--: 
ISBN | INT | N | PK, FK
저자 | VARCHAR(10) | N | PK

테이블 이름: 주문
필드 이름 | 데이터 타입 | 널 허용 여부 | 키 | 기본값 | 제약조건
:--: | :--: | :--: | :--: | :--: | :--: 
아이디 | VARCHAR(20) | N | PK, FK
ISBN | INT | N | PK, FK
구분 | CHAR(2) | N | PK 
주문일 | DATETIME | N | | CURRENT_TIMESTAMP
사용포인트 | INT | N | | 0 | 0 이상
결제가격 | INT | N | | | 0 이상

테이블 이름: 리뷰
필드 이름 | 데이터 타입 | 널 허용 여부 | 키 | 기본값 | 제약조건
:--: | :--: | :--: | :--: | :--: | :--: 
아이디 | VARCHAR(20) | N | PK, FK
ISBN | INT | N | PK, FK
점수 | DECIMAL(2, 1) | N | | 0 | 0 이상 5 이하 
내용 | VARCHAR(100) | N | | | 30자 이상 
작성일 | DATETIME | N | | CURRENT_TIMESTAMP

테이블 이름: 오디오북
필드 이름 | 데이터 타입 | 널 허용 여부 | 키 | 기본값 | 제약조건
:--: | :--: | :--: | :--: | :--: | :--: 
ISBN | INT | N | PK, FK
회차 | INT | N | PK | | 0 이상
낭독자 | VARCHAR(10) | N 
재생시간 | TIME | N 

테이블 이름: 문의글
필드 이름 | 데이터 타입 | 널 허용 여부 | 키 | 기본값 | 제약조건
:--: | :--: | :--: | :--: | :--: | :--: 
글번호 | INT | N | PK | AUTO_INCREMENT
아이디 | VARCHAR(20) | N | FK
제목 | VARCHAR(50) | N 
내용 | VARCHAR(500) | N 
작성일 | DATETIME | N | | CURRENT_TIMESTAMP
답변_내용 | VARCHAR(500) | Y 
답변_작성일 | DATETIME | Y 
사원번호 | INT | Y | FK

***
# 3. 테이블 생성
데이터베이스 생성
```
CREATE DATABASE YBook;
```

회원 테이블 생성
```
CREATE TABLE 회원 (
	아이디 VARCHAR(20) NOT NULL,
	비밀번호 VARCHAR(20) NOT NULL,
	이름 VARCHAR(10) NOT NULL,
	나이 INT NOT NULL,
	포인트 INT NOT NULL DEFAULT 0,
	이용권_종류 INT,
	이용권_주문일 DATE,
	PRIMARY KEY(아이디)
);
```

관리자 테이블 생성
```
CREATE TABLE 관리자 (
	사원번호 INT NOT NULL,
	비밀번호 VARCHAR(20) NOT NULL,
	이름 VARCHAR(10) NOT NULL,
	PRIMARY KEY(사원번호)
);
```

도서 테이블 생성
```
CREATE TABLE 도서 (
	ISBN INT NOT NULL,
	도서명 VARCHAR(20) NOT NULL,
	출판사 VARCHAR(10) NOT NULL,
	출간일 DATE NOT NULL,
	가격 INT NOT NULL,
	할인율 INT NOT NULL DEFAULT 0,
	PRIMARY KEY(ISBN),
	CHECK (가격 >= 0),
	CHECK (할인율 >= 0)
);
```

도서_구분 테이블 생성
```
CREATE TABLE 도서_구분 (
	ISBN INT NOT NULL,
	구분 CHAR(2) NOT NULL,
	PRIMARY KEY(ISBN, 구분),
    	FOREIGN KEY(ISBN) REFERENCES 도서(ISBN)
    	ON DELETE CASCADE
);
```

도서_저자 테이블 생성
```
CREATE TABLE 도서_저자 (
	ISBN INT NOT NULL,
	저자 VARCHAR(10) NOT NULL,
	PRIMARY KEY(ISBN, 저자),
  FOREIGN KEY(ISBN) REFERENCES 도서(ISBN)
  ON DELETE CASCADE
);
```

주문 테이블 생성
```
CREATE TABLE 주문 (
	아이디 VARCHAR(20) NOT NULL,
	ISBN INT NOT NULL,
	구분 CHAR(2) NOT NULL,
	주문일 DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
	사용포인트 INT NOT NULL DEFAULT 0,
	결제가격 INT NOT NULL,
	PRIMARY KEY(아이디, ISBN, 구분),
	FOREIGN KEY(아이디) REFERENCES 회원(아이디)
	ON DELETE CASCADE,
	FOREIGN KEY(ISBN) REFERENCES 도서(ISBN)
	ON DELETE CASCADE,
	CHECK (사용포인트 >= 0),
	CHECK (결제가격 >= 0)
);
```

리뷰 테이블 생성
```
CREATE TABLE 리뷰 (
	아이디 VARCHAR(20) NOT NULL,
	ISBN INT NOT NULL,
	점수 DECIMAL(2, 1) NOT NULL DEFAULT 0,
	내용 VARCHAR(100) NOT NULL,
	작성일 DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
	PRIMARY KEY(아이디, ISBN),
	FOREIGN KEY(아이디) REFERENCES 회원(아이디)
	ON DELETE CASCADE,
	FOREIGN KEY(ISBN) REFERENCES 도서(ISBN)
	ON DELETE CASCADE,
	CHECK (점수 >= 0 AND 점수 <= 5),
	CHECK (CHAR_LENGTH(내용) >= 30)
);
```

오디오북 테이블 생성
```
CREATE TABLE 오디오북 (
	ISBN INT NOT NULL,
	회차 INT NOT NULL,
	낭독자 VARCHAR(10) NOT NULL,
	재생시간 TIME NOT NULL,
	PRIMARY KEY(ISBN, 회차),
	FOREIGN KEY(ISBN) REFERENCES 도서(ISBN)
	ON DELETE CASCADE
);
```

문의글 테이블 생성
```
CREATE TABLE 문의글 (
	글번호 INT NOT NULL AUTO_INCREMENT,
	아이디 VARCHAR(20) NOT NULL,
	제목 VARCHAR(50) NOT NULL,
	내용 VARCHAR(500) NOT NULL,
	작성일 DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
	답변_내용 VARCHAR(500),
	답변_작성일 DATETIME,
	사원번호 INT,
	PRIMARY KEY(글번호),
	FOREIGN KEY(아이디) REFERENCES 회원(아이디)
	ON DELETE CASCADE,
	FOREIGN KEY(사원번호) REFERENCES 관리자(사원번호)
	ON DELETE SET NULL	
);
```
