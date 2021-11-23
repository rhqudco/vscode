# SQLday_4 정리 (2021.11.23 화요일)

## 조인(join)
- 여러 개의 테이블을 결합하여 조건에 맞는 행 검색
- 조인의 종류
  - 내부 조인(inner join) : 가장 많이 사용 
    - 공통되는 열이 있을 때 공통 열의 속성 값이 동일한 튜플만 반환
      - 기본키 = 외래키 관계에서 테이블의 값을 반환한다.
  - 외부조인(outer join)
    - 공통되는 열이 없을 때 공통되는 열(속성)을 매개로 하는 데이터가 없어도 연산의 결과를 반환
    - 값이 없는 대응 속성에 null값으로 반환
    - 좌측 외부 조인(left outer join)
      - 좌측 테이블의 데이터 유지한다.(우측은 null값 표시)
    - 우측 외부 조인(right outer join)
      - 우측 테이블의 데이터를 유지한다.(좌측은 null값 표시)
    - 완전 외부 조인(full outer join)
      - 두 테이블의 모든 정보 유지

~~~sql
SELECT 열 리스트
FROM 테이블명1
	INNER JOIN 테이블명2
	ON 조인 조건 (기본키=외래키);
~~~

### 내부조인 예시

~~~sql
use sqldb3;

-- 	join 표기 형식

-- 1. where 조건 사용
select client.clientNo, clientName, bsQty
from client, bookSale
where client.clientNo = bookSale.clientNo;
-- 양쪽 테이블에 공통되는 열 이름 앞에 테이블 이름 표기(양쪽에 같은 정보가 있기 때문에 어떤 것을 표시할지 모름)
-- client.clientNo <- 모호성 해결

-- 2. 양쪽 테이블에 공통되지 않지만 모든 열 이름에 테이블명을 붙여 서버에서 찾고자 하는 열의 정확한 위치를 알려줘, 성능을 향상시킴.
select client.clientNo, client.clientName, bookSale.bsQty
from client, bookSale
where client.clientNo = bookSale.clientNo;

-- 3. 테이블명 대신 별칭 사용(alias)
select c.clientNo, c.clientName, bs.bsQty
from client c, bookSale bs
where c.clientNo = bs.clientNo;

-- 4. join on 명시하는 방법
select c.clientNo, c.clientName, bs.bsQty
from bookSale bs
join client c
on c.clientNo = bs.clientNo;

-- 5. inner join on (가장 많이 사용)
select c.clientNo, c.clientName, bs.bsQty
from bookSale bs
inner join client c
on c.clientNo = bs.clientNo;

-- client와 booksale 조인
-- clientNo 기준 :  client(모든 고객) > booksale(주문한 고객)
-- '한 번이라도 도서를 주문한 적 있는 고객'이  join을 통해 얻고자 하는 결과
--  출력 열 선택하지 않으면 2개 테이블의 모든 열이 표시된다.
-- 공통되는 clientNo 열이 중복되어 출력된다.
select *
from client
inner join booksale
on client.clientNo = booksale.clientNo;

-- 필요한 열만 추출한다.
-- 테이블명 대신 alias 사용
-- 한 번이라도 도서를 주문한 적 있는 고객의 고객번호, 고객명 출력
select c.clientno, c.clientname
from client c
inner join booksale bs
on c.clientno = bs.clientno;

-- 중복되는 행은 한 번만 출력하고 한 번이라도 도서를 주문한 적 있는 고객의 고객번호, 고객명 출력하는데 고객번호 기준 오름차순으로 정렬
select distinct c.clientno, c.clientname
from client c
inner join booksale bs
on c.clientno = bs.clientno
order by c.clientno desc;
-- client와 booksale 테이블 위치 상관없음
select distinct c.clientno, c.clientname
from booksale bs
inner join client c
on c.clientno = bs.clientno
order by c.clientno desc;

-- 세 개 테이블 결합
-- 테이블은 세 개 조인 조건은 두 개
-- 주문된 도서에 대하여 고객명과 도서명 출력
-- 주문된 도서 : booksale, 고객명 : client, 도서명 : book
--  booksale : 기본키, 외래키1(clientNo), 외래키2(bookNo) 외래키들이 각각 테이블에 조인
select c.clientName, b.bookName
from booksale bs
inner join client c on c.clientNo = bs.clientNo
inner join book b on b.bookNo = bs.bookNo;

