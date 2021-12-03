# FrontEnd_day2 정리 (2021.12.03 금요일)

## 스타일 시트(CSS)
- Cascading Style Sheets : 계단형 스타일 시트
- 단계적으로 스타일 적용
- 여러 스타일이 겹치면 맨 마지막 스타일 적용
- HTML의 레이아웃 배치 등의 한계를 보완하기 위해 개발된 독립 언어
- 일정 기능들을 미리 지정하여 여러 부분에서 동일하게 적용 가능
- 가능한 작업
  - HTML문서 내의 폰트, 크기, 색상, 배경, 테두리, 레이아웃 배치, 여백 등 지정
  - 정렬 방식, 그림자, 동적 기능 등 다양한 효과
- 장점
  - 자유롭게 원하는 형태로 웹 문서 편집 가능
  - 통일감 있는 문서 작성
    - 한 번만 정의하여 문서에 일관되게 적용 가능
  - 편리한 문서 관리
    - 외부 스타일 시트 파일을 사용하여, 여러 웹 문서에 동일한 스타일 시트 사용 가능
    - 한 번만 한 곳에서 수정하여 모든 웹 문서의 스타일을 동시에 변경 가능
- 적용 방법
  - 문서 내부에 정의(Embedded Style)
  - 외부 문서에서 연결(Linked Style)
  - 태그에 직접 정의(Inline Style)

### 문서 내부에 정의
- \<head> 태그에 삽입
- 문서 전체에 특정 효과 주기 위해 사용

~~~html
<head>
    <style type="text/css">
        태그명 {속성:값;}
    </style>
</head>
~~~

### 외부 문서에서 연결
- 별도의 스타일 시트 문서를 만들어 놓고 필요한 HTML에 연결하여 사용
- 웹 사이트의 모든 문서에 동일한 효과를 저용하여 웹 사이트에 통일감을 주고 편리하게 관리 가능.

~~~html
<head>
    <<link rel="stylesheet" type="text/css" href="파일명">
</head>
~~~

### 태그에 직접 정의
- 특정 태그에만 스타일을 적용할 때 사용

~~~html
<body style="font-size; 15pt; color:blue;">
<button onclick="green()" style="width:120; height:30;">
<태그명 style="속성:값;">
~~~

### 다중 스타일 시트
- 하나의 요소에 대하여 외부, 내부, 인라인 스타일이 서로 다르게 지정되어 있는 경우 적용되는 스타일
- 맨 마지막 스타일 적용됨(덮어씀)
- 스타일 적용 순서
  1. 웹브라우저 디폴트 값
  2. 외부 스타일
  3. \<head> 부분의 내부 스타일
  4. 태그에 직접 정의된 인라인 스타일(제일 우선순위가 늦다)

## 스타일 시트의 기본 형식
- 선택자(selector)
  - 스타일을 적용할 대상
  - HTML 문서의 태그, 아이디, 클래스, 속성
- {속성명 : 값;}
  - 변경하고자 하는 속성
  - 폰트, 크기, 색상 등
- 사용 예
  - 모든 \<h1> 태그에 스타일 적용
  - h1{ color:red; }

# FrontEnd_day2 정리 (2021.12.03 금요일)

## CSS 선택자 유형
### 태그 선택자
- 태그명 사용
- 요소(element) 선택자라고도 함
- HTML문서에 있는 모든 같은 태그에 동일하게 적용
- 태그명 {속성명:값;}

~~~html
h3 {
    background-color:#000;
    color:#fff;
    width:50%;
    margin-left:20px;
}
~~~

~~~html
<!doctype html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>태그 선택자</title>
		<style type="text/css">
			/* h3 태그에 스타일 적용 css 주석은 이렇게 사용 */
			h3 {
			background-color:#000;
			color:#fff;
			width:50%;
			margin-left:20px;
		}
		</style>
		
		
	</head>

	<body>
		<h1>태그 선택자 사용하기</h1>
		<hr>
		<h2>두부감자조림</h2> 
		<h3>재료</h3>
		<ul>
			<li>감자 1개</li>
			<li>두부 1/2모</li>
			<li>꽈리고추 10개</li>
			<li>홍고추 1개</li>
		</ul>
		<h3>조리법</h3>
		<ol>
			<li>감자는 껍질을 벗기고 돌려가면서 어슷하게 썰어 찬물에 담가놓고 두부는 도톰하게 한입크기로 썰며 꽈리고추, 홍고추는 어슷썬다.</li>
			<li>첫번째 썰은 재료에 두부를 팬에 기름을 두르고 노릇노릇하게 앞뒤로 지져 기름은 뺀다.</li>
			<li>냄비에 감자와 홍고추를 담고 조림장을 반분량만 넣는다.</li>
			<li>3번째를 끓이다가 감자가 반정도 익으면, 두부와 남은 양념장을 넣는다.</li>
			<li>윤기나게 졸여지면 꽈리고추를 마지막에 넣어 다시한번 살짝 졸여 조린다.</li>
		</ol>
	</body>
