# SQLday_3 정리 (2021.11.22 월요일)

## 데이터 조작어(DML)
- 데이터 입력/수정/삭제/검색
- INSERT
- UPDATE
- DELETE
- SELECT

## INSERT 문
- 테이블에 새로운 행을 삽입하는 명령어
- 기본 형식 : INSERT INTO 테이블명(열이름 리스트) VALUES(값리스트);
  - 예 : INSERT INTO student (stdNo, stdName, stdYear, dptNo) VALUES('20201111', "ghdrlfehd", 4, '3');
    - 숫자는 따옴표 필요 없음.

## 데이터 임포트
- csv 파일 통해 테이블 생성 및 데이터 입력
- 스키마 -> 우클릭 -> table data import wizard
- 파일 임포트를 하면 제약조건이 사라지기 때문에 다시 추가해야 한다.
- 문자 타입을 전부 text로 읽기 때문에 자료형을 변경해야 한다.
  - text to varchar() 등으로 변경

#### DML_insert & update 연습

~~~sql
use sqldb2;

create table publisher(
	pubNo varchar(10) not null primary key,
	pubName varchar(30) not null
);

create table book(
bookNo varchar(10) not null primary key,
bookName varchar(30) not null,
bookPrice int default 10000 check(bookPrice>1000),
bookDate date,
pubNo varchar(10) not null,
constraint FK_book_publisher foreign key(pubNo) references publisher(pubNo)
);

-- publisher 테이블에 데이터 입력
-- INSERT INTO 테이블명(열이름 리스트) VALUES(값리스트);
insert into publisher (pubNo, pubName) values('1', '서울 출판사');
insert into publisher (pubNo, pubName) values('2', '강남 출판사');
insert into publisher (pubNo, pubName) values('3', '종로 출판사');

-- publisher 테이블 내용 조회
select * from publisher;

-- book 테이블에 데이터 입력
insert into book(bookNo, bookName, bookPrice, bookDate, pubNo)
values('1','자바',20000,'2021-05-17','1');
-- 모든 열에 데이터를 입력할 경우 열이름 생략 가능
insert into book values('2','자바스크립트',23000,'2019-05-17','3');

select * from book;

-- 여러 개의 데이터 한 번에 insert

insert into book(bookNo, bookName, bookPrice, bookDate, pubNo)
values	('3','데이터베이스',35000,'2021-05-18','2'),
		('4','알고리즘',18000,'2021-05-19','3'),
		('5','웹프로그래밍',22000,'2021-05-20','2');
        
-- 여러 개의 데이터 한 번에 insert

insert into book
values	('6','데이터베이스',35000,'2021-05-18','2'),
		('7','알고리즘',18000,'2021-05-19','3'),
		('8','웹프로그래밍',22000,'2021-05-20','2');
	
/*
연습문제
INSERT 문을 사용하여
학과 / 학생 테이블에 다음과 같이 데이터 입력
SELECT 문으로 조회
*/

 -- 학과 테이블 생성
    CREATE TABLE department(
        dptNo VARCHAR(10) NOT NULL PRIMARY KEY,
        dptName VARCHAR(30) NOT NULL,
        dptTel VARCHAR(13)
    );

  -- 학생 테이블 생성 
	CREATE TABLE student (
		stdNo VARCHAR(10) NOT NULL PRIMARY KEY,
		stdName VARCHAR(30) NOT NULL,
		stdYear INT DEFAULT 4 CHECK(stdYear >= 1 AND stdYear <= 4),
        stdAddress VARCHAR(50), 
		stdBirthDay DATE,
		dptNo VARCHAR(10) NOT NULL,
        CONSTRAINT FK_student_department FOREIGN KEY (dptNo) REFERENCES department (dptNo)
	);

insert into department 
values('1', '컴퓨터학과', '02-1111-1111'),
('2','경영학과','02-2222-2222'),
('3','수학과','02-7777-7777');

insert into student
values	('2018002','이몽룡',4,'서울시 강남구','1998-05-07','1'),
		('2019003','홍길동',3,'경기도 안양시','1999-11-11','2'),
        ('2021003','성춘향',1,'전라북도 남원시','2002-01-02','3'),
        ('2021004','변학도',1,'서울시 종로구','2000-11-11','2');
        
