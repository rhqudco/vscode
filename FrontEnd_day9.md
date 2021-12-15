## jQuery 선택자
- jQuery 코드는 선택자와 메소드의 조합으로 구성되는 경우가 많음
- 중간에 자바스크립트 코드 같이 작성
- HTML 태그를 쉽게 선택하기 위해 선택자 사용
- 선택자 구조
  - $(‘선택자’).메소드(매개변수, 함수 등)
  - $(‘span’).hide();
  - 큰 따옴표 / 작은 따옴표 다 사용 가능
- 선택자 종류
  - 직접 선택자
    - 전체 : $("*")
    - 태그 : $("태그명")
    - 아이디 : $("#id 명")
    - 클래스 : $(".class 명")
    - 그룹 선택자
  - 인접 관계 선택자
    - 상위 요소(조상/부모) 선택자
    - 하위 요소 (자식/자손) 선택자
    - 형제 선택자
  - 필터 선택자
  - 속성 선택자
  - 컨텐츠 탐색 선택자

### 조상/부모/형제 요소 선택자
- 부모 요소 선택 : parent()
- 조상 : parents()
- 형제 : next() / nextAll() / nextUntil() / prev() / prevAll() / prevUntil()
- __parentNext.html__
~~~html
<style type="text/css">
			div {
				border:1px solid #000000;
				padding:10px;
				display:inline-block;
			}
		</style>
	<script src="jquery-3.6.0.min.js"></script>
	<script type="text/javascript">
	   $(document).ready(function() {
			$('p').parents().css('backgroundColor', 'Yellow'); // 모든 조상
			$('p').parents('#area').css('backgroundColor', 'white'); // 원하는 것만 넣어줌 (조상 area)
			$('p').parents('#c1, #c2').css('backgroundColor', 'brown'); // 원하는 조상 (c1, c2)
			$('p').parent().css('backgroundColor', 'green'); // parent(s 빠짐)는 $('p').parent()에서 p의 부모만
			$('#c1').next().css('backgroundColor', 'pink'); // c1을 기준으로 다음 요소
			$('#c2').nextAll().css('backgroundColor', 'orange'); // c2를 기준으로 다음에 오는 모든요소
			$('#c4').prevAll().css('color', 'blue'); // c4를 기준으로 전에 있는 모든 요소 글자색 변경
			// c1다음,c4 이전까지(c2, c3)
			$('#c1').nextUntil('#c4').css('borderRadius', '20px');
			// c3이전, c1 다음 c2)
			$('#c3').prevUntil('#c1').css('border', 'solid 5px red');
	   });
	</script>            
	</head>
	<body>		
        <h3>조상/부모/형제 요소 선택자</h3>      
        <div id="area">  
        	area 영역 
            <div id="c1">
            	c1영역
                <div id="s1">
                	s1 영역
                    <p>p</p>
            	</div>
            </div>	 
            <div id="c2">
            	c2영역
                <div id="s2">
                	s2 영역
                	<p>p</p>
            	</div>
            </div>
            <div id="c3">
            	c3영역
                <div id="s3">
                	s3 영역
                	<p>p</p>
            	</div>
            </div>
            <div id="c4">
            	c4영역
                <div id="s4">
                	s4 영역
                	<p>p</p>
            	</div>
            </div>
         </div>   	
	</body>
~~~

### 필터 선택자
- 태그의 상태나 순서 등으로 선택
- ${‘태그명:순서필터’)
  - $(‘tr:odd’) : 홀수 행만 선택
- ${‘태그명:상태필터’)
  - $(‘input:checked’) : 체크 상태인 input 태그 선택
- 요소 : 필터
  - 요소 : odd - 홀수 번째 위치한 요소 선택
  - 요소 : even - 짝수 번째
  - 요소 : first - 첫 번째
  - 요소 : last - 마지막
  - 요소 : checked - 체크된 요소 선택(radio나 checkbox)
  - 요소 : selected - 선택된 요소 선택(select의 option selected)
  - 요소 : disabled - 비활성 입력 양식 요소 선택
  - 요소 : enabled - 활성화된 입력 양식 요소 선택
  - 요소 : focus - 커서가 놓여진 입력 양식 요소 선택
  - 요소 : eq(n) - n번째(equal)
  - 요소 : not(선택자) - 선택자와 일치하지 않은 요소 선택
  - 요소 : lt(n) - n번째 미만(less than)
  - 요소 : gt(n) - n번째 초과(greater than)
  - 요소 : has(선택자) - 선택자를 갖고 있는 요소 선택
  - 요소 : nth:child(숫자n) - n의 배수 : nth-child(3n) : 0, 3, 6 ...(번째)
  - 요소 : nth:child(숫자n+1) - n+1의 배수 : nth-child(3n+1) : 1, 4, 7 ...(번째)
