# FrontEnd_day3 정리 (2021.12.06 월요일)

## CSS 예제

### cssEx1.html(테이블 사용)

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>CSS 예제</title>
		<link href="cssEx1.css" rel="stylesheet">
	</head>
	<body>
		<div id="wrap">
			<div id="mainMenuBox">
				<ul id="menuItem">
					<li><a href="#">패션잡화</a></li>
					<li><a href="#">주방용품</a></li>
					<li><a href="#">생활건강</a></li>
					<li><a href="#">DIY가구</a></li>
				</ul>
			</div>
			<div id="product">
				<table>
					<tr><td><img src="image/fashion1.png"></td>
							<td><img src="image/fashion2.png"></td>
							<td><img src="image/fashion3.png"></td></tr>
					<tr id="prdName"><td>캐주얼화<br>스니커즈</td>
												  <td>미니크로스<br>여성 가방</td>
												  <td>페이퍼플레인<br>겨울 신발</td></tr>
					<tr id="prdPrice"><td>35,000원</td>
										         <td>20,000원</td>
										         <td>25,800원</td></tr>
				</table>
			</div>
			<div id="info">
				<div class="box">
					<h4>공지사항</h4>
					<a href="#">[배송] : 무료배송 변경 안내 2021.08.25</a><br>
					<a href="#">[전시] : DIY 가구 전시 안내 2021.09.01</a><br>
					<a href="#">[판매] : 11월 특가 상품 안내 2021.11.01</a><br>
				</div>
				<div class="box">
					<h4>커뮤니티</h4>
					<a href="#">[레시피] : 살 안찌는 야식 만들기</a><br>
					<a href="#">[가구] : 헌집 새집 베스트 가구</a><br>
					<a href="#">[후기] : 배송이 잘못 됐어요 ㅠㅠ</a><br>
				</div>
			</div>
		</div>
	</body>
</html>
~~~

### cssEx1.css(테이블 사용)

~~~css
@charset "UTF-8";

#wrap {
	margin:0 auto; /* 내가 가운데 정렬 */
	width:800px;  /* 가운데 정렬하기 위해서는 width 값 있어야 함 */
	text-align:center; /* 내 안에 들어 있는 요소를 가운데 정렬  */
}

#mainMenuBox {
	height:35px;
	line-height:35px; /*  줄 간격 - 수직으로 가운데 정렬 효과 */
	background-color:#555;
	margin-top:30px;
	margin-bottom:30px;
}

#mainMenuBox ul {
	padding-left:0;
	margin:0;
	list-style:none;  /* type 없음 */
}

#mainMenuBox ul li {   /* #mainMenuBox li  */
	float:left;    /* 한 줄로 정렬  */
	text-align:center;
	width:25%;			/* 항목 4개를 동일한 너비로  */
}

#mainMenuBox a {   /* #mainMenuBox ul li a */
	text-decoration:none;    		/* <a> 태그 밑줄 없애기 */
	color:white; 				/* 글자색 흰색  */
	display:block; 			/* 여백 */
	font-size:14px;
	font-weight:bold;	
}


#mainMenuBox a:hover { 
	color:red;
	text-decoration:underline;    		/* <a> 태그 밑줄 보이기 */
	background-color:black;
}

table {
	margin:0 auto;
	width:600px;
	margin-bottom:30px;
}

#prdName {
	color:blue;
	font-weight:bold;
}

#prdPrice {
	color:red;
}

.box {
	display:inline-block; 		/* 옆으로 나란히 배치 */
	border:solid 1px grey;
	width:320px;
	height:150px;
	font-size:small;
	border-radius:10px;
	padding-left:20px;
	padding-right:20px;
	margin:10px;
	text-align:left;
}

.box a:hover {
	color:red;	
}
~~~