</html>
~~~

### 아이디 선택자
- #을 사용
- 문서에서 트정 부분에만 필요한 스타일 적용할 때 사용
- 필요한 부분에 유일한 아이디를 지정하고 CSS 적용
- 식별 선택자라고도 함
- 사용법
  - #idName{속성명:값;}
  - 태그에 반드시 id로 지정되어 있어야 함.
  - \<태그명 id="idName"> \</태그명>

~~~html
<!doctype html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>아이디 선택자 사용하기</title>
		<style type="text/css">
		#cookBox {
			border: 3px solid #000; /*테두리 굵기 유형 색상(순서는 상관 없지만 저긴 저런 폼으로 작성됨)*/
			width: 500px;
			padding: 10px; /*안쪽 여백*/
			margin-left: 70px; /*바깥쪽 여백*/
			font-size: 12pt;
			color:#777;
			background-color:gold;
		}
		#sourceBox {
			background-color: #ffc;
			line-height: 150%; /*행 높이*/
			list-style: none; /*목록(리스트) 글머리 기호 안 보이게*/
			width: 200px;
			color: red;
			padding: 5px;
			border: 1px solid #000;
			margin-left: 30px;

		}
		</style>
	</head>

	<body>
		<h1>아이디 선택자 사용하기</h1>
		<hr>
		<div id="cookBox">
			<h2>도가니탕</h2> 
			<h3>재료-4인분 기준</h3>
			<ul id="sourceBox">
				<li>도가니 1개</li>
				<li>양지머리 300g</li>
				<li>무 200g</li>
				<li>마늘 5쪽</li>
				<li>대파 3뿌리</li>
				<li>생강 1쪽</li>
			</ul>
			<h3>조리법</h3>
			<ol>
				<li>도가니(무릎뼈)는 뼈 부분을 4∼5 등분으로 잘라 깨끗이 씻어 놓는다. </li>
				<li>양지머리는 물에 한번 씻어 놓는다.</li>
				<li>무는 3cm 두께로 둥글게 썰어 놓는다. </li>
				<li>솥에 물을 붓고 도가니와 마늘, 양지머리, 파, 저민 생강을 넣고불에 올려놓아 끓기 시작하면 중간 불에서 2∼3시간 정도 서서히 고면서 중간에 무 토막을 넣어 함께 끊인다. </li>
				<li>양지머리와 무가 푹 익었으면 건져서 먹기 좋게 썰어 다시 솥에 넣고 소금으로 간을 한다. </li>
				<li>도가니를 끊인 국물이 뽀얗게 우러나면 뚝배기나 탕그릇에 고기와 무를 담아 국물을 붓고 대파를 송송 썰어 얹어 낸다.</li>
			</ol>
		</div>
	</body>
</html>
~~~

### 클래스 선택자
- . 사용(도트 선택자)
- 문서에서 특정 그룹에 필요한 스타일 적용할 때 사용
- .className{속성명:값;}
- HTML 태그의 class속성이 지정되어 있어야 함
  - \<태그명 class="className">\</태그명>

