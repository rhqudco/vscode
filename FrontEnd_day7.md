## 자바스크립트 객체
- 내장객체
- 브라우저 객체
- 문서 객체(DOM)
- 사용자 정의 객체

## 브라우저 객체 모델
- 자바스크립트에서는 웹 페이지를 구성하는 HTML 태그의 모든 요소와 웹 브라우저를 구성하는 요소들을 객체로 정의하여 제공
- 객체들을 계층 구조로 분류
- 브라우저 객체
  - 웹 브라우저를 대상으로 이루어진 객체
  - window 객체 : 창
  - document 객체 : 문서
  - history 객체 : 웹 브라우저 기록 정보
  - location 객체 : 주소 정보
  - navigator 객체 : 웹 브라우저 정보(종류 판별 등)

### 브라우저 객체 계층 구조

### window 객체
- 창에 대한 전반적인 상황을 제어하는 최상위 객체
- 자바스크립트에서 사용되는 모든 객체는 window 객체 하위에 존재
- navigator 객체만 제외하고 모든 객체는 window 객체를 통해 접근하여 사용
- window 객체는 생략 가능
  - window.document.pic.src = "image.jpg";
  - 문서 내에서 name 속성이 "pic"인 객체의 src 속성 변경
  - \<img name=”pic” src=’a.jpg’>
- window 객체의 주요 속성
  - toolbar : 속성 측정 방법 yes/no, 도구 모음 표시 여부 설정
  - location : 속성 측정 방법 yes/no, URL 주소 표시줄 표시여부 설정
  - status : 속성 측정 방법 yes/no, 상태 바 표시 여부 설정
  - menubar : 속성 측정 방법 yes/no, 메뉴 표시줄 표시 여부 설정
  - scrollbars : 속성 측정 방법 yes/no, 스크롤 바 표시 여부 설정
  - directories : 속성 측정 방법 yes/no, 디렉토리 바 표시 설정
  - resizable : 속성 측정 방법 yes/no, 창의 크기 조정 가능 여부 설정
  - height : 픽셀 수, 창의 세로 길이를 픽셀 단위로 설정
  - width : 픽셀 수, 창의 가로 길이를 픽셀 단위로 설정
- window 객체의 주요 메소드
  - open() : 새로운 창을 만들어 화면에 출력하는 기능
  - close() : 열린 창을 닫는 기능
  - setTimeout('호출할 함수', 지연시간) : 일정 시간이 지난 후에 함수 한 번 호출 기능
    - 타이머ID = setTimeout('winclose()', 1000);
  - clearTimeout(타이머ID) : setTimeout() 메소드가 반환하는 타이머ID로 설정된 내용 정지 기능
    - clearTimeout(타이머ID);
  - setInterval() : 일정 시간 간격 후 명령 수행 기능(함수 여러 번 호출 가능 - 애니메이션 효과에 사용)
  - clearInterval() : setInterval()로 설정된 내용 정지 기능
- window 객체의 open() 메소드
  - window.open(“URL”, “창이름”, “창 속성”);
  - URL : 웹페이지 주소나 HTML 파일명. 빈 값이면 새로운 창을 만들어서 오픈
  - 창 이름 : 새로 만들어지는 창 이름 (임의로 작성)
  - 창 속성 : 창의 모양이나 특징
  - window.open(“test.html”, “test”, “width=200, height=200, status=yes, scrollbars=yes, resizable=yes”); // 기존의  test.html 문서 열기
  - window.open(“”, “newWin”, “width=400, height=150”);  // 새로운 창을 만들어서 열기

##### window 객체의 open() 메소드 예제 기존 문서 열기 bigimage.html, windowOpen.html
- bigImage.html

~~~html
<body>
    <center>
        <img src="image/고흐.jpg">
        <br>
        <button onclick="window.close()">닫기</button>
    </center>
</body>
~~~

- windowOpen.html

~~~html
        <script type="text/javascript">
            function showBigImage() {
                window.open("bigImage.html", "bigWin", "width=600, height=800 top=50");
            }
        </script>
</head>
<body>
    <center>
        그림에 마우스를 올리면<br>
        그림을 크게 볼 수 있습니다<br>
        <img src="image/고흐.jpg" width="118" height="146" onmouseover="showBigImage()">
    </center>
</body>
~~~

##### window 객체의 open() 메소드 예제 새로운 문서 만들어서 열기 windowOpen2.html

