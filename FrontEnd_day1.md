# FrontEnd_day1 정리 (2021.12.02 목요일)

## Front-End 개발
- 웹 사이트 중 사용자와 직접 상호작용하는 부분 개발
- 사용자 인터페이스(UI)와 사용자 경험(UX)을 만드는데 초점을 맞추고 있음
- 화면 디자인 : 드롭다운 메뉴, 레이아웃, 슬라이드 쇼, 폰트, 컬러 등
- 언어 : HTML, CSS, JavaScript(각종 라이브러리 포함)
- 프레임워크 : Bootstrap, Angular, Vue.js 등

## Back-End 개발
- 서버 측 개발 분야
- 프론트엔드에 있는 사용자의 요구를 처리하고 응답.
- 웹 서버, 응용 프로그램, 데이터베이스로 구성
- 시스템 컴포넌트 작업, API 작성, 라이브러리 생성, 데이터베이스 통합 등 다양한 작업 처리
- 언어 : Java(Servlet/JSP), PHP, Python, .Net등
- 자바스크립트 라이브러리 : Ajax
- 프레임워크
  - 자바 : Spring
  - 파이썬 : Django
  - JavaScript : Node.js

# FrontEnd_day1 정리 (2021.12.02 목요일)

## HTML(Hyper Text Markup Language)
- 웹 브라우저에서 하이퍼텍스트 기능을 구현하는 웹 페이지 작성 언어
- 하이퍼텍스트
  - 문서간에 서로 링크가 되어 있어 링크를 클릭하면 해당 문서로 이동하는 기능
- HTML 문서의 구성
  - 태그
  - 출력하고자 하는 문서 내용

### 태그(Tag)
- HTML에서 사용하는 명령어(문자열 기호)
- 원하는 모양과 형태로 브라우저에게 명령을 내림
- \<html>, \<body>, \<p></p>
- 태그 사용 형식
  - 대부분 시작 태그(\<태그명>)와 종료 태그(\</태그명>)를 함께 사용
  - \<태그명>출력내용\</태그명>
    - \<title>문서 제목\</title>
    - \<p>문단 형식으로 출력\</p>
  - <태그명 속성명=”속성값”>출력 내용</태그명>
    - \<a href=”a.html” target=”iFrame”>이동</a>
- 종료 태그 없이 혼자 사용하는 태그도 있다.
  - \<br> : 줄바꿈
  - \<img> : 이미지 삽입
  - \<hr> : 수평선 삽입
- 태그는 대/소문자 구분 없이 사용한다.

### HTML 문서 구조
- \<head>와 \<body>로 구성
- 화면에 출력하고자 하는 모든 내용은 \<body> 태그 안에 포함
- \<head> 부분
  - 문서의 정보를 작성하는 부분
  - 문자 세트 설정
    - \<meta charset="UTF-8">
    - 문자열 처리 방식
  - 문서의 제목 설정 \<title>Hello World!\</title>
  - 외부 파일 연결
  - CSS 정의
  - 자바스크립트 정의(필요한 경우 body에도 포함)
  - 등등...

~~~html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello World!</title>
</head>
~~~

## 기본 태그
- HTML 문서 구조 태그
- 텍스트 관련 태그
- 하이퍼링크 태그
- 목록 태그
- 테이블 태그
- 이미지 / 이미지 맵 태그
- 문서 삽입 태그
- 오디오 / 비디오 태그
- 입력 양식 태그
- 공간 분할 태그
- HTML5 시멘틱 구조 태그

# FrontEnd_day1 정리 (2021.12.02 목요일)

## 문서 구조 태그
- \<html>\</html> 태그
  - 문서의 시작과 끝 표시
  - 크게 두 부분으로 구성되어 있음
    - \<head>\</head>
    - \<body>\</body>
- \<head>\</head> 태그
  - 웹 브라우저 화면에는 보이지 않지만 브라우저가 알아야 할 문서 정보 포함
  - \<meta> 태그
    - 문자 인코딩, 문서 키워드, 문서 정보 등
  - \<link> 태그
    - 외부 리소스 연결
    - \<link rel="stylesheet" href=myCss.css>
  - \<title>\</title>
    - 문서 제목
  - \<script>\</script>
    - 자바스크립트 코드 삽입
