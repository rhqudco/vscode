# FrontEnd_day6 정리 (2021.12.09 목요일)

## 자바스크립트 함수
- 자동 호출되는 함수
- 선언적 함수(일반 함수 : function)
- 익명 함수
- 콜백 함수
- 화살표 함수
- 디폴트 매개변수

## 함수의 반환 값
- 함수 실행이 끝난 후 호출한 곳으로 돌려주는 결과 값
- 함수 내에서 return문 사용

~~~js
            function sum() {
                return n1 + n2;
            }
            var s = sum();
            document.write("합계 : " + sum());
~~~

##### 함수의 반환 값이 있는 예제 functionReturn.html

~~~js
            function sum() {
                var n1 = Number(prompt("숫자 1 입력"));
                var n2 = Number(prompt("숫자 2 입력"));
                return n1 + n2;
            }
            document.write("합계 : " + sum());
~~~

##### 함수 반환 값 있는 연습 문제 functionReturnEx1.html

~~~html
        <script type="text/javascript">
            function start() {
                var scoreInput = confirm("성적을 입력하시겠습니까?")
                if(scoreInput) {
                    alert("평균 : " + input());
                }
                else {
                    alert("종료합니다.")
                    document.body.innerHTML = "";
                }
            }
            function input() {
                var korean = Number(prompt("국어 점수를 입력해 주세요."));
                var math = Number(prompt("영어 점수를 입력해 주세요."));
                var eng = Number(prompt("영어 점수를 입력해 주세요."));

                return ((korean+math+eng) / 3).toFixed(2);
                 // .toFixed(소수점 이하 자릿수);
            }
        </script>
</head>
<body>
    <button onclick="start()">성적 입력</button>
</body>
~~~

## 매개변수가 있는 함수
- 함수 호출 시 전달된 값을 받기 위해 사용되는 변수
- 함수 내에서 지역 변수로 사용
- 매개변수가 있는 함수 호출은 반드시 값을 전달해야 한다.
  - 함수 호출하며 전달하는 값을 인수(또는 인자)라고 한다.

~~~js
function sum(x, y) { // 함수 내에서만 사용하는 지역변수로 사용한다.
    return x+y; 
}
document.write("합계 : " + sum(10 + 20));
~~~

##### 매개변수 함수 예제 functionParam.html

~~~html
        <script type="text/javascript">
            function calinterest(deposit, rate) { // 예금액과 이자율을 전달 받아 예금 이자를 출력하는 함수.
                var interest = deposit * rate / 100;
                document.write("예금이자 : " + interest + "원");
            }
            function input() { // 예금액과 이자율 입력 받아서 calinterest에 전달하는 함수
                var deposit = parseInt(prompt("예금액 입력"));
                var rate = parseInt(prompt("이율 입력"));
                calinterest(deposit, rate);
            }
            input();
        </script>
~~~

##### 매개변수 함수 연습 functionParamEx1.html

~~~html
        <script type="text/javascript">
            function input() {
                var row = prompt("행 입력");
                var col = prompt("열 입력");
                makeTable(row, col);
            }
            function makeTable(row, col) {
                document.write("<table border=\"1\">");
                    for(var i = 0; i < row; i++) { // 행 수 만큼 반복
                        document.write("<tr>")
                        for(var j = 0; j <col; j++) { // 각 행마다 열 수 만큼 반복
                            document.write("<td>★</td>");
                        }
                        document.write("</tr>")
                    }
                document.write("</table>");
            }
        </script>
</head>
<body>
    <button onclick="input()">테이블 만들기</button>
</body>
~~~

##### 매개변수, 반환값 있는 함수 functionParamReturnEx1.html

~~~html
        <script type="text/javascript">
            function input() {
                var arr = new Array(5);
                for(var i = 0; i < arr.length; i++) {
                    arr[i] = prompt("배열 arr[" + i + "]번 인덱스 입력");
                }
                document.write("최대 값 : " + max(arr));
            }
            function max(arr) {
                var max = 0;
                for(var i = 0; i < arr.length; i++) {
                    if(max < arr[i]) {
                        max = arr[i]
                    }
                }
                return max;
            }
        </script>