~~~html
        <script type="text/javascript">
            // 새로운 창을 만들어서 열기
            // 새로운 창에 문자열과 버튼 출력 / 버튼 클릭시 창 닫음
            function openNewWindow() {
                var createWin = window.open("", "newWind", "width=400, height=150")
                createWin.document.write("새로 만든 윈도우.<br>");
                createWin.document.write("<button onclick=\"window.close()\">닫기</button>");
            }
            function openWindow() {
                window.open("windowOpen.html", "bigWin", "width=200, height=400, top=50, left=400, scrollbars=yes, status=yes, resizable=yes");
            }
        </script>
</head>
<body>
    <button onclick="openNewWindow()">새 창 열기</button>
    <button onclick="openWindow()">Big Image 열기</button>
</body>
~~~

##### window 객체의 타이머 관련 메소드(setTimeout()/clearTimeout(), setInterval()/clearInterval()) 예제
- setTimeout() 에제 - setTimeout.html

~~~html
<script type="text/javascript">
            function openInfo() {
                window.open("msgWindow.html", "setTimeout", "width=300, height=200");
            }
            function showMsg() {
                document.write("로드하자마자 열린 공지 창이<br>3초 후에 자동으로 닫혔습니다.")
            }
        </script>
</head>
<body onload="openInfo()", onfocus="showMsg()">
    <h1>Opener</h1>
</body>
~~~

- setTimeout() 에제 - msgWindow.html

~~~html
        <script type="text/javascript">
            function winClose() {
                window.close();
                opener.focus(); // 현재 창을 연 부모창에 focus
            }
        </script>
</head>
<body onload="setTimeout('winClose()', 3000)">
    <h1>공지사항</h1>
    <p>이 창은 3초 후에 자동으로 닫힙니다.</p>
</body>
~~~

- setInterval(), clearInterval() 예제 - setInterval.html

~~~html
        <script type="text/javascript">
            function showTime() {
                var today = new Date();
                var hour = today.getHours();
                var minute = today.getMinutes();
                var second = today.getSeconds();
                var ampm;

                if(hour >= 12) {
                    if(hour == 12) { 
                        ampm = "오후 ";
                    }
                    else if (hour == 24) { 
                        ampm = "오전 ";
                        hour -= 24;
                    }
                    else { 
                        ampm = "오후 ";
                        hour -= 12;
                    }
                }
                else { 
                    ampm = "오전 "
                }

                var time = ampm + hour + "시 " + minute + "분 " + second + "초";
                timeShow.innerHTML = time;
            }
        </script>
</head>
<body>
    <button onclick="timerId = setInterval('showTime()', 1000)">시간 출력</button>
    <button onclick="clearInterval(timerId)">시간 정지</button>
    <h2 id="timeShow"></h2>
</body>
~~~

- setInterval(), clearInterval() 예제 - setInterval2.html

~~~html
        <script type="text/javascript">
            var count = 0;
            function start() {
                alert("이미지 10개 출력");
                timerImg = setInterval('showImage()', 1000)
            }
            function showImage() {
                count++;
                if(count % 2 == 0) {
                    document.body.innerHTML += "<img src=\"image/bomb.png\">";
                }
                else {
                    document.body.innerHTML += "<img src=\"image/apple.png\">";
                }

                if(count == 10) {
                    clearInterval(timerImg);
                    alert("이미지 출력 완료")
                }
            }

        </script>
</head>
<body onload="start()">
    
</body>
~~~

- setInterval(), clearInterval() 예제 - setInterval3.html

~~~html
 <style>
        div {margin:0 auto; width:100%; text-align:center;}
    </style>
    <script type="text/javascript">
        var imgCount = 1;    
        var countNum = 10;
        
        function startCount() {
            timerID = setInterval('showImg()', 500);
        }
        
        function showImg() {
            countH1.innerHTML = countNum;
            bombImg.src = `image/bomb${imgCount}.jpg`;
            
            imgCount++;
            countNum--;            	

            if(imgCount == 12) {
                clearInterval(timerID);
                imgCount = 1;
                countNum = 10;
            }
        }
    </script>
</head>
<body>
<div>
    <h1 id="countH1">10</h1>
    <img id="bombImg" src="image/bomb1.jpg" ><br><br>	
    <button id="btn" onClick="startCount()">카운트다운 시작</button>
</div>

</body>
</html>
~~~

## 자바스크립트 객체
- 내장객체
- 브라우저 객체
- 문서 객체(DOM)
- 사용자 정의 객체