select * from department;
select * from student;

ALTER TABLE product MODIFY prdNo VARCHAR(10) NOT NULL;
    
-- 기본키 제약조건 추가
ALTER TABLE product
	ADD CONSTRAINT PK_product_prdNo
	PRIMARY KEY (prdNo);
    
-- 모든 text 타입을 VARCHAR 타입으로 변경
ALTER TABLE product MODIFY prdName VARCHAR(20),
					MODIFY prdMaker VARCHAR(30),
					MODIFY prdColor VARCHAR(10),
					MODIFY ctgNo VARCHAR(10);
                    
/*
    UPDATE 문 (데이터 수정)
	특정 열의 값을 수정하는 명령어 
	조건에 맞는 행을 찾아서 열의 값을 수정
	기본 형식 : UPDATE 테이블명 SET 열이름=새값 WHERE 조건;
	예: 상품번호가 5인 행의 상품명을 ‘UHD TV’로 수정
	UPDATE product SET prdName = ‘UHT TV’ WHERE prdNo=’5’;
*/

--  상품 테이블 내용 조회
SELECT * FROM product;


-- 상품번호가 1005인 상품의 상품명을 ‘UHD TV’로 변경
UPDATE product SET prdName = 'UHD TV' WHERE prdNo='1005';

/*
    DELETE 문 (데이터 삭제)
	테이블에 있는 기존 행을 삭제하는 명령어
	기본 형식 : DELETE FROM 테이블명 WHERE 조건;
	예: DELETE FROM product WHERE prdName = ‘그늘막 텐트’;
	테이블의 모든 행 삭제
	DELETE FROM product;
*/

-- 상품명이 '그늘막 텐트'인 상품 삭제alter  
DELETE FROM product WHERE prdName = '그늘막 텐트';    
    
--  상품 테이블 내용 조회
SELECT * FROM product;

/*
연습문제
1. book 테이블에 다음과 같이 행 삽입 
 (출판사 데이터는 테이블 구조에 맞게 입력) - 9번 10번으로 입력
		강남 출판사
2. book 테이블에서 도서명이 '자바'인 행의 가격을 22000으로 변경
3. book 테이블에서 발행일이 2018년도인 행 삭제  
*/
select * from book;
insert into book 
values	('9','JAVA 프로그래밍',30000,'2021-03-10','1'),
		('10','알고리즘',18000,'2021-05-19','2');
        
update book set bookPrice=22000 where bookName = '자바';
DELETE FROM book 
	WHERE bookDate >= '2018-01-01' AND bookDate <= '2018-12-31';
    

/*
	다음과 같이 SQL 문 작성
	1. 고객 테이블 (customer) 생성 
	2. 고객 테이블의 전화번호 열을 NOT NULL로 변경
	3. 고객 테이블에 ‘성별’, ‘나이’ 열 추가
	4. 고객 테이블에 데이터 삽입 (3개)
	5. 고객명이 홍길동인 고객의 전화번호 값 수정 (값은 임의로)
	6. 나이가 20살 미만인 고객 삭제
*/
	-- 1. 고객 테이블 (customer) 생성  
	CREATE TABLE customer(
		custNo VARCHAR(10) NOT NULL PRIMARY KEY,
		custName VARCHAR(30),
		custPhone VARCHAR(13),
		custAddress VARCHAR(50)
	);
-- 2번
alter table customer modify custPhone varchar(13) not null;
DESCRIBE customer;
-- 3번
alter table customer add (custGendet varchar(10), custAge int);
DESCRIBE customer;
-- 4번
insert into customer
			values('1001', '홍길동', '02-1111-1111', '서울특별시 강남구', '남성', 21),
				('1002', '김병지', '02-2222-2222', '서울특별시 마포구', '남성', 22),
				('1003', '강호동', '02-3333-3333', '서울특별시 은평구', '남성', 23);
SELECT * FROM customer;
-- 5번
update customer set custPhone='010-1231-1233' where custName='홍길동';
SELECT * FROM customer;
-- 6번
delete from customer where custAge < 22;
SELECT * FROM customer;
~~~