</head>
<body onload="input()">
</body>
~~~

##### function 함수 호이스팅 functionHoisting.html

~~~html
        <script type="text/javascript">
            show(); // 선 호출
            function show() { // 후 정의
                alert("호이스팅 show() 함수");
            }
        </script>
~~~

## 익명 함수(Anonymous Function)
- 함수 이름이 없는 함수
- 함수명 대신, 함수명에 함수 코드를 저장해서 구현하는 함수
- 변수명에 값을 대입하는 형식으로 맨 끝에 세미콜론 작성.
- 함수 호출 시 변수명을 함수명처럼 사용
- __var 변수명 = function() { 함수 블록 수행 문장 @@@ };__
- 변수명 다르게 함수 코드 저장 가능
- 호이스팅 불가능
- Callback 함수로 주로 사용

##### 익명 함수 예제 anonymousFunction.html

~~~html
        <script type="text/javascript">
            // 익명 함수는 호이스팅 불가
            //  sum(100, 200); // sum is not a function
            // 익명 함수 : 변수명에 함수 코드 저장
            var sum = function(a, b) {
                document.write(a + b + "<br>");
            }; // 세미 콜론 작성.
            
            // 함수 호출 시 변수명을 함수명처럼 사용
            sum(5, 10); // 15
            // 다른 변수 add 이름으로 기존 sum 재사용
            var add = sum(10, 20); // 30
            // sum 함수도 그대로 사용 가능
            sum(3, 10); // 13
        </script>
~~~

## 콜백 함수(Callback Function)
- 매개변수로 함수를 전달 받아, 함수 내부에서 실행하는 함수
- 인자로 전달되는 함수를 콜백 함수라고 부름
- 콜백 함수로는 주로 익명 함수 사용
- 자바스크립트의 비동기 처리 방식의 문제점을 해결하기 위해 사용하는 함수
  - 자바스크립트는 싱글 스레드로 한 번에 하나의 작억만 처리 가능
  - 특정 코드(작업)가 끝나기 전에 다음 코드(작업)을 처리할 수 없다.
  - 콜백 함수를 사용해서 특정 시점에 호출하여 비동기 처리 작업 수행
  - 콜백 함수 패턴을 사용하면 작업1을 진행 시키고 작업이 완료되었을 때 알림을 받을 콜백 함수를 설정해서 작업1이 완료되면 콜백 함수가 호출되고, 해당 콜백 함수 안에서 작업2를 시작하는 식으로 비동기 작업들 순차적으로 처리 가능
  - 콜백 함수가 계속 호출되면 감당하기 어려울 정도로 깊어지는 문제가 발생(콜백지옥)
    - 이를 해결하기 위해 __Promise__ 를 사용한다.(미래 어떤 시점 결과를 제공하는 방식)
  - 비동기 처리 방식
    - 특정 코드(작업)이 끝나기 전에 다음 코드(작업)을 처리하는 방식

##### 콜백 함수 예제 callback1.html

~~~html
        <script type="text/javascript">
            // 익명 함수를 콜백 함수로 사용
            var callback = function() {
                alert("익명 함수");
            };
            // 함수를 매개변수로 받을 함수
            function show(a) { // 매개변수로 다른 이름 사용해도 상관 없다.
                // 매개변수로 전달될 함수 호출
                a();
            }
            // show 호출하며 함수를 인자로 전달
            show(callback);
        </script>
~~~

##### 콜백 함수 예제 callback2.html

~~~html
        <script type="text/javascript">
            // 일반 함수를 콜백 함수로 사용
            function endFunction() {
                document.write("종료");
            }
            
            function showName(name, callback) { // endFunction()을 callback이라는 매개변수 이름으로 받음
                document.write("name : " + name + "<br>");
                callback(); // 받음 이름(매개변수 명)으로 호출
            }
            showName("홍길동", endFunction);
        </script>
~~~