-- 도서를 주문한 고객의 고객 정보, 주문 정보, 도서 정보 출력
-- 주문번호, 주문일, 고객번호, 고객명, 도서명, 주문수량
-- 날짜 기준 최근 주문이 먼저 출력되도록
select bs.bsNo, bs.bsDate, c.clientNo, c.clientName, b.bookName, bs.bsQty
from booksale bs
inner join client c on c.clientNo = bs.clientNo
inner join book b on b.bookNo = bs.bookNo
order by bs.bsDate desc;

-- 고객별로 총 주문 수량 계산하여 고객번호, 고객명, 총 주문수량 출력
-- 총 주문수량 기준 내림차순 정렬
-- 고객별 = group by, 고객번호 = client 테이블 필요, 총 주문수량 = booksale 필요, 2개 테이블 사용 = 조인(공통값 있으므로 inner join), 내림차순 = order by
select c.clientName, c.clientNo, sum(bsQty) as TotalQty
from booksale bs
inner join client c on c.clientNo = bs.clientNo
group by c.clientNo
order by TotalQty desc;

-- 주문일, 고객명, 도서명, 도서 가격, 주문수량, 주문액 계산하여 출력
-- 주문일 오름차순 정렬
select bs.bsDate, c.clientName, b.bookPrice, bs.bsQty, b.bookPrice * bs.bsQty as 주문액
from booksale bs
inner join client c on c.clientNo = bs.clientNo
inner join book b on b.bookNo = bs.bookNo
order by bs.bsDate;
-- 2019년 ~ 현재까지 판매된 내용만 출력
select bs.bsDate, c.clientName, b.bookPrice, bs.bsQty, b.bookPrice * bs.bsQty as 주문액
from booksale bs
inner join client c on c.clientNo = bs.clientNo
inner join book b on b.bookNo = bs.bookNo
where bs.bsDate >= '2019-01-01'
order by bs.bsDate;
~~~

### 내부조인 연습문제

~~~sql
/*
연습문제
1. 모든 도서에 대하여 도서의 도서번호, 도서명, 출판사명 출력
2. ‘서울 출판사'에서 출간한 도서의 도서명, 저자명, 출판사명 출력 (조건에 출판사명 사용)
3. ＇종로출판사'에서 출간한 도서 중 판매된 도서의 도서명 출력 (중복된 경우 한 번만 출력) (조건에 출판사명 사용)
4. 도서가격이 30,000원 이상인 도서를 주문한 고객의 고객명, 도서명, 도서가격, 주문수량 출력
5. '안드로이드 프로그래밍' 도서를 구매한 고객에 대하여 도서명, 고객명, 성별, 주소 출력 (고객명으로 오름차순 정렬)
6. ‘도서출판 강남'에서 출간된 도서 중 판매된 도서에 대하여 ‘총 매출액’ 출력
7. ‘서울 출판사'에서 출간된 도서에 대하여 판매일, 출판사명, 도서명, 도서가격, 주문수량, 주문액 출력
8. 판매된 도서에 대하여 도서별로 도서번호, 도서명, 총 주문 수량 출력
9. 판매된 도서에 대하여 고객별로 고객명, 총구매액 출력 ( 총구매액이 100,000원 이상인 경우만 해당)
10. 판매된 도서 중 ＇도서출판 강남'에서 출간한 도서에 대하여 고객명, 주문일, 도서명, 주문수량, 출판사명 출력 (고객명으로 오름차순 정렬)
*/
-- no.1
select b.bookNo, b.bookName, p.pubName
from book b
inner join publisher p on p.pubNo = b.pubNo;

-- no.2
select b.bookName, b.bookAuthor, p.pubName
from book b
inner join publisher p on p.pubNo = b.pubNo
where p.pubName = '서울 출판사';

-- no.3
select distinct bs.bookName, p.pubName
from book b
inner join publisher P on  B.pubNo = P.pubNo
inner join bookSale BS on  B.bookNo = BS.bookNo
where pubName = '종로출판사';

-- no.4
select c.clientName, b.bookName, b.bookPrice, bsQty
from booksale bs
inner join client c on c.clientNo = bs.clientNo
inner join book b on b.bookNo = bs.bookNo
where b.bookPrice >= 30000;

-- no.5
select b.bookName, c.clientName, c.clientGender, c.clientAddress
from bookSale bs
inner join book b on b.bookNo = bs.bookNo
inner join client c on c.clientNo = bs.clientNo
where bookName = '안드로이드 프로그래밍'
order by c.clientName;