## SELECT 문
- 테이블에서 조건에 맞는 행 검색 (반환)

~~~sql
기본 형식 : SELECT 열이름 리스트 FROM 테이블명
			[WHERE 검색조건]
			[GROUP BY 열이름] 
			[HAVING 조건]
			[ORDER BY  열이름 [ASC | DESC];
~~~

- 추가 옵션 순서
  - where
  - group by
  - having
  - order by

- select 열이름 : 검색할 열 기술
- from 테이블명 : 데이터를 검색할 테이블명 기술
- where 조건 : 질의 결과에 포함될 행들이 만족해야 할 조건 기술
- order by 열이름 : 특정 열의 값을 기준으로 질의 결과 정렬
  - asc : 오름차순
  - desc : 내림차순
- group by 열이름 : 그룹 질의를 기술할 때 사용, 특정 열로 그룹화한 후 각 그룹에 대해 한 행씩 질의 결과 생성
- having 조건 : group by 절에 의해 구성된 그룹들에 대해 적용할 조건 기술 

## WHERE절 조건
- 비교
  - =, <, >, <=, >=, !=
  - 값의 크기를 비교하여 질의 검색
  - price >= 100000
- 범위
  - BETWEEN
  - 검사 값이 기술된 두 값 사이에 속하는지 검사하여 질의 처리
  - price BETWEEN 10000 AND 20000
- 리스트에 포함
  - IN, NOT IN
  - 검사 값이 주어진 값의 리스트에 속하는지 여부를 검사
  - price IN(100000,200000,300000)
- NULL
  - IS NULL, IS NOT NULL
  - price IS NULL
- 논리
  - AND, OR
  - 단순 탐색 조건을 결합하여 질의 처리
  - (price <= 10000) and (name LIKE '김%')
- 패턴 매칭 문자열 검색
  - LIKE
  - 문자열의 일부가 일치하는 데이터 검색
  - prdName LIKE '%프린터%'
    - '홍%' : '홍'으로 시작하는 문지열 검색
    - '%길%' : '길'을 포함하는 문자열('길' 앞, 뒤에 아무 문자나 와도 됨)
    - '%동' : '동'으로 끝나는 문자열
    - '____' : 4개의 문자로 구성된 문자열(언더바(_) 하나가 1개 문자)
      - % : 0개 이상의 문자를 가진 문자열
      - _ : 단일 문자(_의 수 만큼 문자로 구성된다.)
  - NOT LIKE
  - 문자열의 일부가 일치하지 않는 데이터 검색

#### DML_where 연습

~~~sql
use sqldb3;

-- publisher 테이블 변경
-- 기본키 제약 조건 추가하기 전에 text 타입을 VARCHAR(10)으로 변경
-- 변경하지 않으면 text 길이가 앖다는 오류 발생    
alter table publisher modify pubNo varchar(10) not null;
alter table publisher modify pubName varchar(20);
-- 기본키 제약 조건 추가 
alter table publisher add constraint PK_publisher_pubNo primary key (pubNo);
describe publisher;

-- book 테이블 변경
    -- 기본키 제약 조건 추가하기 전에 text 타입을 VARCHAR(10)으로 변경
    -- 변경하지 않으면 text 길이가 앖다는 오류 발생
    
ALTER TABLE book MODIFY  bookNo VARCHAR(10) NOT NULL, 
				MODIFY bookName VARCHAR(20),
				MODIFY bookAuthor VARCHAR(30),
				MODIFY bookDate DATE,
				MODIFY  pubNo VARCHAR(10) NOT NULL; -- 외래키 pubNo  


 -- 기본키 제약 조건 추가    
ALTER TABLE book 
		ADD CONSTRAINT PK_book_bookNo 
		PRIMARY KEY (bookNo);
    
-- 외래키 제약 조건 추가
ALTER TABLE book 
		ADD CONSTRAINT FK_book_publisher 
		FOREIGN KEY (pubNo) REFERENCES publisher (pubNo);
            
DESCRIBE book;
SELECT * FROM book;
           


-- client 테이블 변경
-- 기본키 제약 조건 추가하기 전에 text 타입을 VARCHAR(10)으로 변경
-- 변경하지 않으면 text 길이가 앖다는 오류 발생    
ALTER TABLE client MODIFY clientNo VARCHAR(10) NOT NULL, 
				   MODIFY clientName VARCHAR(30),
				   MODIFY clientPhone VARCHAR(13),
				   MODIFY clientAddress VARCHAR(50),
				   MODIFY clientBirth DATE,
				   MODIFY clientHobby VARCHAR(30),
				   MODIFY clientGender VARCHAR(1); 

-- 기본키 제약 조건 추가    
ALTER TABLE client 
		ADD CONSTRAINT PK_client_clientNo 
		PRIMARY KEY (clientNo);         

DESCRIBE client;
SELECT * FROM client;


-- bookSale 테이블 변경 
ALTER TABLE bookSale MODIFY bsNo VARCHAR(10) NOT NULL, 
					 MODIFY bsDate DATE,
					 MODIFY clientNo VARCHAR(10) NOT NULL, -- clientNo 외래키
					 MODIFY bookNo VARCHAR(10) NOT NULL;  -- bookNo 외래키

-- 기본키 제약 조건 추가    
ALTER TABLE bookSale 
		ADD CONSTRAINT PK_bookSale_bsNo 
		PRIMARY KEY (bsNo);  	

-- 외래키 제약 조건 추가
ALTER TABLE bookSale 
		ADD CONSTRAINT FK_bookSale_book 
		FOREIGN KEY (bookNo) REFERENCES book (bookNo);
		
ALTER TABLE bookSale 
		ADD CONSTRAINT FK_bookSale_client 
		FOREIGN KEY (clientNo) REFERENCES client (clientNo);

DESCRIBE bookSale;
SELECT * FROM bookSale;

-- book 테이블에서 모든 행 검색하여 출력
-- 모든 열(*) 선택
select *  from book;

-- 도서명과 가격만 검색하여 출력
SELECT bookName, bookPrice FROM book;

-- 저자만 검색하여 출력
SELECT bookAuthor FROM book;

-- 저자만 검색하여 출력 (중복되는 행은 한번만 출력)
-- DISTINCT
SELECT DISTINCT bookAuthor FROM book;

-- where 조건 연습
-- 비교
-- 저자가 홍길동인 도서의 도서명, 저자 출력
select bookName, bookAuthor
from book
where bookAuthor = '홍길동';

-- 가격이 30000원 이상인 도서의 도서명, 가격, 재고 출력
select bookName, bookPrice, bookStock
from book
where bookPrice >= 30000;

-- 재고가 3~5개 사이인 도서의 재고명, 재고 출력
select bookName, bookStock
from book
where bookStock >= 3 and bookStock <= 5;

-- 위랑 같은 문제를 between 사용해서 해결
select bookName, bookStock
from book
where bookStock between 3 and 5;

-- 리스트에 포함(in, not in)
-- 출판사명이 '서울 출판사'와 '도서출판 강남'인 도서의 도서명, 출판사 번호 출력
-- publisher 테이블의 출판사 넘버에 따라 달라지기 때문에 publisher 테이블을 알아야 함.
select bookName,bookNo
from book
where pubNo in ('1', '2');

-- 출판사명이 '도서출판 강남'이 아닌 도서의 도서명, 출판사 번호 출력
select bookName, pubNo
from book
where pubNo not in ('2');

-- null(is null, is not null)
-- 고객 테이블에서 취미 열 확인
select * from client;

-- null 실습을 위해 일부러 null로 설정
update client set clientHobby=null where clientName='호날두';
update client set clientHobby=null where clientName='샤라포바';

-- 모든 고객명, 취미 출력
select clientName, clientHobby from client;

-- 취미에 null 값이 들어 있는 행만 출력
select clientName, clientHobby
from client
where clientHobby is null;

-- 취미가 null값이 아닌 행만 출력
select clientName, clientHobby
from client
where clientHobby is not null;

-- 취미에 공백이 들어있는 행만 출력
-- ''나 '     '나 상관없이 출력 가능.
select clientName, clientHobby
from client
where clientHobby ='  ';

-- 논리(and, or)
-- 저자가 '홍길동'이면서 재고가 3권 이상인 모든 도서 출력
select *
from book
where bookAuthor = '홍길동' and bookStock >= 3;

-- 저자가 '홍길동'이거나 '성춘향'인 모든 도서 출력
select *
from book
where bookAuthor = '홍길동' or bookAuthor = '성춘향';

-- like 연습 문제
-- 출판사 테이블에서 출판사명에 '출판사'가 포함된 모든 행 출력
select *
from publisher
where pubName like '%출판사%';

-- 고객 중 출생년도가 1990년대인 모든 고객 출력
select clientName, clientBirth
from client
where clientBirth like '199%';

-- 고객 테이블에서 고객명이 4글자인 모든 고객 정보
select *
from client
where clientName like '____';

-- 도서 테이블에서 도서명에 '안드로이드'가 들어 있지 않는 도서의 도서명 출력
select bookName
from book
where bookName not like '%안드로이드%';

/*
연습문제
1. 고객 테이블에서 고객명, 생년월일, 성별 출력
2. 고객 테이블에서 주소만 검색하여 출력 (중복되는 주소는 한번만 출력)
3. 고객 테이블에서 취미가 '축구'이거나 '등산'인 고객의 고객명, 취미 출력
4. 도서 테이블에서 저자의 두 번째 위치에 '길'이 들어 있는 저자명 출력 (중복되는 저자명은 한번만 출력)
5. 도서 테이블에서 발행일이 2019년인 도서의 도서명, 저자, 발행일 출력
6. 도서판매 테이블에서 고객번호1, 2를 제외한 모든 판매 데이터 출력
7. 고객 테이블에서 취미가 NULL이 아니면서 주소가 '서울'인 고객의 고객명, 주소, 취미 출력
8. 도서 테이블에서 가격이 25,000원 이상이면서 저자 이름에 '길동'이 들어가는 도서의 도서명, 저자, 가격, 재고 출력
9. 도서 테이블에서 가격이 20,000 ~ 25,000원인 모든 도서 출력 
10. 도서 테이블에서 저자명에 '길동'이 들어 있지 않는 도서의 도서명, 저자 출력
*/
-- no.1
select clientName, clientBirth, clientGender
from client
-- no.2
select distinct clientAddress
from client;
-- no.3
select clientName, clientHobby
from client
where clientHobby = '축구' or clientHobby = '등산';
-- no.4
select distinct bookAuthor
from book
where bookAuthor like '_길%';
-- no.5
select bookName, bookAuthor, bookDate
from book
where bookDate like '2019%';
-- no.6
select *
from booksale
where clientNo not in(1,2);
-- no.7
select clientName,clientAddress,clientHobby
from client
where clientHobby is not null and clientAddress like '%서울%';
-- no.8
select bookName,bookAuthor,bookPrice,bookStock
from book
where bookPrice >= 25000 and bookAuthor like '%길동%';
-- no.9
select *
from book
where bookPrice between 20000 and 25000;
-- no.10
select bookName,bookAuthor
from book
where bookAuthor not like '%길동%';
~~~

## ORDER BY 조건
- 특정 열의 값을 기준으로 쿼리 결과 정렬
- ASC : 오름차순(생략 가능)
- DESC : 내림차순
- 상위 n개 출력
  - LIMIT N
    - Ex) LIMIT 5
  - 또는 OFFSET 0 설정(OFFSET : 시작 위치) - 첫 번째부터 시작한다.
    - Ex) LIMIT 5 OFFSET 0
  - 또는 LIMIT 시작, 개수
    - Ex) LIMIT 0, 5 : 첫 번째부터 5개
    - Ex) LIMIT 10, 5 : 11번째부터 5개