## 브라우저 객체 모델
- 자바스크립트에서는 웹 페이지를 구성하는 HTML 태그의 모든 요소와 웹 브라우저를 구성하는 요소들을 객체로 정의하여 제공
- 객체들을 계층 구조로 분류
- 브라우저 객체
  - 웹 브라우저를 대상으로 이루어진 객체
  - window 객체 : 창
  - document 객체 : 문서
  - history 객체 : 웹 브라우저 기록 정보
  - location 객체 : 주소 정보
  - navigator 객체 : 웹 브라우저 정보(종류 판별 등)

### Location 객체
- 현재 브라우저의 주소창에 표시된 주소 값에 관련된 내용을 다루는 객체
- Location 주요 메소드
  - href = URL : 지정된 URL로 이동
  - pathname : 도메인을 제외한 실제 파일 경로
  - assign(URL) : 지정된 URL로 페이지 이동
  - replace(URL) : 현재 페이지를 URL로 대체(이 경우에 histroy 기록이 남지 않음, back버튼이 적용 안됨)
  - reload() : 문서 내용 새로 고침

##### location 객체 예제 loaction.html

~~~html
        <script type="text/javascript">
            function hrefMove() { // 뒤로가기 가능
                location.href = "http://www.google.com"; // 크롬 사용시
                // window.location.href("http://www.google.com"); // 크롬에서는 지원 안되는 형식
            }
            function assignMove() { // 뒤로가기 가능
                location.assign("http://www.daum.net");
            }
            function replaceMove() { // 뒤로가기 불가능
                location.replace("http://www.youtube.com");
            }
        </script>
</head>
<body>
    <a href="www.naver.com">네이버</a><br><br>
    <button onclick="hrefMove()">구글</button>
    <button onclick="assignMove()">다음</button>
    <button onclick="replaceMove()">유튜브</button>
</body>
~~~

## 자바스크립트 객체
- 내장객체
- 브라우저 객체
- 문서 객체(DOM)
- 사용자 정의 객체

## 브라우저 객체 모델
- 자바스크립트에서는 웹 페이지를 구성하는 HTML 태그의 모든 요소와 웹 브라우저를 구성하는 요소들을 객체로 정의하여 제공
- 객체들을 계층 구조로 분류
- 브라우저 객체
  - 웹 브라우저를 대상으로 이루어진 객체
  - window 객체 : 창
  - document 객체 : 문서
  - history 객체 : 웹 브라우저 기록 정보
  - location 객체 : 주소 정보
  - navigator 객체 : 웹 브라우저 정보(종류 판별 등)

### navigator 객체
- 브라우저에 관한 정보 제공
- 객체 속성
  - appCodeName : 브라우저의 코드명
  - appName : 브라우저의 종류
  - appVersion : 브라우저의 버전
  - cookieEnabled : 쿠키 사용 가능
  - platform : 시스템 환경
  - userAgent : 브라우저 기본 정보(종류/버전)
  - systemLanguage : 시스템 언어

## 자바스크립트 객체
- 내장객체
- 브라우저 객체
- 문서 객체(DOM)
- 사용자 정의 객체

## 브라우저 객체 모델
- 자바스크립트에서는 웹 페이지를 구성하는 HTML 태그의 모든 요소와 웹 브라우저를 구성하는 요소들을 객체로 정의하여 제공
- 객체들을 계층 구조로 분류
- 브라우저 객체
  - 웹 브라우저를 대상으로 이루어진 객체
  - window 객체 : 창
  - document 객체 : 문서
  - history 객체 : 웹 브라우저 기록 정보
  - location 객체 : 주소 정보
  - navigator 객체 : 웹 브라우저 정보(종류 판별 등)

### 문서 객체 모델(Document Object Model)
- 객체 지향 모델로서 구조화된 문서를 표현하는 형식
- HTML 문서에 접근하기 위한 표준 모델
- 표준은 대부분의 브라우저에서 DOM을 구현하는 기준
- 문서 내의 모든 요소를 정의하고, 각 요소에 접근하는 방법을 제공
- 웹 브라우저에서 보여지는 HTML 문서 태그 요소에 대한 정보와 문서에 대한 여러 가지 속성을 제공
- document 객체의 하위 객체를 이용하여 문서 내에서 일어나는 다양한 기능 제어