- \<body>\</body> 태그
  - 문서의 몸통 부분
  - 실제 화면에 보이는 문서 내용 포함
  - 대부분의 태그가 \<body>\</body> 사이에 위치
  - 종료 태그 \</body> 뒤에 다른 태그를 위치시키지 않는다.
  - 줄 바꿈 / 공백 문자 사용하지 않는 경우 줄이 바뀌지 않고 공백은 1개만 인식한다.
  - \<br> 태그를 이용하여 줄바꿈 해야 함.
  - __&nbsp__ 가 스페이스바 1개 역할.

# FrontEnd_day1 정리 (2021.12.02 목요일)

## 텍스트 관련 태그
- 제목
  - \<h1, 2, 3, 4, 5 ,6>\</h1, 2, 3, 4, 5, 6>
  - HeadLine의 약어
  - 제목으로 사용
  - 자동 줄바꿈으로 출력
  - 크기는 1~6 (1 > 6)
- 본문
  - \<p>\</p>
  - 문단을 나누는 태그(paragraph)
  - 새로 줄 바꿔서 시작
  - \<br> 태그를 두 번 사용한 만큼의 간격
  - \<p> 태그를 여러 번 연속적으로 사용해도 행 간격이 더 이상 벌어지지 않음
- 텍스트 형태
  - \<b> \<i> \<strong> \<em>
- 앵커 태그
  - \<a>\</a>
- \<br> 태그
  - 줄 바꿈 태그
  - 여러 줄을 바꾸려면 여러 개 사용
  - \<br>\<br>\<br>
- \<hr> 태그
  - <hr>
  - \<hr>\</hr>
  - 수평 줄 표시
- 주석 처리
  - \<!-- 주석 입니다 -->
- 텍스트에 장식 효과를 주는 태그
  - \<b>\</b>, \<string>\</strong> : 텍스트 강조
  - \<i>\</i>, \<em>\</em> : 이탤릭체
  - \<sub>\</sub> : 아래첨자
  - \<sup>\</sup> : 위첨자
  - \<big>\</big> : 현재 설정된 크기 보다 2포인트 크게
  - \<small>\</small> : 현재 설정된 크기보다 2포인트 작게
  - \<ins>\</ins> : 밑줄 표시
  - \<del>\</del>, \<strike>\</strike> : 가운데 줄 표시(취소선)
- \<pre> 태그
  - 입력한 형태 그대로 출력
- \<span> 태그
  - \<span>\</span>
  - 줄바꿈 없이 영역 묶기
  - 태그 자체로는 아무 의미가 없지만
  - 텍스트 단락 안에서 줄바꿈 없이 일부 텍스트만 묶어서 스타일을 적용하려고 할 때 주로 사용
  - 대한민국 \<span>서울\</span>

# FrontEnd_day1 정리 (2021.12.02 목요일)

## 하이퍼링크 태그
- 하이퍼링크로 문서를 연결하는 \<a> 태그 (앵커 태그)
- 원하는 문서나 사이트로 연결
- 한 문서 내 다른 영역으로 이동 (한 페이지 안에서 지정된 영역으로 이동)
- \<a href="파일 경로" target="연결된 문서가 보여줄 위치(프레임영역)">
- 사이트로 이동 : \<a href=”http://www.naver.com”>
- 다른 문서로 이동 : \<a href=”newMember.html”>
- 문서 내 다른 영역으로 이동 : \<a href=”#jQuery”>id가 jQuery인 영역으로 이동\</a>
  - \<h3 id="jQuery">temp\</h3>

##### 하이퍼링크 예제

- index.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello World!</title>
</head>
<body>
    <h1>HeadLine 1</h1>
    <hr>
    <br>
    <br>
    <h2>HeadLine 2</h2>
    <h3>HeadLine 3</h3>    
    <!-- 주석 입니다 -->
</body>
</html>
~~~

- hyperlink.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HyperLink : a tag</title>
</head>
<body>
    <h3>사이트로 이동</h3>
    <a href="http://www.naver.com">네이버로 이동</a>
    <h3>다른 문서로 이동</h3>
    <a href="index.html">index로 이동</a>
    <h3>문서 내 다른 영역으로 이동</h3>
    <a href="#javascript">id가 javascript인 곳으로 이동</a><br> <br>
    <a href="#jquery">id가 jquery인 곳으로 이동</a><br> <br>
    <a href="#css">id가 css인 곳으로 이동</a><br> <br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <h3 id="javascript">javascript</h3>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <h3 id="jquery">jquery</h3>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br>
    <h3 id="css">css</h3>