#### ORDER BY 조건 연습

~~~sql
-- 도서명 순으로 도서 검색 (기본 : 오름차순 (일반적으로 ASC 생략))
select *
from book
order by bookName asc;


-- 일반적으로 asc 생략
select *
from book
order by bookname;

-- 도서명 순으로 도서 검색 (내림차순 DESC)
select *
from book
order by bookname desc;

-- 한글 -> 영문 -> 숫자 순서로
select * 
from book
order by
(case when ascii(substring(bookName, 1)) between 48 and 57 then 3
	  when ascii(substring(bookName, 1)) < 122 then 2 else 1 end), bookName;
-- 영어 -> 한글 -> 숫자 순서로
select * 
from book
order by
(case when ascii(substring(bookName, 1)) between 48 and 57 then 3
	  when ascii(substring(bookName, 1)) < 122 then 1 else 2 end), bookName;
      
/*
LIMIT 활용 예제
*/

-- 상위 n개 출력
-- 첫번째부터 상위 5개
select *
from book
order by bookname
limit 5;
-- 위랑 같음.
select *
from book
order by bookname
limit 5 offset 5;
-- 위랑 같음.
select *
from book
order by bookname
limit 0, 5;

-- 11번째부터 상위 7개
select *
from book
order by bookname
limit 10, 7;
-- 11번째부터 상위 5개
select *
from book
limit 10, 5;
~~~