### cssEx2.html(div 사용)

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>CSS 예제</title>
		<link href="cssEx2.css" rel="stylesheet">
	</head>
	<body>
		<div id="wrap">
			<div id="mainMenuBox">
				<ul id="menuItem">
					<li><a href="#">패션잡화</a></li>
					<li><a href="#">주방용품</a></li>
					<li><a href="#">생활건강</a></li>
					<li><a href="#">DIY가구</a></li>
				</ul>
			</div>
			<div class="product">
				<div>
					<img src="image/fashion1.png"><br>
					<span class="prdName">캐주얼화<br>스니커즈</span><br>
					<span class="prdPrice">35,000원</span>
				</div>
				<div>
					<img src="image/fashion2.png"><br>
					<span class="prdName">미니크로스<br>여성 가방</span><br>
					<span class="prdPrice">20,000원</span>
				</div>
				<div>
					<img src="image/fashion3.png"><br>
					<span class="prdName">페이퍼플레인<br>겨울 신발</span><br>
					<span class="prdPrice">25,800원</span>
				</div>
			</div>
			<div id="info">
				<div class="box">
					<h4>공지사항</h4>
					<a href="#">[배송] : 무료배송 변경 안내 2021.08.25</a><br>
					<a href="#">[전시] : DIY 가구 전시 안내 2021.09.01</a><br>
					<a href="#">[판매] : 11월 특가 상품 안내 2021.11.01</a><br>
				</div>
				<div class="box">
					<h4>커뮤니티</h4>
					<a href="#">[레시피] : 살 안찌는 야식 만들기</a><br>
					<a href="#">[가구] : 헌집 새집 베스트 가구</a><br>
					<a href="#">[후기] : 배송이 잘못 됐어요 ㅠㅠ</a><br>
				</div>
			</div>
		</div>
	</body>
</html>
~~~

### cssEx2.css(div사용)

~~~css
@charset "UTF-8";

#wrap {
	margin:0 auto; /* 내가 가운데 정렬 */
	width:800px;  /* 가운데 정렬하기 위해서는 width 값 있어야 함 */
	text-align:center; /* 내 안에 들어 있는 요소를 가운데 정렬  */
}

#mainMenuBox {
	height:35px;
	line-height:35px; /*  줄 간격 - 수직으로 가운데 정렬 효과 */
	background-color:#555;
	margin-top:30px;
	margin-bottom:30px;
}

#mainMenuBox ul {
	padding-left:0;
	margin:0;
	list-style:none;  /* type 없음 */
}

#mainMenuBox ul li {   /* #mainMenuBox li  */
	float:left;    /* 한 줄로 정렬  */
	text-align:center;
	width:25%;			/* 항목 4개를 동일한 너비로  */
}

#mainMenuBox a {   /* #mainMenuBox ul li a */
	text-decoration:none;    		/* <a> 태그 밑줄 없애기 */
	color:white; 				/* 글자색 흰색  */
	display:block; 			/* 여백 */
	font-size:14px;
	font-weight:bold;	
}


#mainMenuBox a:hover { 
	color:red;
	text-decoration:underline;    		/* <a> 태그 밑줄 보이기 */
	background-color:black;
}


.product {
	margin-bottom:30px;
}

.product div {
	display:inline-block;
	margin:10px;
}


.prdName {
	color:blue;
	font-weight:bold;
}

.prdPrice {
	color:red;
}

.box {
	display:inline-block; 		/* 옆으로 나란히 배치 */
	border:solid 1px grey;
	width:320px;
	height:150px;
	font-size:small;
	border-radius:10px;
	padding-left:20px;
	padding-right:20px;
	margin:10px;
	text-align:left;
}

.box a:hover {
	color:red;	
}
~~~

# FrontEnd_day3 정리 (2021.12.06 월요일)

## 시멘틱 구조 예제

