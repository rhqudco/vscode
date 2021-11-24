# SQLday_5 정리 (2021.11.24 수요일)

## 내장 함수
#### 수학 함수
- ROUND(값, 자리수)
  - 반올림한 값을 구하는 함수
  - 자리수 아래에서 반올림하여 자리수까지 출력
  - 양수 : 소수점 오른쪽 자릿수(소수점 이하)
  - 음수 : 소수점 왼쪽 자릿수(1의 자리부터)
  - 양수 예 : ROUND(3.456, 1) -> 3.500
  
- ROUND예시

~~~sql
-- ROUND
-- 고객별 평균 주문액을 출력
select clientNo, round(avg(bookPrice * bsQty)) as '평균주문액',
				 round(avg(bookPrice * bsQty), 0) as '1의 자리까지 출력',
                 round(avg(bookPrice * bsQty), -1) as '10의 자리까지 출력',
                 round(avg(bookPrice * bsQty), -2) as '100의 자리까지 출력',
                 round(avg(bookPrice * bsQty), -3) as '1000의 자리까지 출력'
from book, booksale
where book.bookNo = booksale.bookno
group by clientNo;
-- 평균 주문액 : 88333
-- 1의 자리까지 : 88333
-- 10의 자리까지 : 88330
-- 100의 자리까지 : 88300
-- 1000의 자리까지 : 88000
~~~

#### 순위 출력 함수
- RANK()
  - 값의 순위 반환(동일 순위 개수만큼 증가)
  - 순위 : 1 1 3 4 5 6 6 8 9 ....
- DENSE_RANK()
  - 값의 순위 반환(동일 순위 상관없이 1증가)
  - 순위 : 1 1 2 3 4 5 5 6 7 ....
- ROW_NUMBER()
  - 행의 순위 증가

- 순위 출력 함수 예시

~~~sql
-- 순위 출력 함수
-- RANK(), DENSE_RANK(), ROW_NUMBER()
select bookPrice, 
		rank() over(order by bookPrice desc) "rank",
        dense_rank() over(order by bookPrice desc) "dense_rank",
        row_number() over(order by bookPrice desc) "row_number"
from book;
~~~

#### 문자함수
- REPLACE()
  - 문자열을 치환(대체)하는 함수
  - 실제 데이터는 변경되지 않고 출력만 바꿔서 해줌
- CHAR_LENGTH()
  - 문자열 길이(글자 수)를 반환
  - 글자와 공백 모두 포함
    - 자바 프로그래밍 -> 8 반환, 안드로이드 프로그래밍 -> 11 반환
- LENGTH()
  - 바이트 수
  - utf-8인 경우 한글은 3바이트
  - 유니코드는 한글 2바이트
    - 자바 프로그래밍 -> 22 반환됨(한글은 3바이트, 공백은 1바이트)
    - HTML & CSS -> 10 반환됨(영어, 공백 모두 1바이트)
- SUBSTR()
  - 지정한 길이만큼의 문자열을 반환하는 함수
  - SUBSTR(전체 문자열, 시작, 길이)
  - 맨 처음 시작은 개발 언어처럼 0이 아닌 1이다.

- 문자함수 예시

~~~sql
-- 문자 함수
-- 도서명에 '안드로이드'가 포함된 도서에 대해
-- '안드로이드'를 'Android'로 변경해서 출력
-- 실제 데이터는 변경되지 않음(출력만 한다) 
-- replace
select bookNo, replace(bookName, '안드로이드', 'Android') bookName, bookAuthor, bookPrice
from book
where bookName like '안드로이드%';

--  char_length(), length()
-- '서울 출판사'에서 출간한 도서의 도서명과 바이트 수, 문자열 길이 출력, 출판사명 출력
select b.bookName as '도서명',
	   length(b.bookName) as '바이트 수',
       char_length(b.bookName) as '길이',
       p.pubName as '출판사'
from book b
inner join publisher p on p.pubNo = b.pubNo
where p.pubName = '서울 출판사';

-- substr(전체 문자열, 시작, 길이)
-- 도서 테이블의 '저자' 열에서 성만 출력
select substr(bookAuthor, 1, 1) as '성'
from book;
-- 도서 테이블의 '저자' 열에서 이름만 출력
select substr(bookAuthor, 2, 2) as '이름'
from book;
~~~

#### 날짜 함수
- DATE(NOW()) : 현재 날짜 출력
- TIME(NOW()) : 현재 시간 출력
- YEAR(CURDATE()) : 현재 날짜 연도 출력
- MONTH(CURDATE()) : 현재 날짜 월 출력
- DAYOFMONTH(CURDATE()) : 현재 날짜 일 출력
- DATEDIFF() : 날짜 차이 계산
- TIMEDIFF() : 시간 차이 계산

