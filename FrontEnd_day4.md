# FrontEnd_day3 정리 (2021.12.06 월요일)

## Bootstrap 주요 기능
- Containers (Bootstrap - 적용방법, Container에 올림)
- Jumbotron
- Grid
- button
- Table
- Image

## Jumbotron
- 일종의 대형 전광판
- 특정 컨텐츠나 관심있는 정보를 눈에 띄게 보여주기 위한 큰 박스

## 사진

#### 점보트론 예제 : jumbotron.html

~~~html
<body>
    <div class="container bg-primary">
        <div class="jumbotron alert-success">
            <h1>Jumbotron</h1>
            <p>둥근 모서리 사각형 영역</p>
        </div>
    </div>
    <div class="jumbotron alert-success">
        <div class="container bg-primary">
            <h1>Jumbotron</h1>
            <p>container 밖에 있는 jumbotron</p>
        </div>
    </div>
    <div class="jumbotron jumbotron-fluid alert-success">
        <div class="container bg-primary">
            <h1>Jumbotron</h1>
            <p>container 밖에 있는 jumbotron</p>
            <p>jumbotron-fluid : 각진 모서리</p>
        </div>
    </div>
</body>
</html>
~~~

## 사진

#### 점보트론 예제 : jumbotron2.html

~~~html
<div class="container">
       <div class="jumbotron alert-primary">
           <h1 class="text-center">안녕하세요</h1>
           <p class="text-center text-danger">처음 뵙겠습니다. <br>
               저는 개발자가 되고 싶은 고병채라고 합니다<br>
            잘 부탁드리겠습니다.</p>
            <a href="#" class="btn btn-primary btn-lg">CV보기</a>
       </div>
   </div>
~~~

## 그리드(Grid)
- 격자 모양으로 영역 분할 가능
- 1행을 12 등분해서 비율로 배치
- 행 : class="row"
- 열 : class="col-숫자"
  - 숫자 = 12칸 중 차지하는 칸 수
- 필요에 따라 열을 묶어 더 큰 크기의 열로 사용 가능
- col-scale-숫자
  - col-scale-숫자 : 12칸 중 차지하는 칸 수
  - col-sm-숫자 : 576px 이하이면 세로로 배치
  - col-md-숫자 : 768px 이하이면 세로로 배치
  - col-lg-숫자 : 992px 이하이면 세로로 배치
  - col-sxl-숫자 : 1200px 이하이면 세로로 배치

#### 그리드 예제 : grid.html

## 사진

~~~html
<body>
    <div class="row">
        <div class="col bg-success">a</div>
        <div class="col bg-danger">b</div>
        <div class="col bg-warning">c</div>
    </div>
    <br>
    <div class="row">
        <div class="col bg-success">a</div>
        <div class="col bg-danger">b</div>
        <div class="col bg-warning">c</div>
        <div class="col bg-info">d</div>
    </div>
    <br>
    <div class="row">
        <div class="col bg-success">a</div>
        <div class="col bg-danger">b</div>
        <div class="w-100"></div>
        <div class="col bg-warning">c</div>
        <div class="col bg-info">d</div>
    </div>
</body>
~~~

## 사진

### 브라우저 크기에 따라 변경

## 사진

#### 그리드 예제 : grid2.html

~~~html
<body>
    <div class="container">
        <div class="row">
            <div class="col-6 bg-success">a</div>
            <div class="col-6 bg-warning">b</div>
        </div>
        <br>
        <div class="row">
            <div class="col-2 bg-success">a</div>
            <div class="col-10 bg-warning">b</div>
        </div>
        <br>
        <div class="row">
            <div class="col-4 bg-success">a</div>
            <div class="col-8 bg-warning">b</div>
        </div>

        <hr>

        <div class="row">
            <div class="col-sm-6 bg-success">a</div>
            <div class="col-sm-6 bg-warning">b</div>
        </div>
    </div>
    <br>
    <div class="row">
        <div class="col-md-6 bg-success">a</div>
        <div class="col-md-6 bg-warning">b</div>
    </div>
    <br>
    <div class="row">
        <div class="col-lg-6 bg-success">a</div>
        <div class="col-lg-6 bg-warning">b</div>
    </div>
    <br>
    <div class="row">
        <div class="col-xl-6 bg-success">a</div>
        <div class="col-xl-6 bg-warning">b</div>
    </div>
    <hr>
    <div class="container-fluid">
        <div class="row">
            <div class="col-md-1 bg-primary">1</div>
            <div class="col-md-1 bg-primary">1</div>
            <div class="col-md-1 bg-primary">1</div>
            <div class="col-md-1 bg-primary">1</div>
            <div class="col-md-1 bg-primary">1</div>
            <div class="col-md-1 bg-primary">1</div>
            <div class="col-md-1 bg-primary">1</div>
            <div class="col-md-1 bg-primary">1</div>
            <div class="col-md-1 bg-primary">1</div>
            <div class="col-md-1 bg-primary">1</div>
            <div class="col-md-1 bg-primary">1</div>
            <div class="col-md-1 bg-primary">1</div>
        </div>
    </div>