### index.html

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>HTML 시멘틱 구조  css 적용</title>
		<link href="index.css" rel="stylesheet">
	</head>
	<body>
		<div id="wrap">
			<header>
				<div id="topMenu"> 로그인 이벤트 장바구니 고객센터 회원가입</div>			
			</header>
			<nav>
				<div id="mainMenuBox">메뉴</div>
				<div id="subMenuBox"> 서브 메뉴</div>
			</nav>
			<section>
				<article>
					<div id="slideShowBox">슬라이드 쇼</div>
				</article>
				<article>
					<div id="content">메인 내용</div>
				</article>
			</section>
		    <footer>
		    	<div id="companyInfo">회사 정보</div>
		    </footer>		
		</div>
	</body>
</html>
~~~

### index.css

~~~css
@charset "UTF-8";

#wrap {
	margin:0 auto;
	width:1000px;
	background-color:white;
	color:white;
}

header {
	background-color:#0C3;
	text-align:right;
	padding-right:20px;
	height:40px;
	line-height:40px;
}

#mainMenuBox {
	margin-top:10px;
	margin-bottom:10px;
	height:35px;
	line-height:35px;
	background-color:orange;
	text-align:center;
	color:blue;
}

#subMenuBox {
	height:35px;
	line-height:35px;
	background-color:#FF0;
	text-align:center;
	color:blue;
}

#slideShowBox {
	margin-top:10px;
	background-color:blue;
	text-align:center;
	height:200px;
	line-height:200px;
}

#content {
	margin-top:10px;
	background-color:navy;
	text-align:center;
	height:500px;
	line-height:500px;
}

#companyInfo {
	margin-top:10px;
	background-color:black;
	color:yellow;
	text-align:center;
	height:200px;
	line-height:200px;
}
~~~

# FrontEnd_day3 정리 (2021.12.06 월요일)

## 반응형 웹

## 사진

- PC, TV, 내비게이션, 스마트 기기 등 다양한 기기의 화면이나 환경에 맞게 자유자재로 변하도록 만들어진 웹
- 반응형 웹의 장점
  - 유지보수 간편
    - 모바일 버전과 데스크 탑 버전 두개의 웹사이트를 만들게 되면 웹 사이트 수정/갱신할 때 모바일 버전과 데스크탑 버전을 개별적으로 수정해야 하므로 업무량이 늘어나고 작업 내용도 복잡
    - 모바일 버전, 태블릿 버전, 데스크탑 버전 등 모든 디자인을 하나의 HTML과 CSS 파일에서 작업하기 때문에 유지보수 용이
  - 마케팅에 유리
    - 환경이나 기기에 따라 최적화된 구조로 웹사이트를 변경해서 보여줄 수 있기 때문에 확실하게 내용 전달 가능
  - 비용면에서 효과적
    - 두 가지 버전의 웹 사이트를 만들지 않아도 되기 때문에 기업 비용 측면에서 상당히 효과적
  - 검색 엔진 최적화
    - 특정 키워드 검색했을 때 검색 결과에서 상위권에 나타나도록 관리하는 작업에서
    - 반응형 웹은 하나의 주소아 하나의 파일(HTML)로만 이루어져 있어서 검색 결과에 좀 더 잘 노출될 수 있음
  - 미래지향적(현재) 기술
    - 환경에 따라 최적화된 구조로 바꾼 웹사이트를 보여주게되니까
    - 앞으로 어떤 화면의 기기가 나올지 모르는 상황에서 미래에 대비할 수 있는 웹 기술 발전 가능

## 반응형 웹 제작의 핵심 기술

