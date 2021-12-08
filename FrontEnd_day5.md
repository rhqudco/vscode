# FrontEnd_day5 정리 (2021.12.08 수요일)

## 제어문
- Java와 동일하다
- 조건문
  - 조건의 결과가 참일 때, 거짓일 때 수행되는 문장이 각각 다르다.
  - if
  - if - else
  - if -else if
  - switch

#### 조건문 예시 코드

##### ifEx1.html

~~~html
        <script type="text/javascript">
            var max = 0;
            for(var i = 1; i <=3; i++) {
                var input = prompt("숫자" + i + " 입력")
                if(max < input) {
                    max = input;
                }
            }
            document.write("최대값 : " + max)
        </script>
~~~

##### ifEx2.html

~~~html
        <script type="text/javascript">
            var id = prompt("아이디 입력");
            var pw = prompt("비밀번호 압력");
            var rid = "abcd";
            var rpw = "1234";

            if(id == rid && pw == rpw) {
                document.write("로그인 성공.");
            }
            else{
                alert("아이디 또는 비밀번호가 일치하지 않습니다.");
                document.write("로그인 실패.");
            }
        </script>
~~~

##### ifEx3.html

~~~html
        <script type="text/javascript">
            var id = prompt("아이디 입력");
            var pw = prompt("비밀번호 압력");
            var rid = "abcd";
            var rpw = "1234";
            var quiz = "서울";
            if(id == rid && pw == rpw) {
                alert(id + "님 반갑습니다");
                var ans = prompt("대한민국의 수도는?");
                if(ans == quiz) {
                    document.write("정답입니다.");
                }
                else {
                    document.write("틀렸습니다. 대한민국의 수도는 서울입니다.")
                }
            }
            else{
                alert("아이디 또는 비밀번호가 일치하지 않습니다.");
                document.write("종료합니다.");
            }
        </script>
~~~

##### ifEx4.html

~~~html
        <script type="text/javascript">
            var prdNo = prompt("상품번호 입력", "1 또는 2 입력");
            var laptopPrice = 1200000;
            var airJordan = 100000;
            if(prdNo == 1 ) {
                let order = prompt("주문수량 입력");
                let total = laptopPrice * order;
                document.write("상품명 : 노트북<br>");
                document.write("가격 : 1,200,000원<br>");
                document.write("주문수량 : " + order + "개<br>");
                document.write("주문액 : " + total.toLocaleString() + "원<br>");
                document.write("할인액 : " + (total * 0.1).toLocaleString() + "원<br>");
                document.write("총 지불액 : " + (total * 0.9).toLocaleString() + "원<br>");
            }
            else if(prdNo == 2 ) {
                let order = prompt("주문수량 입력");
                let total = airJordan * order;
                document.write("상품명 : 운동화<br>");
                document.write("가격 : 100,000원<br>");
                document.write("주문수량 : " + order.toLocaleString() + "개<br>");
                document.write("주문액 : " + total.toLocaleString() + "원<br>");
                if( total < 500000) {
                    document.write("할인액 : 0 원<br>");
                    document.write("총 지불액 : " + total.toLocaleString() + "원<br>");
                }
                else if ( total >= 500000 && total < 1000000 ) {
                    document.write("할인액 : " + (total * 0.05).toLocaleString() + "원<br>");
                    document.write("총 지불액 : " + (total * 0.95).toLocaleString() + "원<br>");
                }
                else if ( total >= 1000000 ) {
                    document.write("할인액 : " + (total* 0.1).toLocaleString() + "원<br>");
                    document.write("총 지불액 : " + (total * 0.9).toLocaleString() + "원<br>");
                }
            }
            else {
                alert("잘못된 입력");
                document.write("종료합니다");
            }
        </script>
~~~

##### ifEx4-2.html

~~~html
        <script type="text/javascript">
            let prdNo = prompt("상품번호 입력", "1 또는 2 입력");
            if(prdNo == 1 || prdNo == 2) {
                let prdName, prdPrice, prdQyt, amount, discount, total;
                if(prdNo == 1) {
                    prdName = "노트북";
                    prdPrice = 1200000;
                } else {
                    prdName = "운동화";
                    prdPrice = 100000;
                }
                prdQyt = prompt("주문수량 입력");

                amount = prdPrice * prdQyt;
                if(amount >= 1000000) {
                    discount = amount * 0.1;
                }
                else if (amount >= 500000) {
                    discount = amount * 0.05;
                }
                else {
                    discount = 0;
                }
                total = amount - discount;
                document.write("상품명 : " + prdName + "<br>");
                document.write("가격 : " + prdPrice.toLocaleString() + "원<br>");
                document.write("주문수량 : "  + prdQyt + "개<br>");
                document.write("주문액 : " + amount.toLocaleString() + "원<br>");
                document.write("할인액 : " + discount.toLocaleString() + "원<br>");
                document.write("총 지불액 : " + total.toLocaleString() + "원<br>");
            }
            else {
                alert("잘못된 입력");
                document.write("종료합니다");
            }
        </script>