#### DOM 사용 시기
- HTML 문서가 로드되고 나서 파싱 작업을 거쳐 DOM 트리 생성
- DOM 문서가 로드될 때 모든 DOM을 사용할 수 있게 되는 때임
- 문서 내의 요소(태그) 제어 메소드
  - createElement('태그명') : 요소 노드 생성
  - createTextNode(text) : 텍스트 노드 생성
  - appendChild(node) : 객체에 노드 연결
  - setAttribute(name, value) : 객체 속성 설정
  - getAttribute(name) : 객체의 속성 반환
  - getElementById(id) : 태그의 id 속성이 id와 일치하는 문서 객체 반환(동일한 요소가 여러 개인 경우 첫 번째 요소만 반환)
  - getElementByName(name) : 태그의 name 속성이 name과 일치하는 문서 객체를 배열로 반환
  - getElementsByTagName('태그명') : 태그명과 일치하는 문서 객체를 배열로 반환하여 참조할 수 있게 해줌.
  - removeChild(child) : 문서 객체의 자식 노드 제거
  - querySelector(선택자) : 1개의 동일자 선택(동일한 요소가 여러 개인 경우 첫 번째 요소만 선택됨)
  - querySelectorAll(선택자) : 동일한 요소가 여러 개인 경우 모든 요소 선택
- 문서 내의 요소(태그) 제어 메소드를 사용하여 요소를 선택할 때 자바스크립트 위치 주의
  - 문서 내에서 요소(객체)들이 생성되기 전에 자바스크립트를 선택하게 되면 요소를 선택할 수 없다.

## 사진

~~~html
   <script type="text/javascript">
            window.onload = function() {
            var box = document.getElementById('box');
            box.innerHTML = "변경"
            // 이게 제일 좋은 방법?
            }
        </script>
    <!-- <script type="text/javascript">
        var box = document.getElementById('box');
        box.innerHTML = "변경"
    </script> << 이거는 불가능 하다.-->
</head>
<body>
    <div id="box">box</div>
    <!-- <script type="text/javascript">
        var box = document.getElementById('box');
        box.innerHTML = "변경"
    </script>  << 이거는 가능하다. --> 
</body>
</html>
~~~

##### 요소 제어 메소드 예제 1 createElement.html

~~~html
        <script type="text/javascript">
            window.onload = function() {
                // 1. 요소 생성
                // <h3> 태그 생성하고 객체 참조 변수에 저장
                var h3 = document.createElement('h3');
                // 텍스트 노드 생성
                var text = document.createTextNode("출력한 텍스트 : 홍길동");

                // 2. 문서에 출력
                // 텍스트를 h3에 연결
                h3.appendChild(text);
                // h3를 body에 연결(부착)
                document.body.appendChild(h3);
            };
        </script>
~~~

##### 요소 제어 메소드 예제 2 createElement2.html

~~~html
        <script type="text/javascript">
            window.onload = function() {
                // 1. 요소 노드 생성
                // <img> 태그 생성
                var img = document.createElement('img');
                // 속성 설정
                img.src = "image/bird.jpg";
                img.width = 250;
                img.height = 180;
                img.title = "예쁜새";

                // 2. 문서에 출력
                document.body.appendChild(img);
            };
        </script>
~~~

##### getElementById() 예제 1 getElementById1.html

~~~html
        <script type="text/javascript">
            function change() { 
                // 태그의 id 속성 값이 'header'인 문서 객체 반환
                var header = document.getElementById('header');
                // 요소의 텍스트 내용 변경
                header.innerHTML = "변경된 제목 입니다."
            }
        </script>
</head>
<body>
    <h1 id="header">제목</h1>
    <button id="btn" onclick="change()">제목 변경</button>
</body>
~~~

##### getElementById() 예제 2 getElementById2.html

~~~html
<script type="text/javascript">
            function change() {
                var image = document.getElementById('imageA');
                var hint = document.getElementById('hint');
                var btn = document.getElementById('changeButton');
                image.src = "image/B.png";
                hint.innerHTML = "새로운 이미지로 변경되었습니다.";
                btn.innerHTML = "완료";
            }
        </script>
</head>
<body>
    <div>
        <img id="imageA" src="image/A.png">
        <div id="hint">[변경] 버튼을 누르면 이미지가 바뀝니다.</div><br><br>
        <button id="changeButton" onclick="change()">[변경]</button>
    </div>
</body>
~~~

##### querySelector() 예제 1 querySelector.html