- filterSelector.html
~~~html
<script type="text/javascript">
       $(document).ready(function() {
           // 1. 홀수행 선택(1, 3, 5) (행 인덱스 0 부터 시작)
            $('#table1 tr:odd').css('background-color', 'gray');
            // 2. 짝수행 선택 (행 인덱스 0 부터 시작)
            $('#table1 tr:even').css('background-color', 'green');
            // 3. 첫 번째 행 선택 (행 인덱스 0 부터 시작)
            $('#table1 tr:first').css({'background-color':'gray', 'fontsize':'20pt'});
            // 4. 특정 행 선택 : tr의 5행(여섯번째 행)
            $('#table1 tr:eq(5)').css('color', 'red');
            // 4. 특정 행 선택 : tr의 5행(여섯번째 행)
            $('#table1 tr:gt(5)').css('color', 'blue');
            // table2에서 찾기
            // 6. tr의 0행 제외하고 모두 선택
            $('#table2 tr:not(0)').css('background', 'gold');
            // nth : 서수(~번째)
            // 7. nth-child(숫자n+1) : 3n+1번째 : 3의 배수 + 1 번째 선택 : 1, 4, 7, 10
            $('#table2 tr:nth-child(3n+1)').css('background-color', 'orange');
            // 7. 짝수 열 선택(2n)
            $('#table2 td:nth-child(2n)').css('background-color', 'red');
       });
    </script>      
~~~

### 속성 선택자
- HTML 태그(요소)의 지정된 속성 값에 따라 선택자로 정의
- 문법
  - 태그명[속성] : []안의 속성을 포함하는 모든 태그 선택
  - 태그명[속성="값"] : 속성 값이 주어진 값과 동일한 모든 태그 선택
  - 태그명[속성^="값"] : 속성 값이 주어진 값으로 시작하는 모든 태그 선택
  - 태그명[속성$="깂"] : 속성 값이 주어진 값으로 끝나는 모든 태그 선택
  - 태그명[속성*="값"] : 속성 값이 주어진 값을 포함하는 모든 태그 선택
- __attrbSelector.html__

~~~html
    <script src="jquery-3.6.0.min.js"></script>
    <script type="text/javascript">
       $(document).ready(function() {
         // 속성 type 선택
            $('input[type]').css('backgroundColor', 'pink');
            // 속성 type중 text인 것만 선택
            $('input[type=text]').css({'color':'blue', 'width':'200px'});
            // submit과 reset 버튼 선택
            // $('input[type=submit], input[type=reset]')
            // 축약형
            $(':submit, :reset').css('backgroundColor', 'gold');
            // password 선택
            // 축약형, 메소드체인 방식
            $(':password').css({'backgroundColor':'green', 'color':'red'}).css('width', '200px');
            // option 태그 선택
            $('option[value=프로그래머').css('color', 'red');
            // option 태그의 value 속성이 '웹'으로 시작하는 요소 선택
            $('option[value^=웹').css('color', 'blue');
            // option 태그의 value 속성이 '사'로 끝나는 요소 선택
            $('option[value$=사').css('color', 'green');
       });
    </script>
~~~

## 선택한 요소를 변수에 저장
- 형식
  - var $변수명 = $('선택자');    
  - var 변수명 = document.getElementById('#id');
  - 여러 개 찾은 경우 배열로 저장
    - var tds = document.getElementByTagName(‘td’);
  - 주의
    - jQuery 선택자를 찾아서 자바스크립트 변수에 저장한 경우는 jQuery 메소드 사용 가능
    - DOM 선택 방식으로 선택해서 자바스크립트 변수에 저장한 경우 jQuery  메소드 사용 불가능

##### 변수 저장 예제 - select-Variable.html