~~~

##### switchEx1.html

~~~html
        <script type="text/javascript">
            let value = prompt("1 ~ 3 까지 숫자를 입력.");
        switch(value) {
            case "1" : document.write("<img src=\"image/lizard.png\">");
            break;
            case "2" : document.write("<img src=\"image/lizardon.png\">");
            break;
            case "3" : document.write("<img src=\"image/megalizardon.png\">");
            break;
            default : alert("잘못 입력");
        }
        </script>
~~~

- 반복문
  - 반복문에 있는 조건에 따라 반복 횟수가 결정되고 반복 횟수만큼 반복
  - for
  - for in
  - while
  - do - while
  - forEach()
    - 배열.forEach()
    - 배열.forEach(function() { 실행문장 });
    - function()의 인수 3개가 지정되어 있는데, 사용하지 않아도 되지만 사용하는 경우 순서를 잘 지켜야 한다.
      - 첫 번째 인수 : 배열의 항목
      - 두 번째 인수 : 배열의 인덱스
      - 세 번째 인수 : 배열 그 자체
      - function(배열의 항목, 배열의 인덱스, 배열 그 자체)

#### 반복문 예시 코드

##### forEx1.html

~~~html
        <script type="text/javascript">
            var sum = 0;
            for(var i = 1; i <= 10; i++) {
                document.write("i = " + i + "<br>");
                sum += i;
            }
            document.write("sum = " + sum);
        </script>
~~~

##### forEx2.html

~~~html
        <script type="text/javascript">
            document.write("<ul><li>태그 반복 출력</li><ul><br>");
             for(var i = 1; i <= 10; i++) {
                document.write("<li type = \"square\" >" +  "i = " + i + "</li>");
            }
            document.write("</li></ul></ul>");
        </script>
~~~

##### forEx3.html

~~~html
    <style>
        th {background: yellow;}
        td {width: 80px; text-align: center;}
    </style>
        <script type="text/javascript">
            var sum = 0;
            document.write("<table border=\"1\" ><tr><th>i</th><th>sum</th></tr>")
                for(var i = 1; i <= 10; i++) {
                    sum += i;
                document.write("<tr><td>" + i + "</td><td>" + sum + "</td></tr>");
            }
            document.write("</table>");
        </script>
~~~

##### forinEx1.html

~~~html
        <script type="text/javascript">
            var fruits = ["사과", "포도", "복숭아"];
            for(var i in fruits) {
                document.write("fruits[" + i + "]" + " = " + fruits[i] + "<br>");
            }
        </script>
~~~

##### forEach.html

~~~html
        <script type="text/javascript">
                        var fruits = ["사과", "포도", "복숭아"];
                        fruits.forEach(function(item) {
                            document.write(item + "<br>");
                            // 사과
                            // 포도
                            // 복숭아 출력
                        });
                        document.write("<hr>")
                        fruits.forEach(function(item, index) {
                            document.write(item + " " + index + "<br>");
                            // 사과
                            // 포도
                            // 복숭아 출력
                        });
                        document.write("<hr>")
                        fruits.forEach(function(item, index, fruits) {
                            document.write(item + " " + index + " " + fruits + "<br>");
                            // 사과 0 사과,포도,복숭아
                            // 포도 1 사과,포도,복숭아
                            // 복숭아 2 사과,포도,복숭아 출력
                        });
                        
        </script>
~~~

##### nestedForEx.html

~~~html
        <script type="text/javascript">
            for(var i = 0; i < 4; i++) {
                for(var j = 0; j < 7; j++) {
                    document.write("<img src=\"image/apple.png\">");
                }
                document.write("<br>")
            }
            document.write("<hr>")
            for(var i = 1; i <= 4; i++) {
                for(var j = 1; j <= 7; j++) {
                    if( j%2 == 0 ) {
                        document.write("<img src=\"image/bomb.png\">");
                    }else {
                    document.write("<img src=\"image/apple.png\">");
                    }
                }
                document.write("<br>")
            }
        </script>
~~~

##### whileEx.html