</body>
</html>
~~~

# FrontEnd_day1 정리 (2021.12.02 목요일)

## 목록 태그
- 기본 목록
  - \<ul> : 순서가 없는 목록
    - type
      - disc : 검은 원(기본 값)
      - circle : 흰 원
      - square : 사각형
  - \<ol> : 순사가 있는 목록
    - type
      - 1 : 숫자(기본 값)
      - a : 영어 소문자
      - A : 영어 대문자
      - i : 소문자 로마 숫자
      - I : 대문자 로마 숫자
      - start="n" : n번부터 시작
      - type="@@@" reversed : 역순으로 표시
  - \<li> : 목록 내 각 항목을 적을 때 사용
- 정의 목록
  - \<dl>, \<dt>, \<dd>

##### 목록 태그 예제

- list.html

~~~html
<body>
    <ul type="disc"> <!-- 검은 동그라미(기본 값) -->
        <li>javascript/jquery</li>
        <li>web</li>
        <li>internet</li>
    </ul>
    <ul type="circle"> <!-- 빈 동그라미 -->
        <li>water</li>
        <li>coke</li>
        <li>beer</li>
    </ul>
    <ul type="square"> <!-- 검은 네모 -->
        <li>asdas</li>
        <li>dasdasdas</li>
        <li>asdasdadx</li>
    </ul>
    <hr>
    <hr>
    <ol type="1">
        <li>asdasd</li>
        <li>asdasd</li>
        <li>asdasd</li>
    </ol>
    <ol type="a">
        <li>asdasd</li>
        <li>asdasd</li>
        <li>asdasd</li>
    </ol>
    <ol type="A">
        <li>asdasd</li>
        <li>asdasd</li>
        <li>asdasd</li>
    </ol>
    <ol type="i">
        <li>asdasd</li>
        <li>asdasd</li>
        <li>asdasd</li>
    </ol>
    <ol type="I">
        <li>asdasd</li>
        <li>asdasd</li>
        <li>asdasd</li>

    </ol>
    <ol type="A" reversed>
        <li>asdasd</li>
        <li>asdasd</li>
        <li>asdasd</li>
    </ol>
    <ol start="5">
        <li>asdasd</li>
        <li>asdasd</li>
        <li>asdasd</li>
    </ol>
    <hr>
    <hr>
</body>
~~~

- listprac.html

~~~html
<body>
    <h3>컴퓨터 관련 보유 기술</h3>
    <ul>
        <li>프로그래밍</li>
        <ul type="circle">
            <li>웹 프로그래밍</li>
            <ol>
                <li>JSP/Serverlet</li>
                <li>HTML/JavaScript/jQuery</li>
            </ol>
        </ul>
        <ul type="circle">
            <li>모바일 프로그래밍</li>
            <ol>
                <li>Java</li>
                <li>안드로이드</li>
            </ol>
        </ul>
    </ul>
    <ul>
        <li>웹 및 모바일 디자인</li>
        <ol>
            <li>포토샵</li>
            <li>illustrator</li>
            <li>HTML5/CSS3</li>
        </ol>
    </ul>
    <ul>
        <li>데이터 베이스</li>
        <ol>
            <li>Mysql</li>
            <li>MS SQL Server</li>
            <li>Oracle</li>
        </ol>
    </ul>
</body>
~~~

# FrontEnd_day1 정리 (2021.12.02 목요일)

## 테이블 태그
- \<table> : 테이블 선언 태그
- \<tr> : 테이블 내에 한 행을 정의하는 태그
- \<td> : 테이블 내의 한 열, 즉 셀을 만들 때 사용하는 태그
- 테이블 속성
  - align : 테두리 정렬방식(left, right, center)
  - border : 테이블 테두리, 생략하면 테두리 없음
  - bordercolor : 테두리 색상
  - width : 테이블의 너비(가로 길이)
  - height : 테이블의 높이(세로 길이)
  - bgcolor : 테이블 배경색
  - background : 테이블에 배경 이미지 넣기
  - cellspacing : 셀과 셀 사이의 여백
  - cellpadding : 텍스트와 셀 사이의 여백