### 가변 그리드
- 고정 크기인 픽셀(px) 표현은 한계가 있기 때문에
- 픽셀 대신 퍼센트(%)로 제작하는 기술
- width:90%;
- 그리드 기술을 사용하여 픽셀(px)을 퍼센트(%)로 바꾸어 비율로 제작하면 가변적으로 작동하기는 하지만 기기나 환경에 따라 구조를 바꾸지는 못함
- 화면을 제어할 ‘뷰포트’와 화면의 크기나 환경을 감지하여 구조를 바꿔줄 ‘미디어 쿼리’ 필요
- 적용
  - 가변 영역
    - 웹 브라우저 크기 변경해도 가로 비율을 일정하게 유지한다.
  - 가변 폰트
    - 글자를 가변적이게 만들어 주는 가변 폰트
    - viewport-relative length units(뷰포트 비례 단위)
      - vw, vh, vmin, vmax를 사용하면 브라우저 비율에 따라 글자 크기가 늘어나거나 줄어든다.
      - vw : 브라우저의 너비를 100으로 기준해서 글자 크기 결정
      - vh : 높이를 100으로 기준
      - vmin : 너비, 높으 중 작은 쪽 기준
      - vmax : 너비, 높이 중 큰 쪽 기준
  - 가변 margin / padding
    - %로 설정
    - 크기 조절 시 같은 비율로 마진과 패딩 유지
  - 멀티미디어 요소 가변적 작동
    - 브라우저의 비율에 따라 웹사이트의 구조가 늘어나거나 줄어드는 가변형 레이아웃에서 브라우저 너비에 맞게 이미지나 기타 멀티미디어 요소들을 가변적으로 작동하게 만들어줘야 한다.
    - width와 max-width 속성의 차이
      - width : 100%;는 화면의 너비에 맞춰 크기 조정
      - max-width : 100%;는 화면의 너비에 맞춰 크기 조정, 그러나 멀티미디어 요소 자신의 기본 크기 이상으로는 커지지 않게 제한한다.

## 사진

#### varArea.html(가변 영역)

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        #wrap {
            margin: auto 0;
            width: 90%;
            height: 300px;
            border: 4px solid #000;
        }
        #wrap div {
            display: inline-block;
            height: 100%;
        }
        #wrap div:nth-child(1) {
            width: 33.3%;
            background-color: green;
        }
        #wrap div:nth-child(2) {
            width: 66.7%;
            background-color: yellow;
        }
    </style>
</head>
<body>
    <div id="wrap">
        <div></div><div></div>
    </div>
</body>
</html>

<!-- 
wrap이라는 div로 모든 태그를 감싸면 편리한 이유

웹 문서 내용 전체의 크기나 배경색을 한번에 조절할 수 있다.

브라우저 화면 크기에 상관없이 웹문서의 내용을 중앙에 배치할 수 있다.

반응형 웹에서 자식 박스들이 가변 크기로 설정되었을 때 무제한으로 늘어나는 것을 방지할 수 있다. 

자식 박스들을 가변 크기로 만들 때 기준 크기로 사용할 수 있음. 
-->
~~~

## 사진

#### varFont.html(가변 폰트)

~~~html
 <style>
        .vw {font-size: 5vw;}
        .vh {font-size: 5vh;}
        .vmin {font-size: 5vmin;}
        .vmax {font-size: 5vmax;}
    </style>
</head>
<body>
    <p>기본 단위</p>
    <p class="vw">vw 단위</p>
    <p class="vh">vh 단위</p>
    <p class="vmin">vmin 단위</p>
    <p class="vmax">vmax 단위</p>
</body>
</html>
~~~

## 사진

#### varMargin.html(가변 마진)

~~~html
<style>
        *{margin:auto 0; padding: 0; font-size: 100%;} /* 문서 전체에 적용 */
        #wrap {
            margin: 0 auto;
            width: 90%;
            padding: 0.5%;
            background-color: yellow;
        }
        #wrap div {
            width: 90%;
            margin: 5%;
            background-color: green;
        }
        p {padding: 4%;}
    </style>
</head>
<body>
    <div id="wrap">
        <div>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing 
                elit, sed do eiusmod tempor incididunt ut labore et 
                dolore magna aliqua. Ut enim ad minim veniam, quis 
                nostrud exercitation ullamco laboris nisi ut aliquip
                </p> 
        </div>
        <div>
            <p>
            화면의 크기나 환경을 감지하여 웹사이트를 변경하는 기술
            컴퓨터 기기의 환경 또는 종류를 감지해야 그 기기에 맞게 
            웹사이트의 구조를 바꿀 수 있기 때문에 반응형 웹을 제작할 때 
            반드시 필요한 기술</p> 
        </div>
    </div>