~~~html
        <script type="text/javascript">
            var input = prompt("숫자 입력");
            var i = 0;
            document.write("<h1>총 " + input + "개의 이미지 출력</h1>")
            while( i < parseInt(input) ) {
                if( i%3 == 0){
                document.write("<img src=\"image/cherry.png\">");
                }
                else if ( i%3 == 1) {
                document.write("<img src=\"image/bomb.png\">");
                }
                else{
                document.write("<img src=\"image/apple.png\">");
                }
                i++;
            }
        </script>
~~~

##### doWhileEx.html

~~~html
        <script type="text/javascript">
            var count = 0;
            do {
                var check = confirm("계속 경고창을 보시겠습니까?");
                if(check == true) {
                    count++;
                    alert("경고 " + count);
                }
            }
            while(check == true) 
            document.write("경고창 출력 횟수 : " + count);
        </script>
~~~

## 정수(숫자)로 형변환
- prompt()에서 입력 받은 값은 모드 문자로 인식
  - 더하기 연산을 할 경우 문자 연산으로 처리
- 숫자로 연산하기 위해서는 숫자로 형 변환 필요
  - Number() : 숫자형으로 변환(실수형도 포함)
  - parseInt() : 정수형으로 변환

##### typeConversion.html

~~~html
<script type="text/javascript">
            // var n1 = prompt("숫자 1 입력"); 5 
            // var n2 = prompt("숫자 2 입력"); 10
            // document.write(n1 + n2 + "<br>"); 510
            // document.write(n1 * n2 + "<br>"); 50


            // var n1 = parseInt(prompt("숫자 1 입력")); 5 
            // var n2 = parseInt(prompt("숫자 2 입력"));10
            // document.write(n1 + n2 + "<br>"); 15
            // document.write(n1 * n2 + "<br>"); 50
            // parseInt는 정수형으로 변환

            var n1 = Number(prompt("숫자 1 입력")); // 123.45
            var n2 = parseInt(prompt("숫자 2 입력")); // 10
            document.write(n1 + n2 + "<br>"); // 133.45
            document.write(n1 * n2 + "<br>"); // 1234.5
            // Number는 실수형도 포함
        </script>
~~~

## 배열
- 동일한 이름을 갖는 원소들의 연속적 저장 영역
- 배열의 원소는 메모리 내에 순서대로 저장
- 배열의 각 원소는 인덱스([0]부터 시작)로 구별
- 배열 선언 형식
  - var 배열명 = new Array(3); // 크기가 정해진 배열
    - var arr = new Array(3);
  - var 배열명 = new Array(); // 크기가 정해지지 않은 배열
    - var arr = new Array();
  - var 배열명 = new Array(값1, 값2, 값3, ... , 값n); // 선언과 동시에 초기화
    - var arr = new Array(1, 2, 3, ... , n); 
  - var 배열명 = [값1, 값2, 값3, ... , 값n]; // 대괄호를 사용한 선언과 동시에 초기화
    - var arr = [1, 2, 3, ... , n];
- 배열 사용
  - 배열 원소에 값 저장
    - arr[n] = 10; // n번 인덱스(n+1 번째 위치)에 값 저장
  - 배열 출력
    - document.write(arr[n]);
  - 주의사항
    - 배열의 전체 원소에 값을 저장하거나 출력하기 위해서는 반복문 사용
    - 배열은 크기가 정해져 있기 때문에 반복 횟수를 정할 수 있으므로 for문 사용
    - 반복문은 반드시 0부터(배열을 처음부터 순회해야 할 경우) 시작한다.(배열의 인덱스가 0번부터 시작하기 때문) 
- 배열의 크기(원소의 개수)
  - arr.length
- 특징
  - 배열에 데이터 형식이 없기 때문에  각 원소에 다른 유형의 데이터 저장 가능

#### 배열 예시 코드

##### array.html

~~~html
        <script type="text/javascript">
            var num = new Array(5); // 크기가 5인 배열 생성

            var player = new Array(); // 크기가 정해지지 않은 배열 선언

            //  배열 선언과 동시에 초기화
            var fish = new Array("고등어", "갈치", "명태", "대구");
            var score = [84, 90, 75, 99];

            // 각 원소의 데이터 타입이 다른 경우
            var student = ["홍길동", 2, 95.3, 'A'];
            var student2 = new Array("홍길동", 2, 95.3, 'A');

            // num 배열의 각 원소 값 저장
            for(var i = 0; i < num.length; i++) {
                num[i] = i;
            }
            // player 배열에 각 원소 값 저장
            for(var i = 0; i < 3; i++) {
                player[i] = "선수" + ( i+1 );
            }

            document.write("num : ");
            for(var i = 0; i < num.length; i++) {
                document.write(num[i] + " ")
            }

            document.write("<br>player : ");
            for(var i = 0; i < player.length; i++) {
                document.write(player[i] + " ")
            }

            document.write("<br>fish : ");
            for(var i = 0; i < fish.length; i++) {
                document.write(fish[i] + " ")
            }

            document.write("<br>score : ");
            for(var i = 0; i < score.length; i++) {
                document.write(score[i] + " ")
            }

            document.write("<br>student : ");
            for(var i = 0; i < student.length; i++) {
                document.write(student[i] + " ")
            }
        </script>