~~~html
<!doctype html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>클래스 선택자 사용하기</title>
		<style type="text/css">
			.cookTitle {
				background-color: #f03;
				color:#fff;
				padding: 5px;
				border: 1px solid #000;
				margin-left: 20px;
			}
			.cookTitle2 {
				background-color: #ffcc33;
				padding: 5px;
				border: 1px solid #f00;
				margin-left: 20px;
			}
			.redDotLine {
				color:#f00;
				font-weight: bold;
				border-bottom: 1px dashed #f00;
			}
		</style>	
	</head>

	<body>
		<h1>클래스 선택자 사용하기</h1>
		<hr>
		<h2>닭칼국수</h2> 
		<h3 class="cookTitle">재료-4인분 기준</h3>
		<ul>
			<li>밀가루 3컵</li>
			<li>닭 1/2마리 </li>
			<li>호박 1/2개 </li>
			<li>부추 50g</li>
			<li>생강,소금, 후추, 참기름</li>
		</ul>
		<h3 class="cookTitle2">조리법</h3>
		<ol>
			<li><span class="redDotLine">밀가루</span>에 <span class="redDotLine">소금과 달걀</span>을 넣고 반죽하여 밀대로 밀어 0.5cm 두께로 썬다.쟁반에 펼쳐 굳지 않게 가제로 덮어놓는다 </li>
			<li>첫번째 썰은 재료에 두부를 팬에 기름을 두르고 노릇노릇하게 앞뒤로 지져 기름은 뺀다. </li>
			<li>닭은 내장과 필요없는 지방을 제거하고 깨끗이 씻는다.생강을 저며 넣고 찬물을 부어 푹 삶아 닭고기는 살을 곱게 찢어 소금, 후추, 참기름에 양념하여 무쳐 놓고 국물은 가제로 걸러 육수로 사용한다. </li>
			<li>호박은 채 썰고 부추도 다듬어 씻어 4cm 길이로 썰고, 홍고추, 파, 마늘은 곱게 다진다.간장, 깨소금, 참기름을 섞어 양념장을 만든다. </li>
			<li>닭국물이 끓으면 썰어 놓은 칼국수를 넣어 서로 붙지 않게 한소끔 끓인 다음 호박과 부추, <span class="redDotLine">양념한 닭고기</span>를 넣고 다시 한소끔 끓여서 양념장과 김치를 곁들여 먹는다.</li>
		</ol>
	</body>
</html>
~~~

### 속성 선택자
- HTML 태그의 속성 값에 따라 선택자로 정의
- \<a title="산업기사">산업기사\</title>
- 예: \<a> 속성 값으로 선택해서 스타일 지정
- 문법
  - 태그명[속성명=”값”]
  - 태그명[속성명^=”값”]
  - 태그명[속성명$=”값”]
  - 태그명[속성명*=”값”]

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>속성 선택자</title>
    <style>
        a[href="http://www.naver.com"] {
            color:green;
            /*a 태그의 href 속성에 스타일 적용*/
        }
        /* a 태그의 href속성 값 중에 #으로 시작하는 속성 값에 스타일 적용 */
        a[href^="#"] {
            background-color: gold;
        }

    </style>
</head>
<body>
    <h3>사이트로 이동</h3>
    <a href="http://www.naver.com">네이버로 이동</a>
    <h3>다른 문서로 이동</h3>
    <a href="first.html">index로 이동</a>
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

### 상태 선택자
- 태그의 상태로 선택해서 스타일 적용
- 상태 : 체크된 상태, 포커스 받은 상태, 사용 가능 또는 불가능한 상태
- 선택자:checked - 체크된 input 태그 선택
- 선택자:focus - 포커스를 받은 input 태그 선택
- 선택자:enabled - 사용 가능한 input 태그 선택
- 선택자:disabled - 사용 불가능한 input 태그 선택

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>상태 선택자</title>
    <style type="text/css">
        input:enabled{background-color: white;}
        input:disabled{background-color: black;}
        input:focus{background-color: orange;}
    </style>
</head>
<body>
    <h2>사용 가능</h2>
    비밀번호 : <input type="password" size="10">
    <h2>사용 불가능</h2>
    아이디 : <input type="text" size="10" value="abcd" disabled>
</body>
</html>
~~~

### 자식 / 자손 선택자(상속 선택자)
- 자식/자손 개념
## 사진
- 자식 선택자 : > 부호 사용
  - 선택자 > 자식 선택자
  - 선택자A > 선택자B
  - #header > h1
- 자손(후손) 선택자 : 띄어 쓰기(스페이스바)
  - 선택자 자손선택자
  - 선택자A 선택자B
  - #header h1
  - #pageNev ul li a:hover

### first-child 선택자
- 첫 번째 자손 선택
  - .wrap div:first-child
- 두 번째 자손 선택
 - .wrap div:first-child+div
- 또는 .wrap div:nth-child(n)

## 사진