</body>
~~~

## 버튼(Button)
- 버튼으로 사용할 수 있는 요소들에 class="btn" 적용
- \<a>
- \<button>
- \<input type=”button”>
- \<input type=”submit”>
- \<input type=”reset”>
- 기본 : class="btn"
- 색상 설정 : class="btn btn-primary"
- 크기 설정 : btn-lg, btn-md, btn-sm
- 테두리 표시 : btn-outline-dark, btn-outline-primary

## 사진

#### 버튼 예제 : button.html

~~~html
<style>
            .block {width: 50%;}
        </style>
</head>
<button>
    <!-- btn만 설정하면 클릭했을 때 테두리 표시(평소에는 티 안남) -->
    <a href="#" class="btn">Link</a>
    <button class="btn">Button</button>
    <input type="button" class="btn" value="Input-Button">
    <input type="submit" class="btn" value="Input-submit">
    <input type="reset" class="btn" value="Input-reset">
    <hr>
    <!-- 색상 설정 -->
    <a href="#" class="btn btn-success">Link</a>
    <button class="btn btn-primary">Button</button>
    <input type="button" class="btn btn-warning" value="Input-Button">
    <input type="submit" class="btn btn-danger" value="Input-submit">
    <input type="reset" class="btn-info" value="Input-reset">
    <hr>
    <!-- 크기 설정 (md(medium)가 디폴트임)-->
    <a href="#" class="btn btn-success btn-lg">Link</a>
    <button class="btn btn-primary btn-md">Button</button>
    <button class="btn btn-primary btn-mini">mini</button>
    <input type="button" class="btn btn-warning" value="Input-Button"> 
    <input type="submit" class="btn btn-danger btn-sm" value="Input-submit">
    <input type="reset" class="btn-info btn-sm" value="Input-reset">
    <hr>
    <!-- 테두리 설정 -->
    <a href="#" class="btn btn-outline-dark">Link</a>
    <button class="btn btn-outline-primary">Button</button>
    <input type="button" class="btn btn-outline-light text-dark" value="Input-Button">
    <input type="submit" class="btn btn-outline-danger" value="Input-submit">
    <input type="reset" class="btn-outline-info" value="Input-reset">
    <hr>
    <!--  링크만 사용-->
    <a href="#" class="btn-link">Link</a>
    <hr>
    <!-- 버튼 블록 -->
    <button class="block btn-large btn-primary btn-block">Button block</button>
    <button class="block btn-sm btn-info btn-block">Button block</button>
</body>
</html>
~~~

## 이미지(image)
- rounded : 둥근 모서리
- rounded-circle : 둥근 이미지
- img-thumbnail : 썸네일 이미지
- float-left / float-right : 좌 / 우 정렬
- mx-auto + d-block : 가운데 정렬
- img-fluid : 브라우저 크기에 따라 변경

#### 이미지 예제 : image.html

## 사진

~~~html
   <style>
            .container{border: 1px solid black;
            margin: 50px;}
        </style>
</head>
<body>
    <div class="container">
        <img src="image/pic1.jpg" class="rounded float-left">
			<img src="image/pic1.jpg" class="rounded-circle float-right">
			<img src="image/pic1.jpg" class="img-thumbnail mx-auto d-block">
    </div>
</body>
</html>
~~~