~~~html
        <script type="text/javascript">
            window.onload = function() {
                var header = document.querySelector('h1');

                header.style.color = 'orange';
                header.style.background = 'skyblue';
                header.innerHTML = 'JavaScript';
            }
        </script>
</head>
<body>
    <h1>Header</h1>
    <h1>Header</h1>
    <h1>Header</h1>
</body>
~~~

##### querySelectorAll() 예제  querySelectorAll.html

~~~html
    <script type="text/javascript">
        window.onload = function() {
            var headers = document.querySelectorAll('h1');

            for(var i = 0; i < headers.length; i++) {
                // headers[i].style.color = 'orange';
                // headers[i].style.background = 'skyblue';
                // headers[i].innerHTML = 'JavaScript'; 
                //혹은
                var header = headers[i];
                header.style.color = 'orange';
                header.style.background = 'skyblue';
                header.innerHTML = 'JavaScript';
            }
        }
    </script>
</head>
<body>
<h1>Header</h1>
<h1>Header</h1>
<h1>Header</h1>
</body>
~~~

##### getElementsByTagName() 예제 getElementsByTagName.html

~~~html
    <style>
        div {margin: 0 auto; width: 600px; text-align: center;}
        table {margin: 0 auto; width: 100%;}
        td {width: 50px; height: 30px;}
    </style>
        <script type="text/javascript">
            window.onload = function() {
                // 모든 td 요소 가져오기.
                var tdArr = document.getElementsByTagName('td');

                var setNumber = document.getElementById('setNumberBtn');
                var setColor = document.getElementById('setColorBtn');
                var clearNumber = document.getElementById('clearNumberBtn');
                var clearColor = document.getElementById('clearColorBtn');
                var colorArr = ['yellow', 'green', 'blue', 'gold', 'grey', 'red', 'purple']
                setNumber.onclick = function() {
                    for(var i = 0; i < tdArr.length; i++) {
                        tdArr[i].innerHTML = i;
                    }
                }
                clearNumber.onclick = function() {
                for(var i = 0; i < tdArr.length; i++) {
                    tdArr[i].innerHTML = null;
                    }
                }
                setColor.onclick = function() {
                    for(var i = 0; i < tdArr.length; i++) {
                        tdArr[i].style.background = colorArr[i];
                    }
                }
                clearColor.onclick = function() {
                for(var i = 0; i < tdArr.length; i++) {
                    tdArr[i].style.background = 'white';
                    }
                }
            };
        </script>
</head>
<body>
    <div>
        <table border="1">
            <tr>
                <td></td><td></td><td></td><td></td><td></td><td></td><td></td>
            </tr>
        </table>
        <br><br>
        <button id="setNumberBtn">셀에 번호 채우기</button>
        <button id="setColorBtn">셀에 색상 채우기</button>
        <br><br>
        <button id="clearNumberBtn">셀에 번호 지우기</button>
        <button id="clearColorBtn">셀에 색상 지우기</button>
    </div>
</body>
~~~

## 이벤트 핸들러와 이벤트 처리
- 인라인 방식과 고전 방식의 이벤트 처리 방식의 경우 동일한 객체에 대해 동일한 이벤트를 여러 번 사용 불가(마지막 이벤트 하나만 적용)
- 자주 사용되는 이벤트 핸들러
  - onLoad: HTML 문서나 특정 요소가 로드되었을 때 발생
  - onUnload: HTML 문서나 특정 요소가 사라질 때 발생
  - onClick: 클릭했을 때 발생
  - onKeyUp: 키를 눌렀다가 떼었을 때 발생
  - onKeyPress: 키를 누를 때 발생
  - onMouseDown: 마우스 버튼 눌렀을 때 발생
  - onMouseUp: 마우스 버트느 눌렀다가 떼었을 때 발생
  - onMouseOver: 포커스로 마우스 포인터가 들어갈 때 발생
  - onMouseOut: 포커스에서 마우스 포인터가 나갈 때 발생
  - onResize: 무서의 특정 요소의 크기가 변경될 때 발생
  - onSubmit : 폼의 submit 버튼을 눌렀을 때 발생
  - onReset : 폼의 reset 버튼 눌렀을 때 발생

~~~html
<!-- 인라인 이벤트 핸들러 - HTML 태그에 직접 이벤트 달기 -->
<img src="A.png" onmouseover="alert('msg')">
~~~

~~~js
// 고전 방식의 이벤트
객체.onClick = function() {
    alert("msg");
}
~~~