-- no.6
select p.pubName, sum(bs.bsQty * b.bookPrice) as '총 매출액'
from book b
inner join publisher p on p.pubNo = b.pubNo
inner join bookSale bs on bs.bookNo = b.bookNo
where p.pubName = '도서출판 강남';

-- no.7
select bs.bsDate, p.pubName, b.bookName, b.bookPrice, bs.bsQty, bs.bsQty * b.bookPrice as 주문액
from booksale bs
inner join book b on b.bookNo = bs.bookNo
inner join publisher p on p.pubNo = b.pubNo
where p.pubName = '서울 출판사';

-- no.8
select b.bookNo, b.bookName, sum(bs.bsQty) as '총 주문 수량'
from book B
inner join bookSale BS on B.bookNo = BS.bookNo       		
group by B.bookNo;


-- no.9
select c.clientName, sum(b.bookPrice * bs.bsQty) as '총주문액'
from booksale bs
inner join client c on c.clientNo = bs.clientNo
inner join book b on b.bookNo = bs.bookNo
group by c.clientNo
having sum(b.bookPrice * bs.bsQty) >= 100000;

-- no.10
select c.clientName, bs.bsDate, b.bookName, bs.bsQty, p.pubName    
from bookSale BS 
inner join client c on c.clientNo = bs.clientNo
inner join book b  on b.bookNo = bs.bookNo       
inner join publisher p on b.pubNo = p.pubNo
where p.pubName = '도서출판 강남'
order by c.clientName;
~~~

### 외부조인 예시

~~~sql
-- 외부조인
-- 1. 왼쪽 테이블 기준(left outer join)
-- client, booksale
-- 왼쪽 테이블(client) 데이터 모두 출력
-- 오른쪽 테이블 해당 값 없으면 null 출
-- 의미 : 고객 중 한 번도 구매한 적이 없는 고객은 null로 출력
select *
from client c
left outer join booksale bs
on c.clientNo = bs.clientNo
order by c.clientNo;

-- 고객 중에서 한 번도 구매한 적이 없는 고객의 고객 번호, 고객명 출력
select c.clientNo, c.clientName
from client c
left outer join booksale bs
on c.clientNo = bs.clientNo
where bs.clientNo is null
order by c.clientNo;

-- 도서 중에서 힌 반도 판매된 적이 없는 도서의
-- 도서번호, 도서명 출력 
select b.bookNo, b.bookName
from book b
left outer join booksale bs
on b.bookNo = bs.bookNo
where bs.bookNo is null
order by b.bookNo;

-- 오른쪽 테이블 기준
-- 오른쪽 booksale 데이터 모두 출력
-- 왼쪽 테이블 client에는 주문한 적 있는 고객 정보만 출력
select *
from client c
right outer join booksale bs
on c.clientNo = bs.clientNo
order by c.clientNo;

-- 한 번이라도 주문한 적 있는 고객의 고객번호, 고객명 출력(중복된 경우 한 번만 출력)
select distinct c.cleintNo, c.clientName
from client c
right outer join booksale bs
on c.clientNo = bs.clientNo
order by c.clientNo;

-- 완전 외부 조인(full outer join)
-- MySQL에서는 full 키워드를 지원하지 않는다.
-- left join과 right join을 union해서 사용할 수 있다.
select *
from client c
left join booksale bs
on c.clientNo = bs.clientNo
union
select *
from client c
right join booksale bs
on c.clientNo = bs.clientNo;
~~~

## 서브 쿼리(subQuery)
- 하위 질의 또는 부속 질의 라고도 함
- 하나의 SQL문 안에 다른 SQL문이 중접최더 있는 형태
- 질의를 1차 수행하고 반환된 값을 다음 질의에 포함시켜 사용
  - 다른 테이블에서 결과를 가져온 데이터를 통해 현재 테이블에 있는 정보를 찾거나 가공할 때 사용
- 서브 쿼리의 구성 및 형식
  - 메인 쿼리와 서브 쿼리로 구성
  - 서브 쿼리에서 검색한 결과로 메인 쿼리 검색
  - 단일 행 서브쿼리
    - 서브 쿼리 결과 값이 단일 행인 경우
    - __'='__ 연산자 사용
  - 다중 행 서브쿼리
    - 서브 쿼리 결과 값이 여러 행인 경우
    - IN, ANY, ALL, EXISTS 연산자 사용
  - 서브 쿼리 연산자
    - __WHERE__ 절에서 사용
    - 비교 연산자
      - =, >, <, >=, <=, !=
      - 단일 행 반환
    - 집합 연산자
      - IN, NOT IN
      - 다중 행 반환
    - 존재 연산자
      - EXISTS, NOT EXISTS
      - 다중 행 반환
    - 한정 연산자 
      - ALL(모두)
      - ANY(최소 하나라도)
      - 다중 행 반환