##### 콜백 함수 예제 callback3.html

~~~html
        <script type="text/javascript">
            // 지역변수를 콜백함수 매개변수로 전달
            let globalVar = 100;
            // 익명 함수
            var show = function(localVar) {
                document.write(`전역변수 : ${globalVar} / 지역변수 : ${localVar}`);
            }
            // 전달된 show 함수를 callback으로 받음
            function call(callback) {
                let localVar = 1;
                callback(localVar); // show 호출하면서 localVar 전달.
            }
            call(show);
        </script>
~~~

## 화살표 함수 (Arrow Function)
- __=>__ 사용
- 자바 언어의 람다식과 동일하다.
- function 키워드 대신 화살표(=>)를 사용하여 더 간략한 방법으로 함수를 선언하는 방식
- 기본 문법
  - (매개변수) => { 함수 실행 부분 };
  - ( ) => { 함수 실행 부분 }; // 매개변수가 없는 경우
  - x => { 함수 실행 부분 }; // 매개변수가 한 개인 경우 괄호 생략 가능
  - (x, y) => { 함수 실행 부분 }; // 매개변수가 여러 개인 경우 괄호 생략 불가능
  - x => x * x;  // 수행 문장이 한 줄인경우 중괄호 생략 가능

~~~js
객체.addEventListener(‘click’, function(){
수행 문장;
         });
	// 화살표 함수 사용
객체.addEventListener(‘click’, ( ) => {
수행 문장;
         });

~~~

##### 화살표 함수 예제 arrowFunction1.html

~~~html
        <script type="text/javascript">
			// 화살표 함수
			// 익명 함수. 매개변수 2개 (a, b). 반환값은 a+b (return 키워드 생략)
			// 화살표 함수를 사용
			let sum = (a, b) => a+ b;
			
			//익명 함수 sum에 화살표 함수 사용하지 않은 경우
	        /*let sum = function(a, b){
				return a + b;
			} */
			
			alert(sum(10, 20));
        </script>
~~~

##### 화살표 함수 예제 arrowFunction2.html

~~~html
        <script type="text/javascript">
              var fruits = ["사과", "포도", "복숭아"];
              // 화살표 함수를 사용해서 반환
              fruits.forEach( (item, index, fruits) => {
                document.write(item + " " + index + " " + fruits + "<br>");
              } );
        </script>
~~~


## 디폴트 매개변수
- 함수의 매개변수에 기본값을 설정하는 것.
- 일반 매개변수와 같이 사용할 경우 디폴트 매개변수는 맨 뒤에 위치한다.

##### 디폴트 매개변수 예제 defaultParam.html

~~~html
        <script type="text/javascript">
            function rect(width=10, height=20) {
                document.write("width : " + width);
                document.write(" height : " + height + " <br>");
                return width*height;
            }
            document.write(rect() + "<br>");
            document.write(rect(30) + "<br>");
            document.write(rect(100, 200) + "<br>");
            // width : 10 height : 20
            // 200
            // width : 30 height : 20
            // 600
            // width : 100 height : 200
            // 20000
            /////////////////////////////////////////////////////////////////////////////////
            document.write("<hr>")
            function showInfo(name, year=4, score) {
                document.write("name : " + name + "<br>");
                document.write("year : " + year + "<br>");
                document.write("score : " + score + "<br>");
            }
            showInfo();
            // name : undefined
            // year : 4
            // score : undefined
            showInfo("홍길동");
            // name : 홍길동
            // year : 4
            // score : undefined
            showInfo("홍길동", 80);
            // name : 홍길동
            // year : 80
            // score : undefined
            /////////////////////////////////////////////////////////////////////////////////
            document.write("<hr>")
            function showInfo2(name, score, year=4) { // 디폴트 매개변수는 맨 뒤에 위치해야 한다.
                document.write("name : " + name + "<br>");
                document.write("year : " + year + "<br>");
                document.write("score : " + score + "<br>");
            }
            showInfo2();
            // name : undefined
            // year : 4
            // score : undefined
            showInfo2("홍길동");
            // name : 홍길동
            // year : 4
            // score : undefined
            showInfo2("홍길동", 80);
            // name : 홍길동
            // year : 4
            // score : 80
        </script>
