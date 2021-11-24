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