~~~

##### arrayEx1.html

~~~html
        <script type="text/javascript">
            var colors = new Array(4);
            for(var i = 0; i < colors.length; i++) {
                colors[i] = prompt("색상 입력");
            }
            document.write("<ol type=\"A\">");
            for(var i = 0; i < colors.length; i++) {
                document.write( "<li>" + colors[i] + "</li>");
            }
            document.write("</ol>");
        </script>
~~~

##### arrayEx2.html

~~~html
        <script type="text/javascript">
            var student = new Array(4);
            for(var i = 0; i < student.length; i++) {
                student[i] = prompt("학생" + (i+1) + " 입력");
            }
            document.write("<table border=\"1\" width=\"200px\">")
            for(var i = 0; i < student.length; i++) {
                document.write("<tr align=\"center\"><td>" + (i+1) + "</td><td>" + student[i] + "</td></tr>");
            }
            document.write("/<table>")
        </script>
~~~

## 자바스크립트 함수
- 자동 호출되는 함수
- 선언적 함수(일반 함수 : function)
- 익명 함수
- 콜백 함수
- 화살표 함수
- 디폴트 매개변수

### 자동 호출함수 & 선언적 함수
- 독립적인 모듈
- 특정 기능을 수행하고 결과를 돌려주는 독립적인 코드 집합
- 메소드, 모듈, 기능, 프로시저 등으로 불림
- 함수를 사용하기 위해서는 반드시 호출해야 함
- 함수 선언 형식
  - function 함수명() { 함수가 수행하는 문장; }
- 자동 호출되는 함수 : 스스로 동작하는함수
  - (function() { 함수가 수행하는 문장} })();
- 함수 사용
  - 함수를 사용하기 위해서는 반드시 호출해야 함
  - 함수를 만들었다고 해서 스스로 기능을 수행하는 것은 아님
  - 함수 호출 방법 : 함수명() (함수 이름만 호출하면 수행이 된다)
  - function show() { alert("show()함수 입니다"); }
    - 함수 호출
      - show(); // 방법 1 : 필요한 곳에서 호출
      - \<body onLoad="show()"> // 방법 2 : HTML 이벤트 속성에서 호출
      - function show() { alert("show()함수 입니다"); input(); // 다른 함수 호출 } // 방법 3 : 다른 함수 내에서 호출

#### 함수 예제 코드

##### function1.html

~~~html
        <script type="text/javascript">
            // 자동 호출되는 함수 : 호출하지 않아도 스스로 동작하는 함수
            (function() {
                alert("자동 실행");
            })();
            // 함수 정의(함수 선언) - 선언과 동시에 정의
            function show() {
                alert("show()함수 입니다.");
            }
            // 함수 호출
            show();
        </script>
</head>
<!-- HTML 태그 이벤트에서 함수 호출 -->
<!-- <body onload="show()"> -->
~~~

##### function2.html

~~~html
        <script type="text/javascript">
            // 다른 함수 내에서 함수 호출
            function start() {
                var answer = confirm("배경색을 변경하시겠습니까?")
                if(answer) {
                    changeColor();
                }
                else {
                    alert("취소하였습니다.");
                }
            }
            function changeColor() {
                var color = prompt("색상 입력", "red / blue / green");
                document.write(color);
                document.bgColor = color;
            }
            start();
        </script>
~~~

##### functionEx1.html

~~~html
        <script type="text/javascript">
            function input() {
                var color = prompt("색상 입력", "red / blue / green");
                document.bgColor = color;
            }
        </script>
</head>
<body>
    <button onclick="input()">색상 입력</button>
</body>
~~~

##### functionEx2.html

~~~html
        <script type="text/javascript">
            function input() {
                num = prompt("숫자 입력");
                show();
            }
            function show() {
                for (var i = 0; i < num; i++) {
                    document.write("★")
                }
            }
        </script>
</head>
<body>
    <button onclick="input()">숫자 입력</button>
</body>
~~~