- 날짜 함수 예시

~~~sql
-- 날짜 함수
-- 현재 날짜와 시간 출력
select date(now()), time(now());
-- 현재 날짜에서 연, 월, 일 추출
select year(curdate()), month(curdate()), dayofmonth(curdate());
-- 시간에서 시, 분, 초, 마이크로초 출력
-- current_time(), curtime() 둘 다 사용해도 무방하다.
select hour(curtime()),
	   minute(current_time()),
       second(current_time()),
       microsecond(current_time());
       
select hour(curtime()),
	   minute(curtime()),
       second(curtime()),
       microsecond(curtime());
~~~

#### 파일 로드 함수
- 대용량 데이터 저장할 때 사용
- 대본 : text타입
- 동양상 파일 : LONGBLOB 타입
- LOAD_FILE(파일경로)
- 파일 용량이 현재 설정된 크기보다 큰 경우 데이터 저장 안 됨
  - my.ini파일에서 파일 최대 크기 변수 변경
  - 파일 업로드 / 다운로드 하는 폴더 경로를 별도로 허용하는 내용 추가(동영상 파일이 저장된 경로로 지정.. 하려 했지만 맥은 자동 null값이 들어가는 듯 싶다.)

## DDL(Data Control Language)
- 계정 관리
- 데이터의 사용 권한 관리
- 데이터베이스 트랜잭션 명시 (COMMIT / REVOKE)
- COMMIT : 작업 완료
- REVOKE : 작업 취소
- 트랜잭션 처리 중 오류 발생
  - REVOKE 작업 하여 처리하기 이전으로 되돌림.
- GRANT : 데이터베이스 객체 권한 부여
- REVOKE : 이미 부여된 데이터베이스 객체의 권한 취소

### 권한(Privilege)
- 특정 유형의 SQL문을 실행하거나 다른 사용자의 객체를 사용할 수 있는 권리
- 권한의 종류
  - 시스템 권한
  - 객체 권한 : 특정 객체를 조작할 수 있는 권한
    - DML 사용 권한 : SELECT / INSERT / DELETE / UPDATE

- 계정 & 권한 사용 방법

~~~sql
-- DCL
use sqldb3;

-- 사용자 계정 조회하려면 해당 테이블 사용해야 함.
use mysql;

-- 사용자 계정 조회
select * from user;

-- 사용자 계정 생성
-- create user 계정@호스트 identified by 비밀번호
/*
호스트
- localhost : 로컬에서 접근 가능
- 192.168.@@@.@@@ : 특정 ip에서 접근 가능
- '%' : 어디에서나 접근 가능
비밀번호 변경
- SET PASSWORD for '계정명'@호스트 = '새 비밀번호';
계정 삭제
- DROP USER 계정@호스트;
*/

-- 계정생성
create user newuser1@'%' identified by '1111';
-- 스키마 접근 불가

-- 비밀번호 변경
set password for 'newuser1'@'%' = '1234';
-- 서버 연결 (newuser1)

-- 계정 삭제
drop user newuser1@'%';


-- 권한 조회 : SHOW GRANTS FOR 사용자계정;
show grants for root;

-- 권한 부여 : GRANT 권한 ON 데이터베이스.테이블 TO 계정@호스트;
-- 모든 권한 부여 : GRANT ALL PRIVILEGES ON *.* TO 계정@호스트; (*은 '모두'라는 뜻)
-- 특정 DB의 모든 테이블에 특정 권한 부여 : GRANT select, insert, update, delete ON DB명.* TO 계정@호스트;

-- 특정 DB의 모든 테이블에 대한 권한 삭제 : REVOKE ALL PRIVILEGES ON DB.* FROM TO 계정@호스트;

-- 특정 DB의 모든 테이블에 대해 특정 권한 삭제 : REVOKE select, insert, update, delete ON DB명.* FROM 계정@호스트;


-- 계정 생성
create user newuser1@'%' identified by '1111';
-- 권한 조회
show grants for newuser1;
-- 서버 접속은 가능하지만 아무런 스키마가 보이지 않는다(스키마 사용 권한 없음)

-- 모든 권한 부여
grant all privileges on *.* to newuser1@'%';
-- 모든 스키마 / 테이블 접근 가능

-- user1 select 권한 삭제
revoke select on *.* from newuser1@'%';
-- table could not fetched

-- sqldb3의 모든 테이블에 select권한 부여
grant select on sqldb3.* to newuser1@'%';
-- 다른 테이블은 could not fetched
~~~

## 백업 및 복구
- 데이터베이스를 주기적으로 백업해 두거나 다른 서버로 이관할 때 사용
- 백업 : Export
- 복구 : Import
- Server - Data Export or Data Import

