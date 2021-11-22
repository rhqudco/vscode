# SQLday_2 정리 (2021.11.19 금요일)

## 데이터베이스 표준 질의어(SQL)
- 관계영 데이터베이스 시스템(RDBMS)의 데이터베이스, 데이터를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어
- 질의어(Query Language)는 검색 언어라는 의미
- 데이터를 검색하는 역할 외에 데이터 입력, 수정, 삭제, 제어, 복구 등 다양한 기능 제공
- Structured Query Language
- DBMS별로 특화된 SQL사용

## SQL문의 기능별 분류
- 데이터 정의어(DDL)
  - 데이터베이스, 테이블 구조를 생성/수정/삭제하는데 사용
  - CREATE/ALTER/DROP
- 데이터 조작어(DML)
  - 테이블의 데이터를 검색, 삽입, 수정, 삭제하는데 사용
  - 스키마, 테이블, 뷰, 인덱스 정의, 변경, 삭제할 때 사용
  - SELECT/INSERT/UPDATE/DELETE
- 데이터 제어어(DCL)
  - 데이터의 사용 권한 등 관리에 사용
  - GRANT/REVOKE/COMMIT/ROLLBACK

## 데이터 정의어(DDL)
- CREATE : 데이터베이스, 테이블 등 객체 생성
- ALTER : 기존에 존재하는 데이터베이스 객체 변경
- DROP : 데이터베이스 등 객체 삭제

## 데이터 조작어(DML)
- 고급 프로그래밍 언어로 작성된 응용프로그램에 내포되어 사용
- SELECT : 데이터 검색
- INSERT : 데이터 입력
- UPDATE : 데이터 수정
- DELETE : 데이터 삭제

### 데이터 조작어 옵션
- NOT NULL : 빈 값 허용하지 않은
- DEFAULT : 기본값으로 설정
- PRIMARY KEY : 기본키 설정
  - 제약조건
    - 열에 지정
    - 빈 값 안됨
    - (자동으로)중복 안 됨
- FOREIGN KEY : 외래키 설정
- REFERENCES : 외래키가 참조할 테이블 설정
- UNIQUE : 중복값이 없도록 설정
- CHECK : 특정 내용의 제약 조건 설정
- ON DELETE / ON UPDATE 옵션 : 참조되는 테이블의 행 삭제/갱신 시 옵션

## 데이터 제어어(DCL)
- GRANT : 권한 부여
- REVOKE : 권한 취소
- COMMIT : 변경된 내용을 영구적으로 DB에 반영
- ROLLBACK : 변경된 내용을 취소하고 DB를 이전 상태로 되돌림

## CREATE(테이블 생성)
- 테이블 생성
- 속성(열)과 속성에 관한 제약 정의
- 기본키와 외래키 정의

### CREATE문의 기본 형식
~~~sql
CREATE TABLE 테이블명(
	열이름 데이터타입(크기) [제약조건 리스트…],
	열이름 ….,
	열이름...
);
~~~

## CREATE문 연습예제

~~~sql
-- 스키마 생성
create schema sqldb1 default character set utf8;

-- 스키마 삭제
-- drop schema sqldb;

-- 테이블 생성
-- create table
-- 속성(열)과 속성에 관한 제약 정의
-- 기본키(PK), 외래키(FK) 정
use sqldb1;

-- 상품 테이블 생성
-- 제약 조건
	-- 기본키 : prdNo NOT NULL
	-- prdName NOT NULL
create table PRODUCT (
	prdNo varchar(10) NOT NULL PRIMARY KEY,
	prdName varchar(30) not null,
	prdPrice int,
	prdCompany varchar(30)
);

-- 상세 정보 출력
describe product3;

-- 기본키 제약 조건 설정 방법 2
create table PRODUCT2 (
	prdNo varchar(10) NOT NULL,
	prdName varchar(30) not null,
	prdPrice int,
	prdCompany varchar(30),
	primary key(prdNo)
);

-- 기본키 제약 조건 설정 방법 3
create table PRODUCT3 (
	prdNo varchar(10) NOT NULL,
	prdName varchar(30) not null,
	prdPrice int,
	prdCompany varchar(30),
	constraint PK_product_prdNo primary key(prdNo)
);