~~~

## 자바스크립트 객체
- 내장객체
- 브라우저 객체
- 문서 객체(DOM)
- 사용자 정의 객체

### 내장 객체(Built in Object)
- 미리 정의되어 있는 객체
- 선언 과정을 통해 객체 변수를 정의해서 사용
- 특별한 경우에만 사용자 정의 객체를 정의하여 사용하고 대부분 경우 내장 객체 사용.
- 대표적인 내장 객체
  - Date : 날짜와 시간을 처리하기 위한 객체
  - Array : 배열을 만들기 위한 객체
  - String: 문자열을 다루기 위한 객체
  - Math : 수학 계산을 위한 객체
  - Event : 발생하는 이벤트에 관한 정보를 제공하는 객체
  - Screen : 화면의 해상도, 색상, 크기에 관한 정보를 제공하는 객체
- 객체 생성 및 사용 예
  - 객체 생성
    - var today = new Date(); // Date 객체 생성
    - var arr = new Array(3); // Array 객체  생성
  - 객체 사용
    - 객체.메소드();
    - today.getMonth();
    - arr.sort();

### Date 객체
- 날짜와 시간을 관리해주는 내장 객체
- 웹 페이지에 오늘 날짜와 시간, 요일 등 표시
- var today = new Date(); 
-  today.getMonth();
-  Date 객체의 메소드
   - get 메소드 (시간 / 날짜 정보를 반환)
      - getYear() : 1970년도 이후의 연도 반환 / getFullYear()
      - getMonth() : 월 반환 (0 = 1월, 1 = 2월, 2 = 3월, ... 11 = 12월)
      - getDate() : 일 반환
      - getDay() : 요일 반환 (0 = 일요일, 1 = 월요일, ... 6 = 토요일)
      - getHours() : 시 반환 (0 ~ 23)
      - getMinutes() : 분 반환 (0 ~ 59)
      - getSeconds() : 초 반환 (0 ~ 59)
      - getTime() : 1970년 1월 1일 이후 시간을 1/1000 단위로 표시
   - set 메소드 (시간 / 날짜 정보를 설정)
      - setYear() : 1970년도 이후의 연도 설정
      - setMonth() : 월 설정 (0 = 1월, 1 = 2월, 2 = 3월, ... 11 = 12월)
      - setDate() : 일 설정
      - setHours() : 시 설정 (0 ~ 23)
      - setMinutes() : 분 설정 (0 ~ 59)
      - setSeconds() : 초 설정 (0 ~ 59)
      - setTime() : 1970년 1월 1일 이후 시간을 1/1000 단위로 설정
    - 날짜 / 시간 정보의 포맷을 변경하는 데 사용하는 메소드
      - parse(날짜 문자열) : 문자열을 시간으로 변경
      - toGMTString() : 문자열을 GMT 날짜로 복귀
      - toLocaleString() : 날짜를 문자열로 변환 

##### Date 객체 예제 date.html

~~~html
<script type="text/javascript">
            var today = new Date();

            var year = today.getFullYear();
            var month = today.getMonth() + 1;
            var date = today.getDate();
            var day;
            switch(today.getDay()) {
                case 0: day="일"; break;
                case 1: day="월"; break;
                case 2: day="화"; break;
                case 3: day="수"; break;
                case 4: day="목"; break;
                case 5: day="금"; break;
            default : day="토"; break;
            }
            document.write("오늘은 " + year + "년 " + month + "월 " + date + "일 " + day + "요일입니다.");

            var hour = 24;
            var minute = today.getMinutes();
            var second = today.getSeconds();
            var ampm;

            document.write("<br>지금은 " + hour + "시 " + minute + "분 " + second + "초 입니다.");

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
            document.write("<br>지금은 " + ampm + hour + "시 " + minute + "분 " + second + "초 입니다.");
        </script>
~~~