</body>
</html>
~~~

#### varMedia.html(멀티미디어 요소 가변적으로 만들기)

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>가변적 멀티미디어 요소</title>
		<style type="text/css">
			video {
				/* width:100%; */ 
				max-width:100%; /* 자신의 기본 크기 이상으로 커지지 않음 */
			}
		</style>
	</head>
	<body>
		<div id="video">
			<video controls>
				<source src="media/Wildlife.mp4" type="video/mp4"></source>
				
				<track src="media/track.vtt" kind="captions" srclang="ko" label="Korean"></track>
				<track src="media/track2.vtt" kind="captions" srclang="eng" label="English"></track>
				<track src="media/track2.vtt" kind="captions" srclang="chn" label="Chinese"></track>
				<track src="media/track2.vtt" kind="captions" srclang="jp" label="Japanese"></track>
			</video>
		
		</div>
	</body>
</html>
~~~

### 미디어 쿼리
- 화면의 크기나 환경을 감지하여 웹사이트를 변경하는 기술
- 컴퓨터 기기의 환경 또는 종류를 감지해야 그 기기에 맞게 웹사이트의 구조를 바꿀 수 있기 때문에 반응형 웹을 제작할 때 반드시 필요한 기술
- query : 질의 (질문)
- 미디어에게 질문하고 감지하여 웹사이트를 변경하는 기술
  - ‘어떤 종류의 미디어 인가?’
  - ‘미디어 화면의 크기는 어느 정도 되나?’
- 기본 문법
  - @media [미디어 유형] [and] (조건문) {실행문}
  - (조건문)
    - 조건문이 사실일 경우 뒤에 오는 것을 해석하라는 의미
    - (min-width:320px)
  - {실행문}
    - 일반적으로 CSS 코드로 작성
    - @media all and (min-width:960px) { body {background : yellow;} }
    - [미디어 유형] : 생략 가능
      - all, pring, screen, ty, projection, handheld 등
      - 생략 시 all 적용
      - 스마트 기기는 screen 사용
- 주의사항
  - and 다음에 반드시 공백 있어야 함
  - min 접두사를 사용할 때는 반드시 크기가 작은 순서대로 작성
  - max 접두사를 사용할 때는 반드시 크기가 큰 순서대로 작성
  - 크기 감지 기준은 HTML 문서 크기
    - 미디어 쿼리를 사용해서 브라우저 크기를 감지할 때는 HTML 문서 크기를 기준으로 감지한다.

#### mediaQuery.html(문서 내부에 적용)

~~~html
 <style>
        @media all and (min-width:320px) {
            body {background: red;}
        }
        @media all and (min-width:768px) {
            body {background: green;}
        }
        @media all and (min-width:960px) {
            body {background: yellow;}
        }
        * {margin: 0; padding: 0;}
        div{margin: auto 0;
            width: 50%;
            max-width: 420px;
            }
        img {
            width: 100%;
            height: auto;
            border: solid 1px;
        }
    </style>
</head>
<body>
    <div>
        <img src="image/사진.jpg">
    </div>
</body>
</html>
~~~

#### mediaQuery2.html(orientation : portrait/landscape적용)

~~~html
<style>
        @media screen and (orientation:portrait) {
            body {background-color: red;}
        }
        @media screen and (orientation:landscape) {
            body {background-color: green;}
        }
        
        * {margin: 0; padding: 0;}
        div{margin: auto 0;
            width: 50%;
            max-width: 420px;
            }
        img {
            width: 100%;
            height: auto;
            border: solid 1px;
        }
    </style>
</head>
<body>
    <div>
        <img src="image/사진.jpg">
    </div>
</body>
</html>
~~~