## JAVA와 DB연동
- JDBC(Java Database Connectivity)
  - 다양한 종류의 관계형 데이터베이스를 자바와 연동시켜 사용할 수 있게 도와주는 API
  - 모든 DBMS에서 공통적으로 사용할 수 있는 인터페이스와 클래스로 구성됐다
  - 실제 구현 클래스는 각 DBMS 벤더가 구현했기 때문에 모든 벤더가 JDBC드라이버를 제공
    - 각 DBMS에 맞는 JDBC드라이버 사용
  - JDBC 드라이버
    - JDBC 인터페이스를 구현한 클래스 파일 모음(.jar파일)
    - 각 DBMS 벤더에서 제공되는 구현 클래스
  - 응용프로그램과 DBMS 사이에서 연결 역학
  - SQL문을 DBMS에 전달하고 그 결과값을 응용프로그램에 전달하는 역할
  - 장점
    - 사용하는 RDBMS에 독리적인 프로그래밍 가능
    - 쉽게 RDBMS 교체 가능
    - 자바는 단순히 문자열로 쿼리를 전송하고 해석은 각 벤더가 구현한 드라이버에서 담당
    - 표준 SQL뿐 아니라 각 JDBC Driver를 제공하는 DBMS 벤더별로 최적의 성능 발휘
    - 벤더 종속적인 SQL도 처리 가능

## JDBC를 이용한 연결 과정
1. 드라이버 로드
2. Connection 객체 생성
3. Statement 또는 PreparedStatement 생성
4. 쿼리 수행 (sql 문 실행)
5. SQL문에 결과 반환이 있는 경우 ResultSet 객체 생성 (결과 받아옴)
6. 모든 객체 close() : 반환 순서
  - ResultSet 
  - Statement 
  - Connection (접속 종료)

#### 패키지 import
- JDBC는 java.sql 패키지에 포함되어 있음
- import java.sql.DriverManager;
- import java.sql.Connection; ….
- JDBC는 데이터베이스 접속하기 위해
- 한 개의 클래스 java.sql.DriverManager와
- 두 개의 인터페이스(java.sql.Driver 와 java.sql.Connection)를 사용

##### 1 .JDBC 드라이버 로드
- Java에서 MySQL Driver를 사용하기 위해 드라이버를 JVM에 로딩하는 과정
- Class.forName(“com.mysql.cj.jdbc.Driver”);

##### 2. Connection 객체 생성
- DriverManager 클래스의 static 메서드 인 
- getConnection() 메서드를 이용해서 
- Connection 객체를 얻어옴
- MySQL 서버 실제 연결
- Connection 객체가 생성되면 DBMS 접속 성공

~~~java
DriverManager.getConnection(String url,
						  String user,
						  String password)
~~~

- jdbcLmysql : JDBC 드라이버
 - jdbc : JDBC URL의 프로토콜 이름
 - mysql : MySQL JDBC 드라이버
- localhost : MySQL이 설치된 IP (호스트 이름)
 - localhost 또는 127.0.0.1 : 내 컴퓨터
 - 192.168.172.1 : 서버 IP (현재 내 컴퓨터의 Workbench에서 서버 접속해서 사용)
- 3306 : MySQL 접속 포트
- sqldb6 : 사용하는 데이터 베이스 이름
- serverTimezone=UTC


##### 3. Statement 객체 생성
- 쿼리문 전송을 위한 Statement 객체 생성
- 또는 PreparedStatement
- Connection 인터페이스의 createStatement() 메서드를 사용해서 객체 생성
- PreparedStatement pstmt = con.preparedStatement(sql);
- PreparedStatement 객체를 통해 SQL 전송 가능

##### 4. 쿼리 수행
- SQL 전송에 사용되는 메소드
  - executeQuery() / executeUpadte()
    - 두 가지로 구분하는 이유 : sql문 실행 결과가 다르기 때문
  - executeUpdate()
    - 쿼리문이 insert / update / delete 구문인 경우 사용
    - 영향을 받은 행의 수 반환
    - insert 후 반환된 결과값이 0인 경우 insert 되지 않았음
  - executeQuery()
    - select 구문의 경우
    - ResultSet 객체로 반환 (select 문 결과에 해당되는 여러 행 반환)
    - ResultSet에서 데이터 추출
    - next() 메소드 이용해서 논리적 커서를 이동하며 각 열의 데이터를 바인딩
    - rs.next() 호출 결과 true이면 반복해서 다음 행 데이터 가져옴(반복문 사용)
      - cursor : 다음 열로 이동
      - next() : 다음 행으로 이동
      - 정수 : getInt("bookPrice)
      - 문자 : getString("bookName")

##### 5. 모든 객체 자원반납 : close()
- ResultSet
- Statement
- Connection(접속 종료)