## 테이블(Table)
- class="table"
- table-bordered : 테두리 있음
- table-borderless : 테두리 없음
- table-striped : td 태그 흰색행 / 회색행 순차
- table-hover : 행에 마우스 올리면 색상 변경
- table-dark :  배경색을 검점색으로 변경

## 사진

#### 테이블 예제 : table.html

~~~html
<body>
    <div class="container">
        <!-- 기본값은 table-md -->
        <table class="table table-sm table-hover table-info table-striped">
            <thead class="thead-dark">
                <tr>
                    <th>번호</th>
                    <th>제목</th>
                    <th>작성자</th>
                    <th>작성일</th>
                    <th>조회수</th>
            </tr>
            </thead>
            <tr class="table-danger">
                    <td>4</td>
                    <td>HTML /CSS</td>
                    <td>flower</td>
                    <td>2019-11-17</td>
                    <td>2</td>
             </tr>
            <tr>
                    <td>3</td>
                    <td>일본어 스터디</td>
                    <td>성춘향</td>
                    <td>2019-11-15</td>
                    <td>3</td>
             </tr>
            <tr>
                    <td>2</td>
                    <td>Bootstrap</td>
                    <td>이몽룡</td>
                    <td>2019-11-12</td>
                    <td>0</td>
             </tr>
            <tr>
                    <td>1</td>
                    <td>JSP 프로그래밍</td>
                    <td>홍길동</td>
                    <td>2019-11-07</td>
                    <td>1</td>
             </tr>				
        </table>
        <hr>
        <table class="table table-sm table-hover table-striped">
            <thead class="thead-dark">
                <tr>
                    <th>번호</th>
                    <th>제목</th>
                    <th>작성자</th>
                    <th>작성일</th>
                    <th>조회수</th>
            </tr>
            </thead>
            <tr class="table-danger">
                    <td>4</td>
                    <td>HTML /CSS</td>
                    <td>flower</td>
                    <td>2019-11-17</td>
                    <td>2</td>
             </tr>
            <tr>
                    <td>3</td>
                    <td>일본어 스터디</td>
                    <td>성춘향</td>
                    <td>2019-11-15</td>
                    <td>3</td>
             </tr>
            <tr>
                    <td>2</td>
                    <td>Bootstrap</td>
                    <td>이몽룡</td>
                    <td>2019-11-12</td>
                    <td>0</td>
             </tr>
            <tr>
                    <td>1</td>
                    <td>JSP 프로그래밍</td>
                    <td>홍길동</td>
                    <td>2019-11-07</td>
                    <td>1</td>
             </tr>				
        </table>
    </div>
</body>
</html>
~~~

## 내비게이션 바 (Navbar)
- class="navbar"
- navbar-nav / nav-item
- dropdown / dropdown-menu / dropdown-item

### 큰 해상도
## 사진

### 작은 해상도
## 사진

#### 내비게이션 바 예제 : navBar.html

~~~html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Bootstrap navBar</title>
    <link rel="stylesheet" href="css/bootstrap.min.css">
    <script src="js/jquery-3.6.0.min.js"></script>  <!-- jquery가 먼저 와야 함 -->
    <script src="js/bootstrap.min.js"></script>
</head>
<body>
    <div class="container">
        <!-- navBar -->
        <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
            <ul class="navbar-nav mr-auto">
                <li class="nav-item active"><a class="nav-link" href="#">HOME</a> </li>
                <li class="nav-item"><a class="nav-link" href="#">LINK1</a> </li>
                <li class="nav-item"><a class="nav-link" href="#">LINK2</a> </li>
                <li class="nav-item"><a class="nav-link" href="#">LINK3</a> </li>
                <li class="nav-item"><a class="nav-link" href="#">LINK4</a> </li>
                <li class="nav-item"><a class="nav-link" href="#">LINK5</a> </li>
                <!-- 드롭다운 메뉴 -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button"
                       data-toggle="dropdown">DropDown</a>
                    <div class="dropdown-menu">
                        <a class="dropdown-item">Dropdown Item1</a>
                        <a class="dropdown-item">Dropdown Item2</a>
                        <div class="dropdown-divider"></div>
                        <a class="dropdown-item">Dropdown Item3</a>
                        <hr>
                        <a class="dropdown-item">Dropdown Item4</a>
                    </div>
                </li>
            </ul>
            <!-- 검색 form 추가 -->
            <form class="form-inline">
                <input class="form-control mr-lg-2" type="search" placeholder="Search" aria-label="Search">
                <button class="btn btn-success" type="submit">Search</button>
            </form>
        </nav>
    </div>