### 집계 함수
- SUM() : 합계
- AVG() : 평균
- COUNT() : 선택된 열 행 수 (널 값은 제외)
- COUNT(*) : 모든 열을 대상으로 전체 행 수
- MAX() : 최대
- MIN() : 최소

### 집계 함수 연습

~~~sql
-- 정렬

-- SUM
-- 도서 테이블에서 재고 수량 기준 내림차순으로 도서명, 저자, 재고 출력
select bookName, bookAuthor, bookStock
from book
order by bookStock desc;

-- 2차 정렬 (2차 정렬시에도 생략가능)
-- 상위 문제에서 재고 수량이 동일할 때 저자명으로 오름차순 정렬
select bookName, bookAuthor, bookStock
from book
order by bookStock desc, bookAuthor asc;

-- 집계 함수
-- 도서 테이블에서 총 재고 수량 계산하여 출력
select sum(bookStock) -- <- 열 이름으로 함수 코드를 통한 출력.
from book;

-- 열 이름 sym of bookstock 총 재고수량 계산하여 출력
select sum(bookstock) as 'sum of bookStock'
from book;
-- 열 이름으로 한글도 가능, 큰 따옴표도 사용 가능.
select sum(bookstock) as "책 재고"
from book;
-- 열 이름에 공백 없으면 따옴표 필요 없음.
select sum(bookstock) as 책재고
from book;