#### 조인과 서브쿼리의 차이

##### 조인
- 조인은 여러 테이블의 데이터를 모두 합쳐서 연산
- 카티전프로덕트 후 조건에 맞는 행 검색
- 카티전프로덕트 + select 연산
- 예 : 테이블1(15행), 테이블2(3행)이면 15 * 3 = 45행 반환

##### 서브쿼리
- 필요한 데이터만 찾아서 제공
- 테이블1에서 찾아서 그 결과를 테이블2에서 검색
- 예 : 테이블1(15행), 테이블2(3행)이면 15 + 3 = 18행 검색
- 경우에 따라 조인보다 성능이 더 좋을 수도 있지만 대량에 데이터에서는 서브쿼리를 수행할 때 성능이 더 나쁠 수도 있다

### 단일 행 서브쿼리
~~~sql
-- 서브쿼리

-- 단일 행 서브쿼리(=)
-- 고객 호날두의 주문수량 조회
-- 1. client 테이블에서 고객명 호날두의 clientNo를 찾아서 
-- 2. booksale에서 clientNo에 해당되는 주문에 대해 주문일, 주문수량 출력
select bsDate, bsQty
from booksale
where clientNo = (select clientNo
					from client
					where clientName = '호날두');

-- 호날두가 주문한 총 주문수량 출력
-- 1. client 테이블에서 고객명 호날두의 clientNo를 찾아서 
-- 2. booksale에서 clientNo에 해당되는 주문에 대해 총 주문수량 출력
select sum(bsQty) as '총 주문 수량'
from booksale
where clientNo = (select clientNo
					from client
					where clientName = '호날두');

-- 가장 비싼 도서의 도서명과 가격 출력
-- 1. 가장 비싼 도서를 찾아서 해당 도서의 도서명과 가격 출력
select bookName, bookPrice
from book
where bookPrice = (select max(bookPrice)
					from book);
                    
-- 단일 행 서브퀴리 비교 연산자 사용
-- 1. 도서의 평균 가격보다 비싼 도서에 대해 도서명, 가격 출력
-- 평균 도서 가격을 서브쿼리에서 반환하기 때문에 단일행 반환
select bookName, bookPrice
from book
where bookPrice >= (select avg(bookPrice)
					from book);
-- 책의 평균 가격
select round(avg(bookPrice))
from book;

-- 다중 행 서브쿼리(IN, NOT IN)
-- 도서를 구매한 적이 있는 고객의 고객명, 고객번호 출력
-- 1. booksale에 있는 clientNo는 모두 구매한 고객이다.
-- 2. clientNo에 해당되는 고객을 client테이블에서 clientName을 찾는다
select clientName, clientNo
from client
where clientNo in (select clientNo
					from bookSale);
-- 한 번도 주문한 적 없는 고객명, 고객번호 출
select clientName, clientNo
from client
where clientNo not in (select clientNo
					from bookSale);
-- 도서명이 '안드로이드 프로그래밍'인 도서를 구매한 고객의 고객명 출력
-- 1. book 테이블에서 원하는 도서명의 bookNo를 검색
-- 2. bookSale에서 bookNo에 해당되는 도서를 구매한 clientNo를 찾고
-- 3. client 테이블에서 이 clientNo에 해당되는 고객명을 출력
select clientName
from client
where clientNo in (select clientNo
					from bookSale
					where bookNo in (select bookNo
										from book
                                        where bookName = '안드로이드 프로그래밍'));
-- in : 다중 행 반환인 경우에 사용(단일 행 반환 시 사용해도 오류 없음)
-- = : 단일 행 반환인 경우에 사용(결과가 여러 행인 경우에 사용시 오류 해결)
-- 결과 행을 잘 모르겠으면 in 사용

-- 고객명 기준으로 정렬
select clientName
from client
where clientNo in (select clientNo
					from bookSale
					where bookNo in (select bookNo
										from book
                                        where bookName = '안드로이드 프로그래밍'))
order by clientName;
~~~