~~~html
    <script src="jquery-3.6.0.min.js"></script>
    <script type="text/javascript">
        $(document).ready(function(){
            $('.group1').css({
                float: 'left',
                background:'blue',
                color:'white',
                width: '90%',
                height: '30px'
            });
            
            $('.group2').css({
                float: 'right',
                background:'yellow',
                color:'black',
                width: '90%'
            });

                //(1)
	            // jQuery  변수 사용 : $변수명
	            /* var $divs = $('div');    // $divs : jQuery 변수
	            //alert($divs.length);      // 속성 사용
	            $divs.css('color', 'red')      // 메소드 사용  */
	            
	            // (2)
	            // 변수명에서 $ 제거하고 사용 : 자바스크립트 변수(객체)로 사용
	            // 
	            // var divs2 = $('div');      // divs2 : 자바스크립트 변수
	            // //alert(divs2.length);
	            // divs2.css('color', 'pink')  // css() 메소드 적용 되었음
	            // 선택을 $('div')로 했기 때문에
	            // 속성과 jQuery 메소드 사용 가능
	            
	            //(3)
	            // 자바스크립트 DOM 선택 방법으로 선택한 경우
	            // jQuery 메소드 사용 불가
	            // 변수 속성은 사용 가능
	            // var box1 = document.getElementById('box1');	           
	            // box1.css('color', 'red');
	            // 오류 : box1.css is not a function
	            
	            var divs = document.getElementsByTagName('div');	
	            alert(divs.length); // DOM 선택 방식으로 선택해도 속성은 사용 가능
	           // divs.css('color', 'red'); // 오류 : css is not a function
			});
    </script>
~~~

## jQuery 변수
- 변수명 앞에 $ 붙임
- object로 jQuery 메소드 사용 가능
- 일반적으로 태그를 선택한 경우에는 객체로 $를 붙여서 사용
- 값을 가져온 경우 $를 붙이지 않고 사용
- 형식
  - var $div = $(‘div’);
  - var $divLen = $(‘div’).length; 
    - 값을 저장한 경우 타입이 number 인 경우 
    - var divLen = $(‘div’).length; 

##### jQuery 변수 예제 - jQueryVariable.html

~~~html
        <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
                var $box1 = $('#box1');
                $box1.css('color','red');
                $box1.text(typeof $box1); // innerHTML과 동일 : box1의 텍스트 설정하기 typeof : typeof다음에 오는 변수의 타입 체크해서 텍스트 설정해줌

                var $box2 = $('#box2');
                // alert($box2.text()); // box2의 텍스트 읽어오기

                // var $divLen = $('div').length;
                // $box2.text(typeof $divLen);

                var divLen = $('div').length;
                $box2.text(typeof divLen);
           });
        </script>
~~~

##### jQuery 변수 예제 - findElement.html

~~~html
		<script src="jquery-3.6.0.min.js"></script>
		<script type="text/javascript"> 
			$(document).ready(function(){ 
				var $menuItem = $('.menuItem'); // 총 4개
				// alert($menuItem.length) 길이 확인
				// index 값 출력할 <span> 태그 선택
				var $indexSpan = $('#indexSpan');
				// 4개 div에 대해서
				// 각 div 객체에 대해 메소드 수행 : each() 메소드 사용
				// each() 메소드에는 기본적으로 index 의미의 매개변수 포함
				$menuItem.each(function(index) {
					$(this).hover(
					function() { // 마우스 올렸을 때 호출되는 함수
						$(this).css('background', 'yellow');
						$indexSpan.text(index)
					}, 
					function() {// 마우스 땠을 때 호출되는 함수
						$(this).css('background', 'green');
						$indexSpan.text("")
					}); // hover 종료
				}); // each() 종료
			}); //ready() 종료
		</script>  
~~~

## jQuery 이벤트
- 기존 자바스크립트에서 사용했던 이벤트 대부분 사용
- 자바스크립트 보다 간단하고 쉽게 이벤트 처리 가능
- 이벤트 유형
  - 윈도우 이벤트
    - ready(document) : 문서 객체 요소(DOM 요소)가 로드 되었을 때 발생 문서 객체 요소가 자바스크립트에서 사용 가능한 상태인지 확인하고 작동이 가능한 안전 상태일 때 발생
      - $(document).ready()
        - document의 DOM 객체가 로드 되고, 브라우저가 DOM 트리를 생성한 직후 외부 리소스, 이미지 등의 로드 여부 상관 없이 실행
    - resize : 윈도우 창 크기 변경 시 발생
    - scroll : 윈도우 창 스크롤 이동 시 발생
    - load : 문서 객체 요소가 모두 로드 되었을 때 발생. ready와 차이점은 리소드, 이미지 또는 음악 등 로드가 완료된 경우
      - $(window).load()
        - HTML 문서 뿐 아니라 모든 외부 리소스(css, js), 이미지 등이 웹 브라우저 메모리에 모두 올려지면(로드되면) 실행
    - unload : 문서 객체를 닫을 때 발생
    - 이벤트 발생 순서
      - $(document).ready()가 먼저, $(window).load()가 뒤에 발생
      - 이벤트 시점에 따라 오작동 발생 가능성 있기 때문에 같이 사용하지 않고 분리해서 사용
  - 입력 양식 이벤트
  - 마우스 이벤트
  - 키보드 이벤트