</body>
</html>
~~~

# FrontEnd_day4 정리 (2021.12.07 화요일)

## JavaScript
- 정식명칭 : ECMA스크립트(ECMAScript)
- ECMA International ECMA-262 기술 구격에 따라 정의하고 있는 표준화된 스크립트 프로그래밍 언어
- ES6(자바스크립트 버전)
  - default parameter
  - class
  - arrow function
  - const
  - let
  - 등...
- 동적인 웹 페이지를 작성하기 위해 사용되는 언어
- 웹 표준 프로그래밍 언어
- 모든 웹 브라우저에서 자바스크립트 지원
- 웹 브라우저 뿐 아니라 스마트폰 app 개발 등 각종 분야에서 사용
- 과거에는 브라우저에 내장되어 제한된 기능만 지원하였는데 현재는 Ajax(Asynchronous JavaScript and XML) 기술과 함께 영향력이 증가
- 전 세계에서 가장 많이 사용되는 언어

### JavaScript 기능
- HTML이 지원하지 못하는 다양한 기능 지원
  - 동적인 움직임 / 이벤트 발생 처리 / 경고 메시지 출력 / 데이터 유효성 확인 / 멀티미디어 기능
- Ajax를 이용하여 새로운 내용을 동적으로 로딩하거나 서버에 전송하여 동적인 페이지 생성
- 애니메이션 기능 지원
- 브라우저 사용자의 특성(웹 페이지 탐색 움직임, 게시물 읽을 때 습관 등)에 대한 정보를 서버로 전송하여 웹 분석, 사용자 동작 추적, 웹 서비스 개인화 등에 사용

### JavaScript 실행
- 스크립트 언어이기 때문에 컴파일 되지 않고 인터프리터를 통해 웹 브라우저에서 한 줄씩 바로 실행

### JavaScript 용도
- 이벤트에 반응하는 동작 구현
- HTML 요소를 동적으로 변경
- 사용자가 입력한 값들 검증
- 게임이나 애니메이션 / 멀티미디어 기능 구현
- Ajax 기술을 사용하여 서버와 데이터를 비동기적으로 교환
  - 비동기식 처리
    - 서버 측에 데이터를 요청한 후 데이터 수신이 완료될 때 까지 기다리지 않고 다른 작업 진행이 가능한 기술

### JavaScript 기본 구조
- HTML 문서에 \<script> 자바스크립트 코드 \</script> 태그 삽입
- 사용법
  - Internal
  - External
  - Inline

##### Internal
- HTML 문서에 삽입
- 일반적으로 \<head> 부분에 삽입하지만, \<body> 안에 삽입하기도 함.
- \<script type="text/javascript"> alert("알림창"); \</script>
- internal.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript">
        alert("head 부분에 삽입된 알림창");
    </script>
</head>
<body>
    <script type="text/javascript">
        alert("body 부분에 삽입된 알림창");
    </script>
</body>
</html>
~~~

##### External
- 별도의 자바스크립트 파일(확장자가 .js)로 작성하여 HTML 문서에서 소스 지정
- \<script src="@@@.js> \</script>
- external.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="a.js"></script>
</head>
<body>
    
</body>
</html>
~~~

- a.js

~~~js
alert("a.js에 삽입된 알림창");
~~~

##### Inline
- 자바스크립트 코드가 짧을 때 HTML 태그의 이벤트 핸들러 속성을 사용하여 함수 호출
- \<body onLoad="start()">
- \<button onClick="show()">
- inline.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script type="text/javascript">
        function start() {
            alert("inline 방식으로 start() 함수 실행\n출력된 알림창.");
        }
    </script>
</head>
<body onload="start()">
    
</body>
</html>
~~~

### 데이터를 출력하는 방법
- window.alert() : 내용을 알림창(경고창)으로 출력
- consol.log() : 내용을 콘솔에 출력
- document.write() : 화면(문서)에 출력
- DOM : Document Object Model 사용