### Array 객체
- 배열 내장 객체
- var arr = new Array(3); // Array 객체  생성
 - arr.sort();
 - Array 객체 주요 메소드
   - unshift(데이터) :  배열 맨 앞에 요소 추가
   - shift() : 첫 번째 요소 삭제
   - push(데이터) : 배열 마지막에 요소 추가
   - pop() : 마지막 요소 삭제
   - reverse() : 배열 순서를 역순으로 변경
   - sort() : 오름차순으로 정렬
   - slice(start, end) : start ~ end-1 범위의 요소를 추출하여 새로운 배열으로 생성
   - splice(위치, 개수, 데이터) : 특정 위치에 개수만큼 요소 삭제하고 데이터 추가

##### Array 객체 예제 arrayObject.html

~~~html
        <script type="text/javascript">
            var fruits = new Array("사과", "복숭아", "포도");

            document.write("모든 요소 출력<br>");
            for(var i = 0; i < fruits.length; i++) {
                document.write(fruits[i] + " ");
            }
            document.write("<hr>");
            fruits.shift(); // 첫 번째 요소 제거
            document.write("shift 후 요소 출력<br>");
            for(var i = 0; i < fruits.length; i++) {
                document.write(fruits[i] + " ");
            }
            document.write("<hr>");
            fruits.unshift("배"); // 첫 번째 요소에 추가
            document.write("unshift 후 요소 출력<br>");
            for(var i = 0; i < fruits.length; i++) {
                document.write(fruits[i] + " ");
            }
            document.write("<hr>");
            fruits.pop(); // 마지막 요소 제거
            document.write("pop 후 요소 출력<br>");
            for(var i = 0; i < fruits.length; i++) {
                document.write(fruits[i] + " ");
            }
            document.write("<hr>");
            fruits.push("딸기"); // 마지막에 요소 추가
            fruits.push("수박");
            document.write("push 후 요소 출력<br>");
            for(var i = 0; i < fruits.length; i++) {
                document.write(fruits[i] + " ");
            }
            document.write("<hr>");
            fruits.reverse(); // 역순으로 변경
            document.write("reverse 후 요소 출력<br>");
            for(var i = 0; i < fruits.length; i++) {
                document.write(fruits[i] + " ");
            }
            document.write("<hr>");
            fruits.sort(); // 오름차순 정렬
            document.write("sort 후 요소 출력<br>");
            for(var i = 0; i < fruits.length; i++) {
                document.write(fruits[i] + " ");
            }
            document.write("<hr>");
            fruits.splice(2, 1, "망고", "오렌지"); // splice 작업 2번 인덱스부터 1개를 삭제하고 망고, 오렌지 추가
            document.write("splice 후 요소 출력<br>");
            for(var i = 0; i < fruits.length; i++) {
                document.write(fruits[i] + " ");
            }
            document.write("<hr>");
            var newFruits = fruits.slice(1, 4); // slice 작업 1번 인덱스부터 4-1번 인덱스까지 데이터를 잘라서 새 배열 생성
            document.write("slice 후 요소 출력 (newFruits)<br>");
            for(var i = 0; i < newFruits.length; i++) {
                document.write(newFruits[i] + " ");
            }
            document.write("<br>slice 후 요소 출력 (fruits)<br>");
            for(var i = 0; i < fruits.length; i++) {
                document.write(fruits[i] + " ");
            }
        </script>
~~~

### Math 객체
- 수학적 계산에 필요한 함수나 상수 값 제공
- 상수 값은 속성으로, 수학 함수는 메소드로 제공
- Math 객체는 속성이나 메소드에 접근하기 위해 따로 객체 변수 선언하지 않고 Math 클래스 이름 그대로 사용
- 형식
  - Math.속성
  - Math.메소드
- Math 객체의 주요 메소드
  - sin(x) : sin
  - cos(x) : cos
  - tan(x) : tangent
  - abs(x) : 절대값
  - exp(x) : 지수 함수
  - log(x) : 로그 함수
  - random(x) : 난수 함수
  - pow(x ,y) : 지수
  - sqrt(x) : 제곱근
  - round(x) : 반올림
  - floor(x) : 버림
  - ceil(x) : 올림
  - max(x, y) : 최대값
  - min(x, y) : 최소값