~~~html
<style type="text/css">
        /* content의 모든 자손 */
        #content div {
            width: 400px;
            height: 50px;
            border: solid 1px black;
        }
        /* 첫 번째 자손 */
        #content div:first-child {
            background-color: yellow;
        }
        /* 두 번째 자손 */
        #content div:first-child + div {
            background-color: green;
        }
        /* 세 번째 자손 */
        #content div:nth-child(3) {
            background-color: gold;
        }
        /* 네 번째 자손 */
        #content div:nth-child(4) {
            background-color: pink;
        }
        /* div :nth-child(4) < 와 같이 콜론 전/후로 띄어쓰기는 하면 안됨.*/
    </style>
~~~

##### nth-child 예제

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style type="text/css">
        #stdTable {
            margin: 0 auto;
            border-collapse: collapse;
        }
        #stdTable th {color: white; background-color: blue;}
        #stdTable th.name {width: 100px;}
        #stdTable th.email {width: 200px;}
        #stdTable td {height: 20px;}
        /* 짝수 행 선택 */
        #stdTable tr:nth-child(3n) td {
            background-color: yellow;

        }
    </style>
</head>
<body>
    <table id="stdTable" border="1">
        <tr><th class="name">이름</th><th class="email">이메일</th></tr>
        <tr><td><td></td></td></tr>
        <tr><td><td></td></td></tr>
        <tr><td><td></td></td></tr>
        <tr><td><td></td></td></tr>
        <tr><td><td></td></td></tr>
        <tr><td><td></td></td></tr>
        <tr><td><td></td></td></tr>
        <tr><td><td></td></td></tr>
        <tr><td><td></td></td></tr>
        <tr><td><td></td></td></tr>
    </table>
</body>
</html>
~~~

### 동적 반응 선택자
- active
  - 마우스를 클릭한 태그 선택
- hover
  - 마우스를 올린 태그

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style type="text/css">
        /* content의 모든 자손 */
        #content div {
            display: inline-block;
            background: blue;
            width: 100px;
            height: 50px;
        }
        /* 마우스 올렸을 때 */
        #content div:hover {
            background: yellow;
        }
        #content div:active {
            background: red;
        }
    </style>
</head>
<body>
    <div id="content">
        <div></div><div></div><div></div><div></div>
    </div>
</body>
</html>
~~~

# FrontEnd_day2 정리 (2021.12.03 금요일)

## CSS속성
- 텍스트속성
- 배경 색상 / 이미지 관련 속성
- 테두리 속성
- 여백 속성
- display 속성 : inline / block / inline-block
- float 속성
- 목록 관련 속성
- 위치 관련 속성
- 겹침 (레이어)
- overflow
- visibility / opacity
- 그림자

### 텍스트 속성
- font-family : "굴림", "맑은 고딕"; /* 1순위 2순위, ... */
- font-size : 40px;
- color : blue; /* 글자색 */
- font-style : italic;
- font-weight : bold; /* 굵게 */
- text-decoration : underline;
- letter-spacing : 3px; /* 글자 사이 간격 */
- word-spacing : 5px; /” 단어 사이 간격 */
- line-height:10px; /* 줄 간격 */
- text-align : center;
- text-shadow : 2px 2px 2px black; /*(가로 세로 크기 색상) */

### 배경 색
- background-color : #00ff00;
- background-color : #333;
- background-color : rgb(0,255,0);
- background-color : green;

### 배경 이미지 / 반복
- background-image : url(back.png);
- background-repeat : repeat;
- background-repeat : no-repeat;
- background-repeat : repeat-x;
- background-repeat : repeat-y;

### 테두리 속성
- border:solid 1px red;
- border-style : solid;
- border-width : 3px; /* thin medium thick */
- border-left : dotted;
- border-right : double;
- border-bottom : dashed;
- border-top : solid;
- border-color : red:;
- border-radius : 10px; /* 모서리 둥글게 */
- border-bottom-right-radius : 50px;

### 여백 속성

## 사진

### display 속성
- display 속성이 없으면 block이 기본 값이 된다.
- block
  - 행으로 배치
  - 옆으로 나란히 배치 안 됨
  - 여백 있음

##### 사진

- inline
  - 옆으로 나란히 배치
   - 여백 없이 내용물 만큼만 공간 차지

##### 사진