- 행 속성
  - align : 행 전체의 수평 정렬(left, right, center)
  - width : 행의 가로 길이
  - height : 행의 세로 길이
  - bgcolor : 행의 배경색
- 셀 속성
  - valign : 셀의 수직 정렬(top, middle, bottom)
  - align : 셀의 수평 정렬(left, right, center)
  - width : 셀의 가로 길이
  - height : 셀의 세로 길이
  - bgcolor : 셀의 배경색
  - background : 셀의 배경 이미지
  - rowspan : 행 합치기
  - colsapn : 열 합치기


##### 테이블 태그 예제

- table.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        td {width: 100px;}

    </style>
</head>
<body>
    <table border="1">
        <caption>테이블1</caption>
        <thead align="center"></thead>
        <tr><th>a</th><th>b</th><th>c</th><th>d</th></tr>
        <tr><td rowspan="3">a1</td><td>b1</td><td>c1</td><td>d1</td></tr>
        <tr><td>a2</td><td>b2</td><td>c2</td></tr>
        <tr><td>a3</td><td>b3</td><td>c3</td></tr>
        <tr><td colspan="4">a4</td></tr>
    </table>
    <br><br>
    <table border="2">
        <caption>테이블2</caption>
        <thead align="center">
        <tr> <th>a</th> <th>b</th> <th>c</th> <th>d</th> </tr>
        <tr> <td rowspan="4">a1</td> <td colspan="3">b1</td> </tr>
        <tr> <td>b2</td> <td>c2</td> <td>d2</td> </tr>
        <tr> <td rowspan="2">b3</td> <td>c3</td> <td rowspan="3">d3</td> </tr>
        <tr> <td>c4</td> </tr>
    </thead>
    </table>

</body>
</html>
~~~

# FrontEnd_day1 정리 (2021.12.02 목요일)

## 이미지 태그
- \<img> 태그
- 인라인 태그로 이미지 바로 옆에 다른 요소가 나란히 배치
- 여러 개의 태그를 사용하면 계속해서 오른쪽에 표시
- 속성
  - src : 이미지 경로(필수)
  - align : 정렬 방식
  - alt : 이미지 출력 안될 때 대체 텍스트
  - title : 마우스 위치에 출력되는 툴 팁 설명
  - width : 가로 길이
  - height : 세로 길이
  - border : 테두리
  - hspace : 좌/우 여백
  - vsapce : 상/하 여백
- 경로
  - HTML 파일과 같은 폴더에 있는 경우
    - 이미지 파일명만 적으면 됨
    - \<img src=”사진.jpg”>
  - 하위 폴더에 있는 경우
    - 폴더명/이미지 파일명
    - \<img src=”image/사진.jpg”>
  - 상위 폴더에 있는 경우
    - ../폴더명/이미지 파일명
    - \<img src=”../image/사진.jpg”>



##### 이미지 + 테이블 연습 문제

- img.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        td{width:200px;}
        th{width:150px;}
    </style>
</head>
<body>
    <a href="list.html">
    <img src="image/그림.PNG" border="1"
    width="300" height="200"
    alt="조르주 쇠라"title="그랑 차트 섬의 일요일 오후">
    </a>

    <br>

    <table border="1">
        <thead align="center">
        <tr><td rowspan = "8"><a href="table.html"><img src="image/모나리자.jpg" width="200" height="300"></a></td>
        <th>작품명</th><td colspan="2">모나리자</td></tr>
        <tr><th>화가</th><td colspan="2">레오나르도 다 빈치</td></tr>
        <tr><th>시대</th><td colspan="2">15세기경</td></tr>
        <tr><th>기법</th><td colspan = "2">패널에 유채</td></tr>
        <tr><th>크기</th><td colspan = "2">77 x 53</td></tr>
        <tr><th rowspan="2">가<br>격</th><th>정가</th><td>700억원</td></tr>
        <tr><th>판매가</th><td>500억원</td></tr>
        <tr><th>소장기관</th><td colspan="2">루브르박물관</td></tr>
        </thead>
    </table>
</body>
</html>
~~~

## 이미지 맵
- 하나의 이미지에 여러 개의 링크를 만들어 놓고 각 영역마다 다른 링크 연결
- \<img> 태그의 usemap속성
  - 이미지 맵 지정
  - 사용방법
    - \<map> 태그를 이용해 이미지 맵을 만들고
    - \<img> 태그의 usemap 속성으로 이미지 맵 지정