~~~html
  <script type="text/javascript">
            console.log("Hello world!");
            console.log("<h2>Tag</h2>");
            document.write("<h2>Tag</h2>");
            alert("head 부분에 삽입된 알림창");
            document.body.innerHTML += "DOM 객체 innerHTML 속성 사용해서 출력"
            //  document.write("<h2>Tag</h2>");에서 출력된 데이터에 document.body.innerHTML을 사용해서 body에 해당 문자열 값을 더해준다.
            // document.body.innerHTML = "DOM 객체 innerHTML 속성 사용해서 출력" 만 작성했다면 'DOM 객체 innerHTML 속성 사용해서 출력'만 출력된 다.
        </script>
~~~

#### JavaScript 코드 입력 시 주의 점
- 대/소문자 구분
- 문장 끝에 세미콜론 사용
- 문자열에 따옴표 겹침 오류 주의
  - 문자열에 큰 따옴표, 작은 따옴표 모두 사용 가능하지만
  - 큰 따옴표 안에 큰 따옴표 불가능, 작은 따옴표 사용해야 한다.
  - 반대의 경우도 똑같음.
    - document.write(__"__ 이름은 고병채 __"__);
    - document.write(__'__ 이름은 고병채 __'__);
    - document.write(__"__ 이름은 __'__ 고병채 __'__ __"__);
    - document.write(__'__ 이름은 __"__ 고병채 __"__ __'__);

### JavaScript 데이터 입력 방법
- confirm() 함수로 입력 받기
- prompt() 함수로 입력 받기
- getElementsByTagName() : 태그 이름 사용
- \<input> 태그의 value 속성 사용
- DOM 사용

#### confirm() 함수
- 자바스크립트 내장 함수
- [확인] / [취소] 버튼이 있는 대화상자 출력
- 확인 누르면 true 값 반환
- 취소 누르면 false 값 반환

##### confirminput.html

~~~html
 <script type="text/javascript">
            var isStudent = confirm("당신은 학생입니까?");

            document.write("isStudent 값 : " + isStudent);
        </script>
~~~

##### confirminputEx.html

~~~html
  <script type="text/javascript">
            var isStudent = confirm("당신은 학생입니까?");
            if(isStudent) {
                document.write("결과 : 학생입니다.<br>할인율 : 50%");
            }
            else{
                document.write("결과 : 학생이 아닙니다.<br>할인율 : 없음");
            }

        </script>
~~~

#### prompt() 함수
- 자바스크립트 내장 함수
- 사용자로부터 입력 받은 값을 반환  
- prompt("출력 메시지")
- prompt("출력 메시지", "기본값")

##### promptinput.html
~~~html
 <script type="text/javascript">
            var answer = prompt("가장 좋아하는 과일은?",   "딸기" );
            alert("가장 좋아하는 과일 : " + answer + " 입니다.");
            document.write("가장 좋아하는 과일 : " + answer + " 입니다.");
        </script>
~~~

##### promptinputEx.html
~~~html
<script type="text/javascript">
            var useCard = confirm("카드로 결제합니까?");
            if(useCard) {
                var cardNum = prompt("카드로 결제합니까?",   "xxxx-xxxx-xxxx-xxxx");
                document.write("카드번호 : " + cardNum);
            }
            else {
                document.write("카드로 결제하지 않습니다.");
            }
        </script>
~~~

# FrontEnd_day3 정리 (2021.12.06 월요일)

## JavaScript 변수
- 프로그램 실행 중 값을 저장하기 위한 메모리 내의 임시 기억장소
- 자바스크립트에서 식별자(변수명, 함수명 등) 명명 규칙
  - 시작은 반드시 '영문자'나 '_' 사용한다. 숫자로 시작하지 않는다.
  - 대소문자 구별
  - 키워드 사용 불가
  - 특수문자, 공백 사용할 수 없음
  - 한글 사용 가능(영문 사용 권장)
  - 의미 있는 단어 사용(어떻게 사용하는 변수(혹은 함수)인지 알 수 있도록)