- inline-block
  - 인라인, 블록의 성격 모두 포함
  - 옆으로 나란히 배치되면서 여백도 있음

##### 사진

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .greenbox {
            /* display속성이 없으면 block이 디폴트(행으로 배치, 여백 있음) */
            /* display: block;  디폴트 */
            /* display: inline; 옆으로 배치, 내용만큼만 공간 차지 */
            display: inline-block; /* 옆으로 배치, 여백 있음 */
            width: 150px;
            height: 75px;
            margin: 10px;
            border: solid 3px #73AD21;
        }
    </style>
</head>
<body>
    <h2>dispaly 속성 (block/inline/inline-block)</h2>

    <div class="greenbox">박스 1</div>
    <div class="greenbox">박스 2</div>
    <div class="greenbox">박스 3</div>
    <div class="greenbox">박스 4</div>
</body>
</html>
~~~

### float 속성
- 해당 요소를 떠 있게 만든 속성
- 기본 레이아웃 흐름에서 벗어나 왼쪽이나, 오른쪽으로 이동하는 것을 의미
- left : 왼쪽에 배치
- right : 오른쪽에 배치

~~~html
<style>
        .greenbox {
            /* display속성이 없으면 block이 디폴트(행으로 배치, 여백 있음) */
            /* display: block;  디폴트 */
            /* display: inline; 옆으로 배치, 내용만큼만 공간 차지 */
            /* display: inline-block; 옆으로 배치, 여백 있음 */
            float: right;
            width: 150px;
            height: 75px;
            margin: 10px;
            border: solid 3px #73AD21;
        }
    </style>
~~~

### 목록 관련 속성

## 사진

~~~html
/*
...
*/
 <style type="text/css"> 
    /* ul{list-style-type: none;} */
    ul li {display: inline;}
    </style>
</head>
<body>
    <ul>
        <li>봄</li>
        <li>여름</li>
        <li>가을</li>
        <li>겨울</li>
    </ul>
</body>
</html>
~~~

### 위치 관련 속성
- position 속성
- static
  - 디폴트
  - 다른 요소와 겹치지 않게 배치
  - 위치를 지정하지 않으면 static 적용
- relative
  - static의 원래 위치를 기준으로 위치 계산
## 사진
- absolute
  - 가장 가까운 상위 요소(부모)를 기준으로 배치
  - 상위 요소가 static인 경우에는 브라우저 화면 기준
## 사진
  - 상위 요소가 static이 아닌 경우 부모를 기준으로
## 사진
  - 정리
    - div를 parent내에 위치시키기 위해서는 parent의 position을 설정(absolute or relative 상관 없음)
    - absolute과 relative의 차이는 약간의 여백
      - 문서 전체에서 margin을 0px로 설정하면 여백이 사라짐.
        - body{margin:0;} 또는 {margin:0;}

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style type="text/css">
        #parent {
            /* 위치 지정하지 않음 */
            position: absolute;
            top: 0px;
            left: 0px;
            width: 200px;
            height: 300px;
            border: solid 5px #000000;
        }
        #boxA, #boxB, #boxC {
            width: 80px;
            height: 80px;
        }
        #boxA {background-color: #ff0000;}
        #boxB {background-color: #00ff00;}
        #boxC {background-color: #fff000;}

        #boxB {
            /* relative : static에 해당되는 원래 위치를 기준으로
            20, 30 만큼 이동 */
        /* position: relative;  */
        /* absolute : 상위 요소 위치 지정 안했기 때문에 브라우저 기준으로 20, 30만큼 이동 */
        position: absolute;
        top: 20px;
        left:30px;
        }
    </style>
</head>
<body>
    <div id="parent">
        <div id="boxA">A</div>
        <div id="boxB">B</div>
        <div id="boxC">C</div>
    </div>
</body>
</html>
~~~

- fixed
  - 브라우저 화면을 기준으로 고정 위치에 배치
  - 스크롤 시에도 고정되어 있음.

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style type="text/css">
        #fixedBox {
            position: fixed;
            width: 50px;
            height: 50px;
            background-color: blue;
            top: 50px;
            left: 50px;

        }
    </style>
</head>
<body>
    <div id="fixedBox"></div>
    <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
    <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
    문서 끝
</body>
</html>
~~~

### 겹침(레이어) 표현 속성
- z-index 속성
  - 요소들이 겹칠 때 순서 지정
  - 나중에 배치하는 것이 위에 놓임
  - z-index 값이 클수록 위에 놓임