#### 이미지맵 예제

- imgmap.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>이미지 맵</title>
</head>
<body>
    <div id="wrap">
        <img src="image/메인.png" border="1" usemap="#cityMap">
        <map name="cityMap">
            <area shape="rect" coords = "60, 90, 250, 150" href="newyork.html">
            <area shape="rect" coords = "310, 90, 500, 150" href="paris.html">
            <area shape="rect" coords = "560, 90, 750, 150" href="roma.html">
            <area shape="rect" coords = "810, 90, 1000, 150" href="beijing.html">			
        </map>		
    </div>
</body>
</html>
~~~

# FrontEnd_day1 정리 (2021.12.02 목요일)

## 문서 삽입 태그 : \<iframe> 태그
- \<iframe> 태그
  - 현재의 html 문서 내에 다른 문서 포함
  - \<iframe> 태그를 만들어서 영역을 만들어 놓고 \<map>의 \<area>에서 target="iframe이름" 지정
  - \<iframe>의 위치 설정 중요 (css로 크기, 위치 등 속성 설정)

##### 문서 삽입 태그 예제

- iframe.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>이미지 맵</title>
    <style>
        #bigBox { margin:0 auto; width:1024px;}
		#box2 { position:absolute; margin-left:250px; top:270px;}
		iframe {width:580px; height:480px; border:none;}
    </style>
</head>
<body>
    <div id="bigBox">
        <div id="box1">
            <img src="image/메인.png" border="1" usemap="#cityMap">
            <map name="cityMap">
                <area shape="rect" coords = "60, 90, 250, 150" href="newyork.html" target="iFrameArea">
                <area shape="rect" coords = "310, 90, 500, 150" href="paris.html" target="iFrameArea">
                <area shape="rect" coords = "560, 90, 750, 150" href="roma.html" target="iFrameArea">
                <area shape="rect" coords = "810, 90, 1000, 150" href="beijing.html" target="iFrameArea">			
            </map>		
        </div>
        <div id="box2">
            <iframe name="iFrameArea"></iframe>
        </div>
    </div>
</body>
</html>
~~~

# FrontEnd_day1 정리 (2021.12.02 목요일)

## 미디어 태그

### 오디오 태그
- \<audio>
- 오디오 파일 재생
- 속성
  - src : 경로
  - preload : 재생 전 모두 다운로드
  - autoplay : 자동 재생
  - loop : 반복 재생
  - controls : 재생 도구 출력
  - \<audio src=”audio.mp3” preload=”auto” controls loop>
- \<source>
  - 미디어 파일 지정
  - 여러 미디어 파일을 한꺼번에 지정
  - 브라우저에 따라 지원하는 오디오나 비디오 코덱이 다르기 때문에 한 가지 파일만 사용했을 경우 일부 브라우저에서 지원하지 않는 경우 발생
  - 여러 유형의 미디어 파일 지정해야 함
  - \<audio> \<source src="a.ogg" type="audio/ogg"> \</audio>
  - \<audio> \<source src=”a.mp3” type=”audio/mpec”> \</audio>

##### 오디오 태그 예제

- audio.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div>
        <audio src="media/audio.mp3" preload="auto" controls loop></audio>
    </div>
</body>
</html>
~~~

### 비디오 태그
- \<video>
- mp4, ogv, webm 파일 형식
- 속성
  - src : 경로
  - preload : 재생 전 모두 다운로드
  - autoplay : 자동 재생
  - loop : 반복 재생
  - controls : 재생 도구 출력
  - poster : 비디오 준비 중일 때의 이미지 파일 경로 지정

### 자막 태그
- \<track>
- 자막 표시
- WebVTT 형식 파일(.vvt)
- Web Video Text Tracks

##### 비디오&자막 태그 예제

- video.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div>
        <video src="media/Wildlife.mp4" poster="media/poster.jpg" width="640" height="360" controls>
            <track src="media/track.vtt" kind="captions" srclang="ko" label="korean"></track>
        </video>
    </div>
</body>
</html>
~~~

# FrontEnd_day1 정리 (2021.12.02 목요일)