-- 도서판매 테이블에서 고객번호 2가 주문한 도서의 총 주문 수량 계산하여 출력
select sum(bsQty) as '2번의 총 주문 수량'
from bookSale
where clientNo = '2';

-- MIN MAX
-- 도서 판매 테이블에서 최대/최소 주문수량
select max(bsQty) as 최대, min(bsQty) as 최소
from booksale

-- 도서 테이블에서 도서의 가격 총합, 평균가, 최고가, 최저가 출력
select sum(bookPrice) as 총합, 
	   avg(bookPrice) as 평균, 
	   max(bookPrice) as 최대, 
       min(bookPrice) as 최소
from book;
-- as 생략 가능
select sum(bookPrice) 총합, 
	   avg(bookPrice) 평균, 
	   max(bookPrice) 최대, 
       min(bookPrice) 최소
from book;
-- 형변환(평균가 정수로)
-- ROUND(숫자) : 반올림
-- ROUND(솟자, 소수이하 자리수) : 소수점 이하 자리수
select sum(bookPrice) as 총합, 
	   round(avg(bookPrice)) as 평균, 
	   max(bookPrice) as 최대, 
       min(bookPrice) as 최소
from book;

-- COUNT(*) 전체 행 출력
-- 도서 판매 테이블에서 도서 판매 건수 출력(모든 행의 수가 출력된다)
select count(*) as '총 판매 개수'
from bookSale;
-- COUNT(열이름)
-- 고객 테이블에서 전체 고객 수 (모든 행의 수 출력)
select count(*) as '총 고객 수'
from client;
-- null이 있는 행의 개수 출력
-- null은 함수에서 제외된다.
select count(clientHobby) as '총 취미 개수'
from client;
-- 안에 값이 공백인 경우 공백을 빼고 출력 (null과 공백 모두 제거)
select count(clientHobby) as '총 취미 개수'
from client
where clientHobby not in('');
-- 또는 결과가 동일한 다른 방법
select count(clientHobby) as '총 취미 개수'
from client
where clientHobby != '';
~~~