- 이벤트 사용 기본 구조
  - 1. 이벤트 대상 : $('#btn')
  - 2. 이벤트 등록 메소드(이벤트 유형) : click() / click
  - 3. 이벤트 핸들러(이벤트 처리 함수) : function() { .... }
- 이벤트 등록 메소드 유형 (이벤트 적용 방법)
  - 단독 이벤트 등록 메소드
    - $('#btn').click(function() { ... });
    - 한 동작에 대해 이벤트를 등록할 때 사용하는 메소
    - 선택자에 직접 이벤트 메소드를 적용
    - $('선택자').이벤트유형(실행함수)
    - 동적 연결 지원 안 됨.
  - 그룹 이벤트 등록 메소드(여러 이벤트)
    - $('#btn').on('click mouseove focus', function() { ... });
    - 한 번에 여러 개의 이벤트를 등록할 수 있다
    - 선택자에 .on() 메소드 사용하여 이벤트 종류 바인딩 시키는 방법
    - 동적으로 생성된 요소에 적용 가능
- 이벤트 연결 방식
  - 정적 연결
    - 현재 HTML 화면에 있는 태그에만 이벤트 연결
    - jQuery를 통해 새로 삽입되는 태그에는 이벤트 연결 안 됨
  - 동적 연결
    - 현재 HTML 화면에 표시된 요소와 앞으로 생성될 요소에 전부 이벤트 연결 가능
    - 예 
      - 동적으로 \<button id="newBtn">으로 생성했을 때
      - $document.on(‘click’, ‘#newBtn’, function(){ ..... });

##### 윈도우 이벤트 예제 resize() 이벤트(단독 이벤트 등록) - windowResize.html

~~~html
        <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
                // 윈도우 크기가 변경될 때 resize 이벤트 발생 / 처리
                $(window).resize(function() {
                    // 윈도우 크기 알아와서 크기에 따라 배경색 변경(변수에 색상 값 저장)
                    var windWidth = $(window).width();
                    var winHeight = $(window).height();
                    //<h3> 태그에 크기 출력
                        $('h3').text("윈도우 크기 : " + windWidth + ' * ' + winHeight)
                    // 크기에 따라 배경 색 변경 : 변수에 색상 값 지정
                    var bgColor;
                    if(windWidth >= 900)
                    bgColor = "green";
                    else if(windWidth >= 700)
                    bgColor = "yellow";
                    else
                    bgColor = "red";

                    // 변수에 저장된 값에 따라 문서 배경색 변경
                    $('body').css('background-color', bgColor);
                }); // resize 끝
           });
        </script>
~~~

##### 이미지 크기를 동적으로 변경하는 예제(그룹 이벤트 등록) - imageResize.html

~~~html
  <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
                // 윈도우 크기 변경될 때 윈도우 크기에 이미지 맞추기
                $(window).on('resize', function() {
                    // 가로 길이 알아와서 변수에 저장
                    var winWidth = $(window).width();
                    // 이미지의 가로 * 세로 비율에 맞춰 높이 구하기
                    var imgHeight = winWidth * 600 / 1920;
                    // 이미지 가로, 세로 길이 설정
                    $('#topImg').css({'width':winWidth, 'height':imgHeight});
                });
           });
        </script>
</head>
<body>
    <div id="topImgBox"><img src="image/topImg.jpg" id="topImg"></div>
</body>
~~~