- Math.random()
  - 0.0x ~ 0.9x 사이의 실수 형태의 값으로 난수 발생
  - 정수값으로 사용하기 위해서는 곱하기 10을 하고, Math.floor() 메소드로 소수점 이하 값을 버린 후 시작 값 더해서 사용
  - 예 : 1 ~ 10 사이의 난수 발생
  - var num = 1 + Math.floor(Math.random() * 10);

##### Math.random() 연습문제 random.html

~~~html
        <script type="text/javascript">
            var num = 1 + Math.floor(Math.random() * 3);

            document.write(`<img src="image/그림${num}.jpg"> <br> 그림${num}.jpg  난수 :  ` + num);
        </script>
~~~

## String 객체
- 문자열 객체
- var name = “홍길동’; // 상수 형태 문자열 (객체로 자동 변환 : 일시적)
- var name = new String();
- new를 이용해서 객체를 생성하지 않고 상수 형태(“문자열”)로 문자열을 만들어도 문자열 객체의 특징 모두 사용
- String 객체의 주요 메소드
  - charAt() : 인덱스로 지정된 위치의 문자 반환
  - indexOf("찾고자 하는 문자") : 문자열에서 특정 문자의 위치를 인덱스 값으로 반환(인덱스는 0부터) 발견하지 못하면 -1 반환
  - lastIndexOf() :문자열 끝에서부터 검색하여 위치 반환
  - subString(start, end) : 문자열의 일부분(start ~ end-1) 추출
  - slice() : 문자열의 일부분 추출(오른쪽 끝(음수) 지정 가능)
  - substr() : 문자열의 일부분 추출(추출할 문자 개수 지정)
  - toUpperCase() : 문자열을 모두 대문자로 변경
  - toLowerCase() : 문자열을 모두 소문자로 변경
  - concat() : 문자열 연결
  - split("구분자") : 구분자를 기준으로 문자열 분리되어 배열에 순서대로 저장

##### String 객체 연습 예제 string.html

~~~html
        <script type="text/javascript">
            var name = new String("홍길동");
            // var name = "홍길동"; 과 동일

            document.write(name.bold());
            document.write(name.sub());
            document.write(name.sup());
            document.write(name.italics());
            document.write(name.fontcolor("red"));
            document.write(name.fontsize(5));
            document.write(name.fontsize(6).fontcolor("blue"));
        </script>
~~~

##### String 객체 연습 문제 charAtEx1.html

~~~html
        <script type="text/javascript">
            var input = prompt("숫자를 입력해 주세요.")
            for(var i=0; i<input.length; i++){
				if(!('0' <= input.charAt(i) && input.charAt(i) <='9')){
					alert("숫자 형식이 아닙니다!");
					break;
				}
            }
        </script>
~~~

##### String 객체 연습 문제 subStringEx1.html

~~~html
        <script type="text/javascript">
            var birth = prompt("생년월일 입력", "예 : 19990101");
            document.write(birth.substring(0, 4) + "년 " + birth.substring(4, 6) + "월 " + birth.substring(6, 8) + "일에 태어나셨군요");
        </script>
~~~

##### String 객체 연습 문제 indexOfEx1.html

~~~html
        <script type="text/javascript">
            var email = prompt("이메일 입력");
            if(email.indexOf("@") == -1 || email.indexOf(".") == -1 || (email.indexOf("@") > email.indexOf("."))) {
                alert("이메일 형식이 아닙니다.")
                document.write(email);
            }
        </script>
~~~

##### String 객체 연습 문제 splitEx1.html

~~~html
        <script type="text/javascript">
            var birth = prompt("생년월일 입력", "예 : 1999-01-01");
            var date = birth.split("-");
            document.write(date[0] + "년 " + date[1] + "월 " + date[2] + "일")
        </script>
~~~