-- 출판사 테이블과 도서 테이블 생성
-- 기본키 / 외래키 제약 조건 설정

/*
출판사 테이블 생성 (출판사 번호, 출판사명)
제약조건 설정
- 기본키로 pubNo NOT NULL
- pubName NOT NULL
*/

-- publisher
-- pubNo 가변문자 10
-- pubName 가변문자 30 
-- 제약조건 설정하고
-- 테이블 생성

create table publisher(
	pubNo varchar(10) not null primary key,
	pubName varchar(30) not null
);

-- 도서 테이블 생성
-- 외래키(출판사 번호 pubNO) 제약조건 설정
-- 기타 제약조건 설정
	-- 기본키 : bookNo not null
    -- 외래키 : pubNo (참조 테이블의 기본키와 동일 -> varchar(10) not null)
    -- bookPirce : 기본값 10000, 1000보다 큰 값만 들어갈 수 있게 설정 
create table book(
bookNo varchar(10) not null primary key,
bookName varchar(30) not null,
bookPrice int default 10000 check(bookPrice>1000),
bookData date,
pubNo varchar(10) not null,
constraint FK_book_publisher foreign key(pubNo) references publisher(pubNo)
);
-- constraint 제약조건 이름 foreign key(외래키로 사용하는 열이름) references 참조하는 테이블명(참조하는 테이블의 기본키)
describe book;
-- pri : 기본키
-- mul : 중복 가능한 키(외래키)
-- 외래키로 지정된 열에는 동일 값(중복 값) 저장 가능
-- @@ 출판사에서 출간한 도서가 여러 권 가능하기 때문
-- 테이블 생성 순서 주의
-- 외래키로 제약조건을 설정할 경우
-- 테이블 생성 순서
-- 1. publisher(book에서 사용할 외래키가 해당 테이블의 기본키이기 때문에)
-- 2. book(publisher의 기본키를 외래키로 사용하기 때문)

-- 테이블 생성 후 데이터 입력 시 주의
-- publisher의 기본키인 pubNo에 값을 먼저 입력해야 book의 pubNo를 입력할 때 오류가 없다.
-- 즉, 외래키 값을 입력할 때는 참조되는 테이블의 기본키로서의 값과 동일해야 한다(참조 무결성 제약조건)

-- 테이블 삭제 시 주의
-- publisher 먼저 삭제하면 외래키로 사용 중이라는 오류 발생(book에서 pubNo 사용 중 이기 때문)
-- book 테이블 먼저 삭제하고 publisher 삭제
-- 즉, 외래키로 사용 중인 경우 참조되는 테이블(부모 테이블)의 기본키를 삭제할 수 없다(참조 무결성 제약조건 때문)


-- 데이터 입력  publisher
-- 서울 출판사, 도서출판 강남, 정보 출판

-- book 테이블에 데이터 입력
-- 설정된 제약조건
	-- bookName에 NULL 값을 삽입할 수 없음
    -- bookPrice에 1000 이하 값을 입력 시 CHECK 제약조건 충돌 오류 발생
	-- bookPrice에 값을 입력하지 않으면(NULL) 자동으로 기본값인 10000으로 입력됨
    -- 클릭 하지 않은 상태에서 null 글자가 있으면 Null상태
    -- book 테이블의 pubNo입력 시 1,2,3 이외의 값 입력 시 외래키 제약조건 충돌 오류 발생


create table department(
	departmentCode int not null primary key,
	departmentName varchar(30) not null
);

create table student (
	studentNumber varchar(20) not null primary key,
	studentName varchar(30) not null,
    studentGrade int not null default 4 check(studentGrade >= 1 and studentGrade <= 4),
    departmentCode int not null,
    constraint FK_student_department foreign key(departmentCode) references department(departmentCode)
);

/*
테이블 생성 순서
1. 학과 테이블
2. 학생 테이블 : 학과번호를 외래키로 설정
*/
/*연습문제
학생(student)과 학과(department) 테이블 생성하고 데이터 3개씩 입력
제약조건
기본키 설정
필요한 경우 외래키 설정
학생은 학과에 소속
학생 이름과 학과 이름은 NULL 값을 허용하지 않음
학년은 4를 기본값으로, 범위를 1~4로 설정 (AND 키워드 사용)
*/