#### mediqQuery3.html(스마트폰 크기일 경우 스타일 해제)

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>미디어 쿼리 : 스마트폰에서 스타일 해제</title>
		<style type="text/css">
			* { margin:0; padding:0;}
			
			body {
				width:960px;
				margin:0 auto;
				overflow:hidden;
			}
			
			#menu {
				width:260px;
				float:left;
			}
			
			#section {
				width:700px;
				float:right; 
			}
			
			@media screen and (max-width:767px){
				/* 스마트폰 사이즈에서는 전부 해제  */
				body { width:auto;}
				#menu { width:auto; float:none;}
				#section { width:auto; float:none;}  
			}
		</style>
	</head>
	<body>
		<div id="menu">
			<ul>
				<li>메뉴1</li>
				<li>메뉴2</li>
				<li>메뉴3</li>
			</ul>
		</div>
		<div id="section">
			<h1>반응형 웹</h1>
			<p>크기 감지 기준은 HTML 문서 크기라는 것
					미디어 쿼리를 사용해서 브라우저 크기를 감지할 때, 어떤 대상을 기준으로 크기를 감지하는지 모르고 있는 경우가 대부분임
					이처럼 어떤 기준으로 크기를 감지해야 하는지 몰라 웹사이트 제작 시 혼란을 겪는 경우가 많음
					미디어쿼리를 사용해서 브라우저의 크기를 감지할 때는 HTML 문서 크기를 기준으로 감지한다는 것</p>
			<p>브라우저의 비율에 따라 웹사이트의 구조가 늘어나거나 줄어드는 가변형 레이아웃에서
					브라우저 너비에 맞게 이미지나 기타 멀티미디어 요소들을 가변적으로 작동하게 만들어줘야 함
					width와 max-width 속성의 차이
					width : 100%; 화면의 너비에 맞춰 크기 조정
					max-width:100%;
					화면의 너비에 맞춰 크기 조정
					그러나 멀티미디어 요소 자신의 기본 크기 이상으로는 커지지 </p>
		</div>
	</body>
</html>
~~~

#### mediaQuery4.html(모바일과 PC에서 각각 다르게 적용, 외부 CSS 사용)

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<meta name=”viewport” content=”width=divice-width, initial-scale=1”>
		
		<title>미디어 쿼리 : 외부 CSS 사용</title>
		<style type="text/css">
			div {
					margin:0 auto;
					width:50%;
				}
				
			img{
				width:100%;
				border:solid 1px; 
			}		
		</style>
		<!-- 모바일용 -->
		<link rel="stylesheet" href="mobile.css" media="(max-width:800px)">
		<!-- PC용 -->
		<link rel="stylesheet" href="pc.css" media="(min-width:800px)">
	</head>
	<body>
		<div><img src="image/사진.jpg"></div>	
	</body>
</html>
~~~

~~~css
/* pc */
@charset "UTF-8";
body {background:red;}
~~~

~~~css
/* 모바일 */
@charset "UTF-8";
body {background:yellow;}
~~~

### 뷰포트
- 화면에 보이는 영역을 제어하는 기술
- 데스크탑 컴퓨터 : 해상도를 화면 크기로 감지
- 스마트 기기 : 기본 설정값을 보이는 영역(viewport)으로 감지
- 뷰포트 기술로 스마트 기기의 보이는 영역을 실제 화면 크기로 변경
- 미디어 쿼리가 기기의 화면 크기를 정확하게 감지할 수 있도록 하기 위해 뷰포트 기술 이용
- \<mete> 태그의 name 속성을 "viewport"로 지정

~~~html
<meta name="viewport" content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1, user-scalable=no">
~~~

- width : 뷰포트의 넓이
- initial-scale : 뷰포트의 초기 배율
  - 1 보다 작으면 축소
  - 1 보다 크면 확대
- minimum-scale
  - 뷰포트의 최소 축소 비율
  - 기본값 : 0.25
- maximum-scale
  - 뷰포트의 최대 확대 비율
  - 기본값 : 0.25