- 변수 선언
  - var
  - let
  - const
  - EC6 이후 보완하기위해 추가된 변수 선언 방식 : let, const
  - 변수를 필요한 곳에 사용하면 자동으로 생성되기 때문에 반드시 선언하지 않아도 된다.
  - 변수의 데이터 타입은 실행 시 결정(동적 타이핑)
  - 명시적으로 선언하는 경우 예약어  var사용 (명시적 선언 권장)
    - var @@@; // 명시적 선언
    - var @@@, ###, $$$; // 여러개 동시 선언 가능
    - var price = 10000; // 변수 초기화
    - var name = "홍길동"; // 변수 초기화
    - tel = "010-1111-1111"; // 명시적 선언하지 않고 변수 선언
- 정적 타이핑 언어
  - 변수의 자료형을 컴파일 시에 결정
    - c, c++, java 등
    - 선언한 변수의 자료형에 따라 값 저장
    - 선언의 의미는 실행 시 컴파일러가 운영체제에게 메모리를 얼만큼 할당 받아야 하는지 확보하도록 알리는 것
- 동적 타이핑 언어
  - 변수의 자료형을 실행 시 결정
  - 자료형 없이 변수에 값 저장
  - var name = “홍길동”;
  - num = 100;
  - JavaScript, Python 등

##### 변수 선언 예제 : variable.html

~~~html
<script type="text/javascript">
            // 명시적 선언
            var num = 10, pi = 3.14;
            var ch = 'a';
            var name = "홍길동";
            // 명시적 선언하지 않고 값 저장.
            address = "서울시 강남구";
            nation = "대한민국";
            // 변수 값만 출력
            document.write(num);
            // 문자열과 변수, 태그 연결해서 출력
            document.write("<br>");
            document.write("num : " + num + "<br>");
            document.write("pi : " + pi + "<br>");
            document.write("name : " + name + "<br>");
            document.write("address : " + address + "<br>");
            document.write("nation : " + nation + "<br>");
        </script>
~~~

### 변수의 유형
- 멤버변수(전역변수)
  - 전역 범위
  - \<script> 바로 하위에 명시적(var 사용 o)으로 선언되거나, 명시적(var 사용 x)으로 선언하지 않고 사용하는 변수
  - 자바스크립트 코드 내 모든 곳에서 사용 가능
- 지역변수
  - 함수 내에서 var를 붙여서 선언된 변수
  - 함수 내에서만 사용 가능
  - 함수 내에서 var를 붙이지 않고 사용하는 변수는 전역변수가 된다.
    - function @@@() { var name = "홍길동";} // 지역변수
    - function @@@() { name = "홍길동";} // 전역변수

##### 전역변수/지역변수 사용 예제 : variableLocalGlobal.html

~~~html
<script type="text/javascript">
            // 여기에 선언된 변수는 var 존재 여부와 상관 없이 전역 변수
            var x = 5, y = 10; // 명시적 선언 전역변수
            total = 0; // 비명시적 선언 전역변수

            function f1() { // 모든 전역 변수 사용 가능
                x = x + y;
                document.write(x + "<br>");
            }
            function f2() { // 모든 전역 변수 사용 가능
                total = x + y;
                document.write(total + "<br>");
            }

            f1();
            f2();
            document.write(x + "<br>");
            document.write(total + "<br>");

            function localf1() {
                // 지역변수 : 함수 내에서 var 붙인 변수
                // 함수 내에서만 사용 가능
                var localVar1 = 100;
            }
            localf1(); // 값이 사용 되는지 확인 위해 함수 호출
            //document.write(localVar1 + "<br>");
            // 함수에서 선언된 지역변수 사용 불가 : Uncaught ReferenceError: localVar1 is not defined
            function localf2() {
                // 전역변수 : 함수 내에서 var 붙이지 않고 저장한 변수
                // 함수 밖에서도 사용 가능
                localVar2 = 200;
            }
            localf2(); // 값이 사용 되는지 확인 위해 함수 호출
            document.write(localVar2 + "<br>"); // 제대로 출력 된다.
        </script>
~~~

### var와 let, const의 차이
- 차이점 1 : scope
  - var : function 단위의 scope
  - let : { }(block) 단위의 scope
- 차이점 2 : 
  - var는 동일 변수명 여러 개 사용해도 오류 없음
  - let은 이미 선언된 변수명으로 선언 불가
- const : 상수의 개념(값 변경 불가)