CREATE TABLE department2(
	 dptNo VARCHAR(10) NOT NULL PRIMARY KEY,
     dptName VARCHAR(30) NOT NULL,
     dptTel VARCHAR(13)
);

CREATE TABLE student2(
	stdNo VARCHAR(10) NOT NULL PRIMARY KEY,
    stdName VARCHAR(30) NOT NULL,
    stdYear INT DEFAULT 4 CHECK(stdYear >=1 AND stdYear <= 4),
    stdAddress VARCHAR(50),
    stdBirthday DATE,
    dptNo VARCHAR(10) NOT NULL,
    CONSTRAINT FK_student2_department2 FOREIGN KEY (dptNo) REFERENCES department2(dptNo)
);

/*
교수 테이블
교수번호 : 기본키, NOT NULL 
학과코드 : 외래키 설정
과목
과목코드 : 기본키, NOT NULL
교수번호 : 외래키 설정
성적
학번과 과목코드 2개로 기본키 설정
학번 : 외래키 설정
과목코드 : 외래키 설정

*/

create table professor(
	proId varchar(10) not null primary key,
	proName varchar(30) not null,
	proPosition varchar(20) not null,
	proTel varchar(13),
	dptNo varchar(10) not null,
	constraint FK_professor_department2 foreign key (dptNo) references department2(dptNo)
);
create table subjects(
	subId varchar(10) not null primary key,
    subName varchar(20) not null,
    subCredit int,
    proId varchar(10) not null,
    constraint FK_subjects_professor foreign key (proId) references professor(proId)
);
create table scores(
	stdNo varchar(10) not null,
    subId varchar(10) not null,
    scSc int,
    scGrade varchar(2), 
    constraint PK_scores_stdNo_subId primary key(stdNo, subId),
    constraint FK_scores_student2 foreign key (stdNo) references student2(stdNo),
    constraint FK_scores_subjects foreign key (subId) references subjects(subId)
);

/*
실습
1. 1부터 1씩 증가
2. 초기값 100으로 설정하고 3씩 증가
3. 다시 1부터 1씩 증가하도록 변경
4. 중간에 있는 값 삭제하고 전체를 다시 1부터 1씩 증가하도록 재정
*/
-- 1번
create table board(
	boardNo int auto_increment not null primary key,
    boardTitle varchar(30) not null,
    boardWriter varchar(20),
    boardContent varchar(100) not null
    );
-- 2번
create table board2(
	boardNo int auto_increment not null primary key,
    boardTitle varchar(30) not null,
    boardWriter varchar(20),
    boardContent varchar(100) not null
    );
    alter table board2
    auto_increment = 100;
    set @@auto_increment_increment = 3;
-- 3번
set @count = 0;
update board2 set boardNo = @count:=@count+1;
-- 자바에서 변수값 1 증가 : sum = sum + 1 과 동일한 의미
-- 4번
-- 다시 0으로 설정하고
set @count = 0;
update board2 set boardNo = @count:=@count+1;
-- 초기 값을 1로 다시 설정
alter table board2 auto_increment = 1;
~~~

## AUTO_INCREMENT
- 기본 값 자동 증가
- 속성 값을 자동으로 증가(아무 것도 지정하지 않으면 기본 1부터 시작해서 1씩 증가)
  - AUTO_INCREMENT = 100
    - 기본 시작 값을 100으로 설정
  - SET @@AUTO_INCREMENT_INCREMENT = 3
    - 3씩 증가

## ALTER(테이블 수정)
- 테이블에 대한 정의(구조) 변경
- 새로운 열 추가, 특정 열의 디폴트값 변경, 특정 열 삭제 등 수행

### ALTER문의 기본 형식
- ALTER TABLE 테이블명
  - ADD : 열 추가
  - RENAME COLUMN : 열 이름 변경
  - MIDIFY : 열의 데이터 형식 변경
  - CHANGE : 열 이름과 데이터 형식 동시 변경
  - DROP COLUMN : 열 삭제
  - DROP : 여러 개 열 삭제
  - DROP PRIMARY KEY : 기본키 삭제
  - DROP CONSTRAINT : 제약조건 삭제

~~~sql
ALTER TABLE 테이블명 ADD ...
~~~

## TABLE 제약조건 이름 확인

~~~sql
-- 모든 제약조건 출력
select * from information_schema.table_constraints;