### 다중 행 서브 쿼리(EXISTS, NOT EXISTS)

~~~sql
-- 다중 행 서브 쿼리(EXISTS, NOT EXISTS)
-- EXISTS : 서브 쿼리 결과가 행을 반환하면 참이 되는 연산자
-- 도서를 구매한 적이 있는 고객
-- 1. bookSale에 조건에 해당되는 행이 존재하면 참 반환
-- 2. client 테이블에서 이 clientNo에 해당되는 고객의 고객번호, 고객명 출력
select clientNo, clientName
from client
where exists (select clientNo
				from bookSale
				where client.clientNo = bookSale.clientNo);
-- 구매한 적 없는 고객번호, 고객명 출력
-- not exists
select clientNo, clientName
from client
where not exists (select clientNo
				from bookSale
				where client.clientNo = bookSale.clientNo);
-- null인 경우 in과 exists의 차이
-- clientHobby에 null값이 포함됐다
-- exists : 서브 쿼리에 null값 포함
-- null과 공백 다 출력됨.
select clientHobby
from client
where exists (select clientHobby
					from client);
-- in : 서브 쿼리 결과에 null 값 포함되지 않음
-- null 값을 갖지 않는 행만 출력
-- null 제외 공백, 유효값 출력됨.
select clientHobby
from client
where clientHobby in (select clientHobby
					from client); 
~~~

#### IN과 EXISTS의 차이 (NOT IN과 NOT EXISTS의 차이)

#### IN
- 서브 쿼리에서 조건에 해당되는 행의 열을 비교하여 값 확인
- 서브 쿼리의 결과 값을 메인 쿼리에 대입하여 조건 비교 후 결과 출력
- IN -> 메인 쿼리
- IN : 결과에 NULL 값 포함되지 않음

##### EXISTS
- 서브 쿼리에서 조건에 해당되는 행의 존재 여부만 확인 (TRUE/FALSE 반환)
- 따라서 IN에 비해 성능 좋음
- EXISTS 키워드 앞에 속성명, 수식 등 올 수 없음
- WHERE 절에 외래키 제약조건 지정
- EXISTS : NULL 값도 결과에 포함

##### NOT EXISTS와 NOT IN 차이
- 대부분 NOT EXISTS와 NOT IN 결과 동일하지만
- 공통되는 조인 속성의 값이 NULL인 경우 결과 다름
  - NOT EXISTS : NULL 값도 결과에 포함
  - NOT IN : NULL 값이 결과에 포함되지 않음

### ALL / ANY
- 관계 연산자 뒤에 위치

~~~sql
where bsQty > ALL(...);
~~~

#### ALL
- 검색 조건이 서브 쿼리 결과의 모든 값에 만족하면 참
- 조건  > ALL(서브 쿼리)

#### ANY
- 검색 조건이 서브 쿼리 결과 중 하나 이상에 만족하면 참
- 조건 > ANY(서브 쿼리)

### 서브쿼리 종합 연습

~~~sql
/*
연습문제 (서브 쿼리 사용)
1. 호날두(고객명)가 주문한 도서의 총 구매량 출력
2. ‘종로출판사’에서 출간한 도서를 구매한 적이 있는 고객명 출력
3. 베컴이 주문한 도서의 최고 주문수량보다 더 많은 도서를 구매한 고객명 출력
4. 서울에 거주하는 고객에게 판매한 도서의 총 판매량 출력
*/
-- no.1
select sum(bsQty)
from bookSale
where clientNo = (select clientNo
					from client
					where clientName = '호날두');

-- no.2
select clientName
from client
where clientNo in (select clientNo
					from bookSale
					where bookNo in (select bookNo
									from book
									where pubNo in (select pubNo
													from publisher
													where pubName = '종로출판사'))); 