## 입력 양식 태그
- 입력 양식(form)을 만들 때 사용하는 태그
- 모든 입력 태그에서
  - name 속성 : 서버에 전달될 때 서버에서 인식하는 이름
  - id 속성 : 자바스크립트, jQuery에서 객체로 선택해 올 때 인식하는 이름
- \<form>
  - 입력 양식을 구성하는 기본 골격 제공
  - \<form method=”post” action=”newMember.jsp”>
    다양한 입력 양식 태그 포함 
    \<input type=”text” name=”id”>
    \</form>
- \<label>
  - 폼 요소에 캡션(라벨) 붙이기
  - \<label>\</label>
- \<input>
  - 데이터를 입력 받기 위한 태그
  - \<input type="text" id="id" name="id">
  - 속성
    - name : 입력상자의 이름(속성값 : 문자열)
    - type : 입력 유형(속성값 : text, password, checkbox, radio)
    - size : 입력 상자의 크기(속성값 : 숫자)
    - value : 초기값/태그가 지닌 값(속성값 : 문자열)
    - maxlength : 최대 길이(속성값 : 숫자)
    - placeholder : 입력할 내용의 힌트 표시(속성값 : 문자열)
    - readonly : 읽기 전용 필드
    - autocomplete : 자동 완성 기능 제어(속성값:on/off)
    - required : 필수 필드 지정
    - autofocus : 입력 커서 표시
    - hidden : 숨김(사용자에게는 보이지 않지만, 서버로 넘겨지는 값을 갖는 필드)
  - type 속성에서 사용 가능한 유형
    - \<input type="submit" value="회원가입">
    - __입력된 값들을 서버로 전송하게 하는 submit이벤트 발생__
    - text : 한 줄의 텍스트 입력
    - password : 비밀번호 입력
    - checkbox : 체크박스 (여러 개 선택 가능)
    - radio : 라디오버튼(1개만 선택 가능)
    - button : 버튼
    - file : 파일을 첨부할 수 있는 버튼
    - image : submit 버튼 대신 사용할 이미지 삽입
    - submit : 서버 전송 버튼
    - reset : 리셋 버튼
  - 라디오 버튼 (radio)
    - 여러 항목 중에 한 개를 선택할 때 사용
    - \<input type=”radio” name=”year” value=”1”>1학년
    - \<input type=”radio” name=”year” value=”4” checked>4학년
    - name : 그룹 이름
    - value : 선택한 버튼의 값 (서버로 전송되는 값)
    - checked : 처음부터 선택된 상태로 만들기

  - 체크박스(checkbox)
    - 여러 항목 중에 여러 개를 선택할 때 사용
    - \<input type=”checkbox” name=”hobby” value=”게임” checked>게임
    - \<input type=”checkbox” name=”hobby” value=”영화”>영화
    - name 속성을 동일하게 사용해도 되고 다른 이름이도 해도 됨
    - 일반적으로 동일으로 하고 전송 받을 때 배열로 처리 (선택한 개수 만큼의 값이 전달하고, 개수 크기의 배열로 생성)

- \<select> \<option>
  - 드롭다운 목록 표시

~~~html
<select name="nation">
				<option value="미국">미국</option>
				<option value="중국">중국</option>
				<option value="호주" selected”>호주</option>
</select>
~~~

- \<textarea>
 - 여러 라인 입력
   - rows : 텍스트 영역의 세로 길이
   - cols : 텍스트 영역의 가로 길이
   - \<textarea rows="10" cols="50" name="content">\</textarea>

##### 입력 양식 태그 예