- user-scalable
  - 뷰포트의 확대 / 축소 여부
  - 기본값 : yes
  - no로 설정하면 사용자가 페이지 확대, 축소 불가능.
- 크롬 브라우저의 __검사__ 도구를 활용하면 뷰포트 영역 확인 가능 (F12)

### 플렉서블 박스
- 가변적인 박슬 만드는 기술인 동시에 웹사이트의 구조 설계를 위한 기술
- 가변적인 박스를 간단하게 만들어줄 뿐 아니라 박스를 쉽게 배치할 수 있다는 장법
- 플렉서블 박스의 특정 속성값을 설정하여, 여러 박스의 높이/길이/위치 등이 유연하게 작동하는 박스를 간단히 만들 수 있음
- __플렉서블 박스__ 와 __플렉서블 아이템__ 으로 구성

## 사진

- 플렉서블 박스
  - 부모 박스(flex container)
  - 가변적인 박스로 작동하기 위한 기본 개념
  - wrap처럼 모든 요소들을 감싸고 있는 존재
  - 특정 속성 값을 적용해서 가변적인 박스로 작동하게 함.
- 플렉서블 아이템
  - 자식 박스(flex item)
  - 플렉서블 박스 안에 들어있는 박스
  - 정렬 대상
  - 속성 값에 의해 작동
- 플렉서블 박스의 축과 방향
  - 플렉서블 박스에는 플렉스 아이템을 지탱하기 위한 개의 축이 있음
  - 주축(main axis)과 교차축(cross axis)
  - 주축(main axis)
    - 중심이 되는 되는 축
    - 주축을 따라 플렉스 아이템이 배치됨
  - 축의 방향
    - 주축이 가로일 경우 박스들이 왼쪽에서 오른쪽으로 배치 (역방향 가능)
    - 주축이 세로일 경우 박스들이 위에서 아래로 배치 (역방향 가능)
  - 교차축(cross axis)은 주축에 교차하는 축

## 사진

- flexbox 적용 (플렉서블 박스 (부모 박스)에 설정하는 속성)
- display : 부모 박스 배치 형태
  - flex : 수직 정렬 (block 형태)
  - inline-flex : 수평 정렬 (inline-block)
- flex-direction : item 배치 형태
  - row : 왼쪽 -> 오른쪽
  - row-reverse : 오른쪽 -> 왼쪽
  - column : 위 -> 아래
  - column-reverse : 아래 -> 위
- flex-wrap
  - wrap : 여러 줄
  - nowrap : 1줄
  - wrap-reverse. 여러 줄. 아래 -> 위
- justify-content (주축에서의 정렬 방식. 수평 방향)
  - flex-star: 시작점으로 배치
  - flex-end: 끝점으로 배치
  - space-between : item 사이에 간격 배치. 빈 공간이 있을 때 간격 동일
  - space-around: item 사이에 간격 배치. 빈 공간이 있을 때 양 옆에도 공간.
  - space-evenly : 동일한 공간으로 배치

#### flexBox.html

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>플렉서블 박스</title>
		<style type="text/css">
			* {margin:0; padding:0;}
			.wrap {
			    display:flex;			/* 부모 박스 배치 형태 : flex(위아래 block) */
			    /* display:inline-flex; */   /* 부모 박스 배치 형태 : inline-flex(좌우 나란히 inline-block) */ 
			    /* justify-content:space-between; */
			    /* justify-content:space-around; */
			    justify-content:space-evenly; 
			    flex-direction:row; 
				width:45%;
				height:300px;
				margin:0 auto;
				border:4px solid #000;
				margin-bottom:10px; 
			}
			
			.wrap div {
				width:20%;
			}
			
			.wrap div:first-child {
				background-color:red;		
			}
			
			.wrap div:nth-child(2) {
				background-color:blue;		
			}
			
			.wrap div:nth-child(3) {
				background-color:yellow;		
			}
		
		</style>
	</head>
	<body>
		<div class='wrap'>
			<div></div><div></div><div></div>
		</div>
		
		<div class='wrap'>
			<div></div><div></div><div></div>
		</div>
	</body>