## 사진

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style type="text/css">
        #outBox {
            margin: 0 auto; /* 브라우저 화면의 가운데 정렬 */
            width: 1020px;
            position: relative;/* absolute인 경우 가운데 정렬 안 됨 */
        }
        #box1{
            position: absolute; /* 부모 박스 기준으로 배치 */
            left: 25px;
            top: 181px;
            z-index: 1;
        }
        #box2{
            position: absolute; /* 부모 박스 기준으로 배치 */
            left: 187px;
            top: 155px;
            z-index: 2;
        }
        #box3{
            position: absolute; /* 부모 박스 기준으로 배치 */
            left: 369px;
            top: 129px;
            z-index: 3;
        }
        #box4{
            position: absolute; /* 부모 박스 기준으로 배치 */
            left: 603px;
            top: 155px;
            z-index: 4;
        }
        #box5{
            position: absolute; /* 부모 박스 기준으로 배치 */
            left: 795px;
            top: 181px;
            z-index: 5;
        }
    </style>
</head>
<body>
    <div id="outBox">
        <div id="box1"><img src="image/img1.png"></div>
        <div id="box2"><img src="image/img2.png"></div>
        <div id="box3"><img src="image/img3.png"></div>
        <div id="box4"><img src="image/img4.png"></div>
        <div id="box5"><img src="image/img5.png"></div>
    </div>
</body>
</html>
~~~

### Overflow
- 자식 요소가 부모 요소의 범위를 벗어났을 때
- 어떻게 처리할 것인지 지정
- hidden : 부모 영역을 벗어나는 부분은 보이지 않게 처리
- scroll : 스크롤바 표시 (가로 / 세로)
- auto : 자동으로 필요한 부분에만 스크롤바 표시

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style type="text/css">
        div {
            width: 200px;
            height: 175px;
            border: 1px black;
            /* overflow: hidden;
            overflow: scroll;
            overflow: auto; */
        }
    </style>
</head>
<body>
    <div>
        <img src="image/fashion1.png">
        <img src="image/fashion2.png">
        <img src="image/fashion3.png">
    </div>
</body>
</html>
~~~

### 투명도 / 가시성
- 투명도
  - opacity
    - 0 ~ 1 사이의 값 지정
    - 0 = 투명
    - 1 = 불투명
    - 0.5 = 반투명
- 가시성
  - visibility
    - hidden = 숨김
    - visible = 보임

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        /* 마우스 올렸을 때 */
        #f1:hover {opacity: 0.5;}
        /* 마우스 클릭했을 때 */
        #f1:active {opacity: 1;}
        /* 마우스 클릭했을 때 */
        #f2:active {visibility: hidden;}
    </style>
</head>
<body>
    <img id="f1" src="image/fashion1.png">
    <img id="f2" src="image/fashion2.png">
</body>
</html>
~~~

### 그림자 효과
- box-shadow
- none : 그림자 없음
- x-position : 가로 위치에 그림자 표시(양수-오른쪽, 음수-왼쪽)
- y-position : 세로 위치에 그림자 표시(양수-아래쪽, 음수-위쪽)
- blur : 흐릿하게 표시 값이 클수록 더 흐림
- color : 그림자 색상
- inset : 그림자를 요소의 안쪽에 표시

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div.polaroid { 
            width: 300px;
            height: 300px;
            background: white;
            box-shadow: 10px 4px 8px 0 rgba(0, 0, 0, 0.3);
            margin-bottom: 15px;
        }
        div.container {
            text-align: center;
            padding: 5px 5px;

        }
        img {
            width: 100%;
            height: 230px;
        }
    </style>
</head>
<body>
    <div class="polaroid">
        <img src="image/pic1.jpg">
        <div class="container">
            <p>카드놀이 하는 사람들</p>
        </div>
    </div>

    <div class="polaroid">
        <img src="image/pic2.jpg">
        <div class="container">
            <p>길가의 집</p>
        </div>
    </div>
</body>
</html>
~~~

# FrontEnd_day2 정리 (2021.12.03 금요일)

## CSS 파일로 HTML 문서 외부에 정의
- CSS 파일 인코딩 UTF-8
- CSS 파일 생성
- HTML : \<link...>

~~~html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="external.css">
</head>
~~~