- form.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>입력 양식 태그</title>
</head>
	<body>
		<form method="post" action="newMember.jsp">
			label 태그 사용하지 않음<p>
			성명 <input type="text" id="name" name="name" size="10" autofocus><br>
			
			hidden 태그
			<input type="text" id="prdNo" hidden>
			<hr>
		
		   힌트 출력<p>
		   <input type="text" name="id" size="10" placeholder="아이디"><br>
		   <hr>
		   
		   label 태그 사용 <p>
		   <label>성명 <input type="text" name="name" size="10" placeholder="아이디"></label><br><br>
		  <label>성명 <input type="text" name="name" size="10" placeholder="아이디"></label><br><br>
		  <label>우편번호 <input type="text" name="zipcode" value="12345" readonly></label><br><br>
		  <label>주소 <input type="text" name="address" required></label><br><br>
		  <label>비밀번호 <input type="password" name="passwd"size="10" ></label><br><br>
		  <hr>
		  
		   학년
		   <label><input type="radio"  value=”1” >1학년</label> 
		   <label><input type="radio" value=”2” >2학년</label> 
		   <label><input type= "radio" value=”3” >3학년</label> 
		   <label><input type="radio" name=”year” value=”4” checked>4학년</label><br><br>
		   <hr>
		   
		   차이점? label 태그로 텍스트까지 감싸주면 클릭 영역이 텍스트까지 확장 (클릭 영역을 넓힐 수 있음)<br>
		  <input type="radio"  value=”1” >1학년<br>
		   <label><input type="radio"  value=”1” >1학년</label><br><br> 
		   
		   
		   <label><input type="checkbox" name=”hobby” value=”게임” checked>게임</label>
           <label><input type="checkbox"  name=”hobby” value=”영화”>영화</label>
           <label><input type="checkbox" name=”hobby” value=”독서”>독서</label>
           <label><input type="checkbox" name=”hobby” value=”운동”>운동</label><br><br>
           
           
           여행하고 싶은 나라 :
           <select name="nation">
				<option value="미국">미국</option>
				<option value="중국">중국</option>
				<option value="호주" selected>호주</option>
			</select><br><br>
			
			자기 소개 : <br>
			<textarea rows="10" cols="50" name="content"></textarea><br><br>
           
		   첨부 파일 선택 : <input type="file" size="30"><br><br>
		   
		   <input type="button" value="아이디 중복 확인"><br><br>
		   
		   <input type="image" id="cartImg" src="image/cart.jpg"><br><br>
		   
		    <input type="email"><br><br>
		    
		    <input type="submit" value="회원가입">  <input type="reset" value="취소">  
		</form>
	</body>
</html>
~~~

# FrontEnd_day1 정리 (2021.12.02 목요일)

## 공간 분할 태그
- \<div>
  - block 형식으로 공간 분할
- \<span>
  - inline 형식으로 공간 분할

## 사진

~~~html
<div>div1</div>
<div>div2</div>
<div>div3</div>
<div>div4</div>

<br>
<span>span1</span>
<span>span2</span>
<span>span3</span>
<span>span4</span>
~~~

## 사진

~~~html
<!-- div 중첩 사용 -->
<div>
    <div></div>
    <div></div>
    <div></div>
</div>
~~~

# FrontEnd_day1 정리 (2021.12.02 목요일)

## HTML5 시멘틱 구조 태그
- 시멘틱(Semantic) : 의미의, 의미론적인
- 역할과 기능에 맞는 요소로 영역 구분해서 사용
- 각 요소(태그)가 의미가 있다는 것
  - \<header> : 헤더 (제목)
  - \<nav> : 내비게이션 (메뉴)
  - \<aside> : 사이드 바
  - \<section> : 컨텐츠 (내용)
  - \<article> : 컨텐츠 안의 내용 (컨텐츠 영역을 세분화)
  - \<footer> : 푸터 (주소 / 연락처 / 저작권 등)

## 사진 두 장

- HTML5 시멘틱 구조의 특징
  - HTML4로 만든 웹 문서의 결과 화면이나 HTML5로 만든 웹 문서의 결과 화면만 보면 웹 브라우저에 보이는 모습은 동일하지만 실제로 웹 브라우저에서 문서를 처리할 때 큰 차이

- HTML5 시멘틱 구조의 장점
  - 소스만으로도 문서 내용 쉽게 이해
  - 태그만 보고도 어느 부분이 제목이고, 메뉴이고, 실제 내용인지 쉽게 구분
  - 편리한 검색
  - 사이트 검색 시 필요한 내용을 정확하게 찾을 수 있어 편리
  - \<header>나 \<nav> 태그 영역은 검색하지 않고
  - \<section>이나 \<article> 태그 영역만 찾아서 검색
  - 뛰어난 웹 접근성
  - 시각 장애인들이 웹 보조 기구로 사용하는 화면 판독기에서 시멘틱 태그를 통해 제목과 내용을 구별하여 사용자에게 정확한 내용 전달 가능
  - 다양한 장치에 통일된 결과 제공
  - 태그의 역할이 정해져있기 때문에 어떤 장치에서든 동일하게 문서 해독이 가능