-- no.3
select clientName
from client
where clientNo in (select clientNo
					from bookSale
					where bsQty > all (select bsQty
										from bookSale
										where bsQty > all (select bsQty
														from bookSale
														where clientNo in (select clientNo
																			from client
																			where clientName = '베컴')));	
                    
-- no.4
select sum(bsQty)
from bookSale
where clientNo in (select clientNo
					from client
					where clientAddress like '서울%');
~~~

## 스칼라 서브 쿼리 (Scalar Subquery)
- SELECT 절에서 사용
- SELECT 절에 오는 것은 열이름 리스트
- 단일 열 반환
- 결과 값을 단일 열의 스칼라 값으로 반환
- 스칼라 값이 들어 갈 수 있는 곳에서 사용 가능
- 일반적으로  SELECT 문과 UPDATE SET 문에서 사용 가능

#### 스칼라 서브 쿼리 예시

~~~sql
-- no.4
select sum(bsQty)
from bookSale
where clientNo in (select clientNo
					from client
					where clientAddress like '서울%');
                    
-- 스칼라 서브쿼리
-- 고객별로 고객변호, 고객명, 총 주문수량 출력
select clientNo, sum(bsQty), (select clientName
								from client
                                where client.clientNo = bookSale.clientNo)
from bookSale
group by clientNo;
-- 스칼라 서브쿼리
-- 고객별로 고객변호, 고객명, 총 주문수량 출력할 때 결과에 이름 지정
select clientNo, sum(bsQty) as '총 주문 수량', (select clientName
								from client
                                where client.clientNo = bookSale.clientNo) as '고객명'
~~~

## 인라인 뷰 (InLine View) 서브 쿼리
- FROM 절에서 사용
- 즉, 테이블명 대신 인라인 뷰 쿼리 결과(가상 테이블 : 뷰) 사용
- 서브 쿼리 결과로 반환되는 데이터는 다중 행, 다중 열이어도 상관 없음
- 가상의 뷰 형태로 제공
- 개발 중에 뷰가 필요한 모든 경우 뷰를 생성하면 관리할 양이 많아 트랜잭션 관리나 성능 상 문제가 발생할 수 있기 때문에 필요한 시점에 따라 필요한 뷰을 인라인 뷰로 생성해서 사용
- 결과는 인라인 뷰 서브쿼리에 있는 SELECT문에서 찾고자 하는 속성의 값으로만 이루어진 테이블로 반환된다.

#### 인라인 뷰 서브 쿼리 예시

~~~sql
-- 인라인 뷰 서브 쿼리
-- 도서 가격이 25,000 이상인 도서에 대하여 도서별로 도서명, 도서가격, 총 판매수량, 총 판매액 출력
-- 총 판매액 기준으로 내림차순 정렬
select bookName, bookPrice, sum(bsQty) as 총판매량, sum(bookPrice * bsQty) as '총 판매액'
from (select bookNo, bookName, bookPrice
		from book
		where bookPrice >= 25000) book, bookSale
where book.bookNo = bookSale.bookNo
group by book.bookNo
order by 총판매량 desc;
~~~

## 테이블 복사
- 새 테이블로 전체 복사
- 새 테이블로 일부만 복사
- 기존 테이블로 데이터만 복사
  - 테이블 구조가 동일한 경우에만 가능
- 다른 데이터베이스의 테이블 복사
- 테이블 복사 구문
- 주의사항
  - 기본키 등 제약조건은 복사 안 됨
  - 복사 후 제약조건 설정해야 함



~~~sql
CREATE TABLE 새 테이블 이름 AS
SELECT 열이름 리스트 
FROM 원본 테이블;
~~~

#### 테이블 복사 예시

~~~sql
-- 테이블 복사
-- 제약조건 복사 안됨
-- 복사 후 제약조건 설정 필요

-- 테이블 복사 : 새 테이블로 전체 복사
create table new_book1 as
select * 
from book;

select * from new_book1
desc new_book1;

-- 기본키 제약조건 추가
alter table new_book1
add constraint PK_new_book1_bookNo
primary key (bookNo);

-- 테이블 복사 : 새 테이블로 일부만 복사
create table new_book2 as
select * 
from book
where bookDate like '2020%';

select * from new_book2
desc new_book2;

-- 기본키 제약조건 추가
alter table new_book2
add constraint PK_new_book2_bookNo
primary key (bookNo);

-- 테이블 복사 : 기존 테이블로 데이터만 복사
-- 테이블 구조가 동일한 경우에만 가능

-- new_book2 테이블 데이터 전체 삭제 (구조, 제약조건은 남아 있음)
delete from new_book2;

-- new_book2 테이블에 데이터 복사
insert into new_book2
select *
from book;

select * from new_book2
desc new_book2;

-- 테이블 복사 : 다른 데이터베이스의 테이블에서 복사
-- 새 테이블로 일부 복사
create table product2 as
select * 
from sqldb2.product
where prdPrice >= 1000000;

-- 기본키 제약조건 추가
alter table product2
add constraint PK_product2_prdNo
primary key (prdNo);
~~~