##### var와 let, const의 차이 예제 : var_let.html

~~~html
        <script type="text/javascript">
            var name = "홍길동";
            document.write(name + "<br>");
            var name = "이몽룡";
            document.write(name + "<br>");
            // 홍길동
            // 이몽룡 출력됨
            // 동일 변수명으로 중복 선언해도 오류 없고 다른 값으로 출력 됐다.

            // let name = "성춘향";
            // document.write(name + "<br>");
            // Uncaught SyntaxError: Identifier 'name' has already been declared
            // 이미 사용됐기 때문에 사용 불가능
            let name2 = "성춘향";
            document.write(name2 + "<br>");
            // 사용 가능

            sumi = 0;
            for(var i = 0; i < 10; i++) {
                sumi += i;
            }
            document.write(i + "<br>"); // 10 출력 => i는 for문 밖에서도 사용 가능하다. 

            // sumj = 0;
            // for(let j = 0; j < 10; j++) {
            //     sumj += j;
            // }
            // document.write(j); //  j is not defined 출력 안됨. => let은 해당 블록 안에서만 유효한 값.

            // const : 상수 개념. 값을 변경할 수 없다.
            let name3 = "홍길동";
            document.write(name3 + "<br>");
            name3 = "이몽룡";
            document.write(name3 + "<br>")
            const address = "서울";
            document.write(address + "<br>")
            // address = "부산";
            // document.write(address + "<br>") // Assignment to constant variable. => 값 변경 불가능.
        </script>
~~~

### 호이스팅(Hoisting)
- 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것
- 즉, 선언은 뒤에 하지만 선언 전에 미리 변수 사용하는 것
- var로 선언된 변수는 가능하지만, let으로 선언된 변수는 불가능.
- document.write(name);
- var name = "홍길동"; 이 가능하다. (다른 출력 함수도 마찬가지)

##### 호이스팅 예제 : variableHoisting.html

~~~html
  <script type="text/javascript">
            document.write(name);
            var name = "홍길동";
        </script>
~~~

### 연산자
- 자바와 동일

## 사진

### 데이터 타입
- 숫자 : 정수형, 실수형
- 문자 : 'a'
- 문자열 : "큰 따옴표도 가능하고", '작은 따옴표도 가능하다'
- 논리값 : true, false
- undefined와 null
  - null : 참조 객체 없음(값이 없다)
  - undefined : 값의 유형을 알 수 없다.
- 데이터 형변환
  - parseInt() : 정수값으로 형변환
  - parseFloat() : 실수값으로 형변환
  - String() / toString() : 문자열로 형변환
  - .toLocaleString() : 천단위 구분

##### 데이터 타입, 형변환 예제 : dataType.html

~~~html
        <script type="text/javascript">
            var num1 = 15; // 정수
            var num2 = 123.45; // 실수
            var answer = 'Y'; // 문자
            var name = "홍길동"; // 큰 따옴표 문자열
            var address = '서울시 강남구'; // 작은 따옴표 문자열
            var result = true; // 참
            var nothing;
            var input = prompt("자료형 예제", "취소 버튼 누르세요") // 취소 버튼 누르면 null값 반환

            // 1. 숫자 연산
            // 1851.75 출력
            document.write("정수 * 실수 : " + (num1 * num2));
            // 2. 형변환 parseInt(num2) 실수를 정수로 변환
            // 123 출력
            document.write("<br>실수를 정수로 형변환 : " + parseInt(num2));
            // 3. 숫자를  문자열로 변환
            // 15123.45 출력
            document.write("<br>숫자를 문자열로 형변환 : " + String(num1) + num2.toString());
            // 4. 문자열 * 문자열
            // NaN (Not a Number : 숫자가 아니다) 출력됨
            document.write("<br>문자열 곱하기 : " + (name*address));
            // 5. noting 변수를 선언만 하고 값을 저장하지 않은 경우 출력
            // undefined(값의 유형을 확인할 수 없음) 출력됨
            document.write("<br>nothing :  " + nothing);
            // 6. prompt() 대화상자에 취소 버튼 누를 경우
            // null(값이 없을 때) 출력됨 : '참조 객체 없음' 
            document.write("<br>input :  " + input);
        </script>
~~~