### 마우스 이벤트
- 이벤트
  - click : 마우스를 클릭했을 때 발생
  - dbclick : 마우스를 더블클릭 했을 때 발생
  - mousedown : 마우스 버튼을 누를 때 발생
  - mouseup : 마우스 버튼을 뗄 때 발생
  - mouseenter : 마우스가 요소의 경계 외부에서 내부로 이동할 때 발생
  - mouseleave : 마우스가 요소의 경계 내부에서 외부로 이동할 때 발생
  - mousemove : 마우스를 움직일 때 발생
  - mouseout : 마우스가 요소를 벗어날 때 발생
  - mouseover : 마우스가 요소 안에 들어올 때 발생
  - hover : 마우스를 over 했을 때, out 했을 때 발생
  - contextmenu : 마우스 오른쪽 버튼을 클릭했을 때 발생

##### 마우스 이벤트 - mouseEvent.html

~~~html
        <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
                $('#btn').on('click', function() {
                    alert("클릭했습니다.");
                });
                // 방법 1 : .on(event1).on(event2)
                // 2개의 이벤트 처리
                $('#btn')
                .on('mouseover', function() {
                    $(this).css('background-color', 'yellow');
                })
                .on('mouseout', function() {
                    $(this).css('background-color', '');
                 }); // on 종료
                // 방법 2 : .on({event1, event2})
                $('#btn').on({
                    mouseover:function() {
                        $(this).css('background-color', 'pink');
                    },
                    mouseout:function() {
                        $(this).css('background-color', 'skyblue');
                    }});
           });
        </script>
~~~

### 동적 연결 이벤트
- 현재 HTML 화면에 표시된 요소와 앞으로 생성될 요소에 전부 이벤트 연결 가능
- 예 
  - 동적으로 \<button id="newBtn">으로 생성했을 때
  - $document.on(‘click’, ‘#newBtn’, function(){ ..... });

##### 동적 연결 이벤트 예시 - dynamicEvent.html

~~~html
        <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
                // createBtn 눌렀을 때 새 버튼 두 개 생성
                $('#createBtn').on('click', function() {
                    $(this).after("<p><button id='newBtn1'>새 버튼 1</button>" + "<p><button id='newBtn2'>새 버튼 2</button>" )
                });
                // 정적 이벤트 연결 방식으로 이벤트 처리
                // 새로 생성된 요소에 이벤트 등록 되지 않음
                $('#newBtn1').on('click', function() {
                    alert("[새 버튼 1]을 클릭 했음")
                });
                // 동적 이벤트 연결 방식으로 이벤트 처리
                // 클릭 이벤트 등록 처리되어서 알림창 출력
                $(document).on('click', '#newBtn2', function() {
                    alert("[새 버튼 2]를 클릭 했음")
                });
           });
        </script>
</head>
<body>
    <button id="createBtn">새 버튼 만들기</button>
</body>
~~~

##### 이벤트 연습 문제 - dynamicEventEx1.html

~~~html
    <style>
        #Btn {
            border: rgb(73, 122, 124) solid;
            border-radius: 20px;
            font-size: 20px;
            color: white;
            width: 80px;
            height: 50px;
            background-color: rgb(73, 122, 124);
        }
    </style>
        <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
                $('#Btn').on({
                    mouseover:function() {
                        $(this).css('opacity', '0.5');
                    },
                    mouseout:function() {
                        $(this).css('opacity', '1.0');
                    }});
           });
        </script>
</head>
<body>
    <button id="Btn">버튼</button>
</body>
~~~

##### 이벤트 연습 문제 - dynamicEventEx2.html

~~~html
    <style>
        #Btn {
            width: 80px;
            height: 50px;
            border-radius: 15px;
            background-color: red;
            border: solid;
        }
    </style>
        <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
               let i = 0;
               let arr = ['green', 'blue', 'red']
                $('#Btn').on('click', function() {
                        $(this).css('background-color', arr[i]);
                        i++
                        if(i == 3) {
                            i = 0;
                        }
                });
           });
        </script>
~~~

### 키보드 이벤트
- 키보드 이벤트 종류
  - keyup : 키보드가 떼어질 때 발생
  - keydown  : 키보드가 눌러질 때 발생
  - keypress : 글자가 입력될 때 발생

##### 키보드 이벤트 예제 - newMember.html, formCheck.js