## GROUP BY
- 그룹 쿼리를 기술할 때 사용
- 특정 열로 그룹화한후 각 그룹에 대해 한 행씩 쿼리 결과 생성

~~~sql
-- group by절 연습
-- 도서 판매 테이블에서 도서별 판매수량 합계 출력
select bookNo, sum(bsQty) as '판매량 합계'
from bookSale
group by bookNo;
-- group by절에서 정렬 - 열 이름으로 정렬
select bookNo, sum(bsQty) as '판매량 합계'
from bookSale
group by bookNo
order by bookNo;
-- 열 순서로 정렬 가능
select bookNo, sum(bsQty) as '판매량 합계'
from bookSale
group by bookNo
order by 1; -- 첫 번째 열(bookNo)로 정렬

select bookNo, sum(bsQty) as '판매량 합계'
from bookSale
group by bookNo
order by 2; -- 두 번째 열(판매량 합계)로 정렬

select bookNo, sum(bsQty) as '판매량 합계'
from bookSale
group by bookNo
order by '판매량 합계'; -- 두 번째 열(판매량 합계)로 정렬 <- 불가능 정렬이 되지 않는다
-- 해결방법
select bookNo, sum(bsQty) as 판매량합계
from bookSale
group by bookNo
order by 판매량합계; -- 열 이름에 따옴표, 공백을 쓰지 않으면 정렬할 수 있다.
~~~

## HAVING
- having 조건
- group by 절에 의해 구성된 그룹들에 대해 적용할 조건 기술
- 집계함수(sum, max, min, 등)와 함께 사용한다.
- 반드시 group by와 사용 해야 하고 where절보다 뒤에 사용 해야 하며, 검색 조건에 집계함수가 와야한다.

#### having절 연습

~~~sql
-- having 연습
-- 도서 테이블에서 가격이 25000원인 도서에 대하여 출판사별로 도서 수 합계(출판사별 = group by)
-- 단 도서 수 합계가 2인 이상만 출력
select pubNo, count(*) as '도서 수 합계'
from book
where bookPrice >= 25000
group by pubNo
having count(*) >= 2;
-- 1번 출판사는 2권 2번 출판사는 6권 나옴

-- having절 빼고 출력
select pubNo, count(*) as '도서 수 합계'
from book
where bookPrice >= 25000
group by pubNo;
-- 1번 출판사는 2권, 2번 출판사는 6권, 3번 출판사는 1권 나옴
~~~

## SELECT문 종합 예제 문제

~~~sql
/*
연습문제
1. 도서 테이블에서 가격 순으로 내림차순 정렬하여,  도서명, 저자, 가격 출력 (가격이 같으면 저자 순으로 오름차순 정렬)
2. 도서 테이블에서 저자에 '길동'이 들어가는 도서의 총 재고 수량 계산하여 출력
3. 도서 테이블에서 ‘서울 출판사' 도서 중 최고가와 최저가 출력 
4. 도서 테이블에서 출판사별로 총 재고수량과 평균 재고 수량 계산하여 출력 (‘총 재고 수량’으로 내림차순 정렬)
5. 도서판매 테이블에서 고객별로 ‘총 주문 수량’과 ‘총 주문 건수’ 출력. 단 주문 건수가 2이상인 고객만 해당  
*/
-- no.1
select bookName, bookAuthor, bookPrice
from book
order by bookPrice desc, bookAuthor asc;
-- no.2
select sum(bookStock) as '총 재고 수량'
from book
where bookAuthor like '%길동%';
-- no.3
select max(bookPrice) as 최고가, min(bookPrice) as 최저가
from book
where pubNo ='1';
-- no.4
-- round 대신 ceil 사용하면 올림, floor 사용하면 내림
select pubNo, sum(bookStock) as '총 재고수량', round(avg(bookStock)) as '평균 재고수량'
from book
group by pubNo
order by 2 desc; -- 따옴표 있으면 order by에 정렬 불가능.
-- no.5
select clientNo, sum(bsQty) as '총 주문 수량', count(clientNo) as '총 주문 건수'
from bookSale
group by clientNo
having count(*) >= 2;
~~~