</html>
~~~

# FrontEnd_day3 정리 (2021.12.06 월요일)

## Bootstrap
- HTML, CSS, JS 라이브러리
- jQuery 기반의 HTM5 Web Framework
- 프론트엔드에서 작동되는 프레임워크
- 트위터에서 사용하던 각종 레이아웃, 버튼, 입력 요소 등 UI 요소들을 누구나 사용할 수 있도록 만들어진 오픈 소스 프레임 워크 (라이브러리)
- HTML/CSS 기반의 템플릿 양식, 버튼, 내비게이션 등 다양한 UI 요소 포함
- 자바스크립트를 선택적으로 확장 가능

### Bootstrap 특징
- 쉽고 편리하게 사용할 수 있음
- HTML/CSS 기본 지식만 있으면 누구나 사용 가능
- 반응형 웹 디자인
- PC 또는 스마트폰이나 태블릿 등의 모바일용 디자인 지원
- 모든 최신 브라우저와 호환

### Bootstrap 기능
- CSS 기능 : 디자인이나 스타일 적용
- 컴포넌트 기능 : 내비게이션 바, 탭, 버튼 등의 기능을 간단하게 수정해서 사용 가능
- 자바스크립트 기능 : 사용자의 액션과 상호작용하는 기능 제공

### Bootstrap 장점
- 쉽고 빠르게 다양한 기능 개발 가능
- 모바일 환경과 반응형 웹 제작 가능
- 수준 높은 퀄리티 제공
- 개발 시간 단축으로 개발 비용 절감
- 오픈 소스이며 상업적 이용 가능

### Bootstrap 단점
- jQuery 의존성 높음
- 정형화된 디자인

### 사용 방법
- 파일을 다운 받아서 사용
  - Bootstrap 구성
    - css 폴더
    - js 폴더
    - Bootstrap을 다운로드 받아 프로젝트 폴더에 css, js 폴더를 넣는다.
  - jQuery파일 필요
    - jQuery 파일을 다운로드 받아서 프로젝트 폴더에 넣는다.
- CDN 이용
  - 링크를 통해서 네트워크로 import

### Bootstrap 사용
- 부트스트랩에 정의된 다양한 클래스들을 HTML 태그에 적용하고 (class 속성에 지정)
- 부가적인 속성들을 정의한 클래스들을 조합해서 사용

~~~html
<태그 class=”bs클래스이름1  bs클래스이름2, …..” >
<button type=”button” class=”btn btn-primary”>
<div class=”container bg-primary text-white”>
~~~

### Bootstrap 색상
- 사진사진사진사진

### 주요 기능
- Containers
- Jumbotron
- Grid
- button
- Table
- Image

#### Containers
- 레이아웃 최상위 요소로 다른 요소 포함
- \<div clas=”container”>
- .container : 반응형 고정 폭 컨테이너
- .container-fluid : 뷰포트 전체 폭까지 늘어나는 최대폭 컨테이너
- 컨테이너 예제 (container.html)
- viewport 포함
- \<link> : css/bootstrap.min.css
- \<script> : jquery 파일 소스 지정
- \<script> : js/bootstrap.min.js 소스 지정
- 순서 주의!!! 
  - jquery 파일 소스 지정이 먼저 와야 함

##### container.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!-- link -->
    <link rel="stylesheet" href="css/bootstrap.min.css">
    <!-- jQuery가 먼저 와야 한다!!! -->
    <script src="js/jquery-3.6.0.min.js"></script>
    <script src="js/bootstrap.min.js"></script>
</head>
<body>
    <div class="container bg-primary text-white">
        <h1>bootstrap</h1>
        <p>container</p>
    </div>
    <div class="container-fluid bg-danger text-white">
        <h1>bootstrap</h1>
        <p>container</p>
    </div>
</body>
</html>
~~~

## 사진