~~~html
<style>			
			#id, #pwd { width: 100px;}
			table { margin:0 auto; width:600px; }
		</style>
		<script src="jquery-3.6.0.min.js"></script>	
		<script src="formCheck.js"></script>
	</head>
	<body>
		<div id="wrap">
	        <h3 align="center">회원 가입</h3>
	        <hr>
	        <form id="newMemberForm" name="newMemberForm" method="post" action="newMemberOk.jsp">
	          <table>
	            <tr><td> ID</td><td><input type="text" id="id" name="id"></td></tr>
	            <tr><td>비밀번호</td><td><input type="password" id="pwd" name="pwd"></td></tr>
	            <tr><td>휴대폰 번호</td><td><input type="text" id="hp1" size="3"> 
	                    - <input type="text" id="hp2" size="4">
	                    - <input type="text" id="hp3" size="4"></td></tr>   
	            <tr><td>학년</td><td><input type="radio" id="year1" name="year" value="1" >1학년
	                                     <input type="radio" id="year2" name="year" value="2">2학년
	                                     <input type="radio" id="year3" name="year" value="3">3학년
	                                     <input type="radio" id="year4" name="year" value="4">4학년</td></tr>
	            <tr><td>관심분야</td>
	                  <td><input type="checkbox"  id="web" name="web" value="웹">웹 프로그래밍
	                         <input type="checkbox"  id="design" name="python" value="웹디자인">파이썬
	                         <input type="checkbox"  id="bigdata" name="bigdata" value="빅데이터">빅데이터
	                         <input type="checkbox"  id="java" name="java" value="자바">자바 프로그래밍</td></tr>
	            <tr><td>학과</td>
	                  <td><select id="department" name="department">
	                               <option value="">선택하세요</option>
								   <option value="경영학과">경영학과</option>
								   <option value="산업공학과">산업공학과</option>
								   <option value="경제학과">경제학과</option>
								   <option value="전자공학과">전자공학과</option>
								   <option value="컴퓨터학과">컴퓨터학과</option>
	                          </select></td></tr>
	             <tr>
	                <td colspan="2" align="center">
	                    <br><input type="submit" value="완료">
	                    <input type="reset" value="취소">
	                </td>
	            </tr>             
	          </table>
      		</form>	
      	 </div>            
    </body>
~~~

~~~js
$(document).ready(function() {
    // 시작시 ID 입력란에 포커스 추가
    let $id = $('#id');
    //$id.focus();
    let $pwd = $('#pwd');
    let $year = $(':radio[name="year"]'); // 여러 개 있는 경우
    // 한 개만 있는 경우 var $year = $(':radio'); 
    let $check = $(':checkbox[type=checkbox]');
    let $department = $('#department');
    // 완료버튼 클릭하면 입력 유효성 확인
    // input 텍스트 입력란에(id, pw) focus 있을 때 색상 변경
    $($id).on({
        focus:function() {
            $(this).css('background-color', 'pink');
        },
        blur:function() {
            $(this).css('background-color', 'white');
        }});
    $($pwd).on({
        focus:function() {
            $(this).css('background-color', 'yellow');
        },
        blur:function() {
            $(this).css('background-color', 'white');
        }});

        $('#hp1').on('keyup', function() {
            if($('#hp1').val().length > 2) {
                $('#hp2').focus();
            }
        });
        $('#hp2').on('keyup', function() {
            if($(this).val().length > 3) {
                $('#hp3').focus();
            }
        });
        // 엔터키 입력하면 sumbit 시키지 않게
        // function(e)의 e는 이벤트 발생 시 처리 함수로 전달되는 event 객체
        // 함수의 매개변수로 받아서 사용
        // 필요 없을 때는 function() 안 받으면 됨.
        // 이름은 임의로 사용 가능 : event로 해도 되고 a, b, c 등 자유
        // 일반적으로 이벤트를 의미하는 event, e 사용
        $(document).on('keydown', function(e){
            if(e.keyCode == 13) 
            return false;
        });
        // id에서 엔터키 입력하면 다음 pw칸으로 포커스
        $($id).on('keydown', function(e) {
            // id 값이 비어도 넘어감
            // if(e.keyCode == 13) 
            // $pwd.focus();
            // id 값이 입력되어야 엔터키 눌러도 넘어감
            if(e.keyCode == 13 && $id.val() != "") 
            $pwd.focus();
        });
        

    // ID를 입력하지 않은 경우 "아이디를 입력하세요"경고창 출력
    // ID 입력란에 포커스
    // 다음 페이지로 전송되지 않도록 처리
    // 비밀번호 입력하지 않은 경우 "비밀번호를 입력하세요" 출력
    // 비밀번호 입력란에 포커스
    // 다음 페이지로 전송되지 않도록 처리
    $('#newMemberForm').submit(function() {
        if($id.val() == "") {
            alert("아이디를 입력하세요.");
            $id.focus();
            return false;
        }
        if($pwd.val() == "" && $id.val() != "") {
            alert("비밀번호를 입력하세요.");
            $pwd.focus();
            return false;
        }
        if($year.is(':checked') == false) {
            alert("학년을 선택하세요.");
            return false;
        }
        if($check.is(':checked') == false) {
            alert("관심분야를 선택하세요.");
            return false;
        }
        if($department.val() == "") {
            alert("학과를 선택해 주세요.");
            $department.focus();
            return false;
        }
    }); // submit 끝.
}); //ready 종료
~~~