-- 특정 데이터베이스의 특정 테이블 제약조건 출력
select * from information_schema.table_constraints 
where table_schema = DB이름 and table_name = "테이블 이름";

-- 특정 테이블의 제약조건 출력 (이것만 사용해도 알 수 있다.)
select * from information_schema.table_constraints 
where table_name = "테이블 이름";
~~~

## ALTER문 연습예제
~~~sql
use sqldb1;

-- steTel 추가
ALTER TABLE student2 ADD steTel varchar(13);

describe student2;

-- 여러 개의 열(stdAge, stdAddress)추가 
alter table student2 add (stdAge varchar(2), stdAddress2 varchar(50));

-- 열의 데이터 형식 변경 : stdAge 열의 데이터 타입을 INT로 바꾼다.
alter table student2 modify stdAge int;

-- 열의 제약조건 변경 : stdName을 NULL 허용으로 설정
alter table student2 modify stdname varchar(2) null;

-- 열 이름 변경 : stdTel을 stdHP로 변경(데이터 타입 적으면 구문 오류)
alter table student2 rename column stdTel to stdHP;

-- 열 이름과 데이터 타입 변경
alter table student2 change stdAddress stdAddress1 varchar(30);

-- 열 삭제 : stdHP 삭제
alter table student2 drop column stdHP;

-- 여러 개의 열 삭제
alter table student2 drop stdAge,
					 drop stdAddress1,
					 drop stdAddress2;
                     
-- alter table 연습문제
/*
테이블 ALTER 연습문제
1. product 테이블에 숫자 값을 갖는 prdStock과 제조일을 나타내는 prdDate 열 추가
2. product 테이블의 prdCompany 열을 NOT NULL로 변경
3. publisher 테이블에 pubPhone, pubAddress 열 추가
4. publisher 테이블에서 pubPhone 열 삭제
*/
alter table product add (prdStock int, prdDate date);
alter table product modify prdCompany varchar(30) not null;
alter table publisher add (pubPhone varchar(13), pubAddress varchar(30));
alter table publisher drop column pubPhone;

-- 기본키 삭제
alter table department2 drop primary key; 
/*해당 sql구문은 오류 외래키 제약조건이 설정됐기 때문*/

-- 외래키 제약조건 삭제
alter table student2 drop constraint FK_student2_department2;
alter table professor drop constraint FK_professor_department2;

-- 외래키 제약조건 삭제 후 기본키 삭제
alter table department2 drop primary key;

-- 기본키 / 외래키 추가

-- 기본키 제약조건 추가 : department2 테이블
-- 둘 다 가능한 구문
alter table department2 add constraint PK_department2_dptNo primary key(dptNo);
alter table department2 add primary key(dptNo);

-- 외래키 제약조건 추가 : student2와 professor 테이블
alter table student2 
add constraint FK_student2_department2 
foreign key(dptNo) references department2(dptNo);

alter table professor 
add constraint FK_professor_department2 
foreign key(dptNo) references department2(dptNo);

-- ON DELETE CASCADE
-- student2 테이블의 기존 외래키 삭제하고 다시 설정
-- 기존 외래키 삭제
alter table student2 drop constraint FK_student2_department2;
-- ON DELETE CASCADE로 다시 외래키 설정
-- department2 table에서 값이 지워지면 자동으로 student2 table의 외래키가 지워진다.
alter table student2 add constraint FK_student2_department2
foreign key(dptNo) references department2(dptNo)
ON DELETE CASCADE;
~~~

## ON DELETE CASCADE
- 기준 테이블의 데이터가 삭제됐을 때 외래키로 사용하는 테이블의 데이터도 자동으로 삭제되도록 설정
  - department 테이블의  dptNo 값 2가 삭제되었을 때 student 테이블에서 dptNo 값을 2로 갖고 있는 레코드(행)도 자동 삭제

## DROP(테이블 삭제)
- 스키마, 테이블, 뷰, 인덱스 등 삭제하는 명령문
- 테이블 구조와 데이터 모두 삭제
  - 데이터만 삭제하려면 DELETE문 사용(DML)

### DROP문의 기본 형식
- DROP TABLE 테이블명

~~~sql
DROP TABLE book;
DROP TABLE publisher;
~~~