~~~js
// DOM : 이벤트 리스너 등록
addEventListener('이벤트 종류', '함수 이름');
removeEventListener();
~~~

##### 이벤트 처리 예제 - 인라인 방식 event1.html

~~~html
        <script type="text/javascript">
            function show() {
                alert("클릭2");
            }
        </script>
</head>
<body>
    <div onclick="alert('클릭1')">클릭1</div>
    <div onclick="show()">클릭2</div>
</body>
~~~

##### 이벤트 처리 예제 - 고전 방식 mouseEvent.html

~~~html
        <script type="text/javascript">
            window.onload = function() {
                var birdImg = document.getElementById('birdImg');

                birdImg.onmouseover = function() {
                    birdImg.style.opacity = 0.5; // 투명도
                }
                birdImg.onmouseout = function() {
                    birdImg.style.opacity = 1;
                }
            };

            // 문서 상에서 오른쪽 마우스 클릭했을 때 이벤트 처리
            document.oncontextmenu = function() {
                alert("오른쪽 마우스 사용을 금지 합니다.");
                // return false;
        
~~~

##### 이벤트 처리 예제 - 동일한 이벤트 여러 번 적용(마지막 하나만 적용된다) sameEvent.html

~~~html
        <script type="text/javascript">
            // 동일한 객체에 대해 동일한 이벤트를 여러 번 사용 불가
            // 마지막 이벤트 하나만 적용
            function show1() {
                alert("실행1");
            }
            function show2() {
                alert("실행2");
            }
            window.onload = show1();
            window.onload = show2(); // 마지막 이벤트만 처리
        </script>
~~~

### DOM 이벤트 리스너 등록
- addEventListener() 메소드 사용해서 이벤트 리스너 등록

~~~js
객체.addEventListener('이벤트명', function() { 

});
~~~

- 콜백 함수로 화살표 함수 사용할 경우

~~~js
객체.addEventListener('이벤트명',() => {

});
~~~

##### DOM 이벤트 리스너 등록 예제 addEventListner.html

~~~html
        <script type="text/javascript">
            window.onload = function() {
                var greenBtn = document.getElementById('greenBtn');
                var redBtn = document.getElementById('redBtn');
                var h2 = document.getElementById('h2');

                // 객체에 이벤트 리스너 등록 : click 이벤트
                greenBtn.addEventListener("click", function() {
                    h2.style.color = "green";
                });

                // 객체에 이벤트 리스너 등록 : mouseover 이벤트
                redBtn.addEventListener("mouseover", function() {
                    h2.style.color = "red";
                });
            };
        </script>
</head>
<body>
    <h2 id="h2">제목</h2>
    <button id="greenBtn">green</button>
    <button id="redBtn">red</button>
</body>
~~~

##### DOM 이벤트 리스너 등록 예제 - 동일 이벤트 처리 addEventListner2.html

~~~html
        <script type="text/javascript">
            window.onload = function() {
                var btn = document.getElementById('btn');

                btn.addEventListener("click", show1);
                btn.addEventListener("click", show2);
            };
            function show1() {
                alert("실행1");
            }
            function show2() {
                alert("실행2");
            }
            // 동일 이벤트 둘 다 처리가 가능하다.
        </script>
</head>
<body>
    <button id="btn">클릭</button>
</body>
~~~

##### DOM 이벤트 리스너 등록 예제 - 화살표 함수 addEventListner3.html

~~~html
        <script type="text/javascript">
            window.onload = function() {
                let box = document.getElementById("box");

                box.addEventListener("mousedown", () => {
                    box.style.background = 'green';
                });
                box.addEventListener("mouseup", event => {
                    event.currentTarget.style.background = 'white';
                });
            }
        </script>
~~~

## 폼 유효성 확인
- form 객체
  - document 객체의 하위 객체
  - form 태그 내에 있는 여러 입력 양식을 제어
  - form의 하위 객체들

## 사진

- from 객체 사용 방법
  1. 태그의 name 속성을 객체로 사용하는 경우
    - \<form name="newMemberForm">
    - \<input type="text" name="id">
    - newMemberForm.id.focus();
    - newMemberForm.id.value = “”;
    - newMemberForm.passwd.focus();

  2. 문서 객체 모델(DOM) 방식을 사용하는 경우
    - <input type=”text” id=”name”>
    - var name = document.getElementById(‘name’);
    - name.focus();
    - name.value = "";