### 입력 양식 이벤트 
- 종류
  - submit : submit(전송) 버튼 눌렀을 때 발생
  - reset : reset(취소) 버튼 눌렀을 때 발생
  - change : 입력 양식의 내용을 변경할 때 발생(select 입력 시)
  - focus : 입력 양식에 커서를 놓을 때 발생
  - blur : 입력 양식이 커서를 잃을 때 발생
- 입력 양식 관련 메소드
  - value : val()
    - $(‘선택자’).val()
  - focus : focus()
  - 체크 되었는지 : is(':checked')

##### \<select> 태그에서 change 이벤트 예제 - selectChange.html

~~~html
        <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
                $('#department').on('change', function() {
                    $('span').text($(this).val());
                });
           });
        </script>
</head>
<body>
    <select id="department" name="department">
        <option value="">선택하세요</option>
        <option value="경영학과">경영학과</option>
        <option value="산업공학과">산업공학과</option>
        <option value="경제학과">경제학과</option>
        <option value="전자공학과">전자공학과</option>
        <option value="컴퓨터학과">컴퓨터학과</option>
   </select> &nbsp;&nbsp;
   <span>학과</span>
</body>
~~~

##### \<select> 태그에서 change 이벤트 연습문제 - selectChangeEvent.html

~~~html
<script src="jquery-3.6.0.min.js"></script>
		<script type="text/javascript">
			$(document).ready(function() {	
                // 변수
				var price = 4500000;
				var chkAmount=0, optAmount=0;
				var $checkBox = $(':checkbox'); // 체크박스 배열
				
				// 주문액 계산 함수 
				function showAmount(){
					var amount = price + optAmount + chkAmount;
					$('#amount').text(amount.toLocaleString() + " 원"); 	// toLocaleString() :  천 단위 구분				
				}				
				
				// 이벤트 처리1 : <select> 태그의 change 이벤트 처리
				// 옵션 금액 설정
				$('#basicOption').on('change', function(){
					optAmount = parseInt($(this).val());
					showAmount();
				});
				
				
				// 이벤트 처리2 : 체크박스 태그의 click 이벤트 처리
				// 체크박스 3개이므로 각각 금액을 설정하기 위해서 
				// 총 체크박스 선택 금액 설정 
				$checkBox.on('click', function(){
					chkAmount = 0;
					
					$checkBox.each(function(){
						if($(this ).is(':checked'))
							chkAmount += parseInt($(this).val());
				    });					
					showAmount();
			    });
	 	    });
		</script> 
    </head>
    <body>
        	<h1>카메라 주문서</h1>        
            <table border="1">
                <tr><td colspan="3"><img src="image/camera.jpg"></td></tr>
                <tr><td class="bg">기본 가격</td><td  colspan="2">4,500,000 원</td></tr>   
                <tr><td class="bg">기본 옵션 </td>
                     <td  colspan="2"><select id="basicOption" >
                                   <option value="0">선택하세요</option>
                                   <option value="100000">삼각대 100,000원</option>
                                   <option value="50000">차량용 충전기 50,000원</option>
                              </select></td></tr>
                <tr><th>선택 옵션</th><th>가격</th><th>선택</th></tr>   
                <tr><td>렌즈 필터</td><td>30,000 원</td><td><input type="checkbox"  id="lenzFilter" value="30000"></td></tr>        
                <tr><td>DSLR 가방</td><td>40,000 원</td><td><input type="checkbox"  id="dslrBag" value="40000"></td></tr>   
                <tr><td>청소도구</td><td>7,000 원</td><td><input type="checkbox"  id="cleaningTools" value="7000"></td></tr> 
                <tr><td class="bg">주문액</td><td id="amount" colspan="2" value="4500000">4,500,000 원</td></tr>           
            </table>          
    </body>
~~~