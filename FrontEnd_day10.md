## each() 메소드
- $(선택자).each(콜백함수function(){});
- $.each(배열, 콜백함수);
- $.each(객체, 콜백함수);

##### each() 메소드 예제 - eachFunction.html

~~~html
        <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
                $('div').each(function() {
                    console.log($(this).text()); // 텍스트 읽어오기 a, b, c 출력
                });
                $('div').each(function(index) {
                    console.log($(this).text(index)); // 텍스트로 출력하기     S.fn.init [div]
                                                                            // 0: div
                                                                            // length: 1
                });
                //$.each(배열, 콜백함수)
                var names = ["홍길동", "이몽룡", "성춘향", "변학도"];
                $.each(names, function(index, value){
                    console.log(index + " : " + value);
                });
                // 0 : 홍길동
                // 1 : 이몽룡
                // 2 : 성춘향
                // 3 : 변학도
                // 인덱스 번호 : 이름

                //$.each(객체, 콜백함수)
                // 사용자 정의 객체 생성
                let car = {
                no : "11가 1111", // 프로퍼티(속성) : 값
                name : "소나타",
                maker : "현대",
                cc : 2000,
                year : 2021
            };
            $.each(car, function(prop, value) {
                console.log(prop + " : " + value);
            });
            // no : 11가 1111
            // name : 소나타
            // maker : 현대
            // cc : 2000
            // year : 2021
            // 프로퍼티(속성) : 값
           });
        </script>
</head>
<body>
    <div>a</div>
    <div>b</div>
    <div>c</div>
</body>
~~~

## 이벤트 객체 메소드
- preventDefault() : 현재 이벤트의 기본 동작 중지
- stopPropagation() : 상위 요소로 이벤트가 전파되는 것 중지
  - 이벤트 전파
    - 자식 요소에서 발생한 이벤트가 부모 요소에게까지 전파되는 것
    - 이벤트 버블링이라는 표현으로 사용하기도 함.
    - \<div id="parent">\<div id="child">자식\</div>\</div>
    - 자식 \<div>를 클릭했는데, 부모 \<div>클릭 이벤트 발생
- stopImmediatePropagation() : 현재 이벤트의 다른 리스너 중지 및 상위로 전파되는 것 중지
  - 하나의 버튼에 3개의 이벤트 핸들러가 있다면 이벤트 3개가 수행됨.
- return false
  - jQuery에서는 preventDefault() + stopPropagation() 
  - JavaScript에서는 preventDefault()
- \<a> 태그 클릭 시 href 속성에 지정된 url로 이동
- document에서 오른쪽 마우스 클릭 시 contextmenu(팝업메뉴) 출력

##### preventDefault() 예제 - preventDefault.html

~~~html
        <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
            // a 태그의 기본 동작(url로 이동) 중지.
           $(document).ready(function() {
                $('#link').on('click', function(e) {
                    e.preventDefault();
                    alert("일시적 이동 중지");
                });
                // 문서 상에서 오른쪽 마우스 클릭했을 때 이벤트 처리
                document.oncontextmenu = function(e) {
                    e.preventDefault();
                    alert("오른쪽 마우스 클릭 금지");
                    // return false; // 해도 무방.
                }
           });
        </script>
</head>
<body>
    <!-- a 태그는 클릭하면 href 속성에 지정된 url로 이동하는 기본 동작 수행 -->
    <a href="https://www.naver.com" id="link">네이버로 이동</a>
</body>
~~~

##### stopPropagation() 예제 - stopPropagation.html

~~~html
    <style>
        #parent {
            border: solid 1px blue;
        }
        #child {
            border: solid 1px red;
            width: 20%;
        }
    </style>
        <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
                $('#parent').on('click', function() {
                    alert("parent")
                    // parent만 발생
                });
                $('#child').on('click', function(e) {
                    // 상위 요소로 이벤트가 전파되는 것 중지
                    e.stopPropagation();
                    alert("child")
                    // child, parent 발생
                });
           });
        </script>
</head>
<body>
    <div id="parent">
        <div id="child">클릭</div>
    </div>
~~~

##### stopImmediatePropagation() 예제 - stopImmediatePropagation.html

~~~html
        <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
               // 현재 세 개의 이벤트 리스너가 수행
               // 클릭1, 클릭 2만 수행되게 하고 다른 리스너는 중지 및 상위 전파 중지
                $('#btn').on('click', function() {
                    alert("클릭1");
                })
                $('#btn').on('click', function(e) {
                    e.stopImmediatePropagation();
                    alert("클릭2");
                })
                $('#btn').on('click', function() {
                    alert("클릭3");
                })
           });
        </script>
</head>
<body>
    <button id="btn">클릭</button>
</body>
~~~

## jQuery DOM 요소 조작
- 동적으로 쉽고 간단하게 DOM 요소 조작 가능
- DOM 요소 삽입 / 삭제 / 속성 추가 및 삭제 / 클래스 속성
- DOM 요소 조작 관련 메소드
  - text() : 글자와 관련된 내용을 반환하거나 설정
  - html() : HTML과 관련된 내용을 반환하거나 설정
  - $(선택자).append(A) : 선택자의 내부 요소들 맨 뒤에 A를 삽입
  - $(선택자).prepend(A) : 선택자의 내부 요소들 맨 앞에 A를 삽입
  - $(A).apeentTo(선택자) : A를 선택자의 내부 요소들 맨 뒤에 삽입
  - $(A).prependTo(선택자) : A를 선택자의 내부 요소들 맨 앞에 삽입
  - $(선택자).after(A) : 선택자 뒤에 A 삽입
  - $(선택자).before(A) : 선택자 앞에 A 삽입
  - $(A).insertAfter(선택자) : A를 선택자의 뒤에 삽입
  - $(A).insertBefore(선택자) :  A를 선택자의 앞에 삽입
  - $(선택자).remove() : 해당되는 요소 제거
  - $(선택자).empty() : 해당되는 요소의 모든 자식 노드 제거

### text()와 html() 메소드
- 자바스크립트의 innerHTML 속성과 유사
- 찾은 DOM 요소의 글자(텍스트)를 설정하거나 반환
- html() : HTML 태그 인식 (태그 효과 적용)
- text() : HTML 태그 인식하지 못하고 글자로 인식 (\<h1> 그대로 출력)

##### text()와 html() 예제 - DOMtextHtml.html

~~~html
        <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
               // 1. text() : 문자열만 반환(태그 제외)
                var aText = $('#a').text(); // 괄호안에 인자 없으면 get()의 의미 
                // 변수 aText는 텍스트 값을 저장한 변수 : 객체의 역할로 메소드 사용 불가
                alert("text : " + aText); // text : A

                // 2. html() : 태그 포함된 문자열 반환
                var bHtml = $('#b').html();// 괄호안에 인자 없으면 get()의 의미
                alert("html : " + bHtml); // html : <h3>B</h3>

                // 3. text(문자열) : <h1>jQuery</h1> 출력 <h1>을 태그로 인식하지 못하고 문자열로 취급하여 출력됨
                // aText.text('<h1>jQuery</h1>'); @@ 변수 aText는 텍스트 값을 저장한 변수 : 객체의 역할로 메소드 사용 불가
                $('#a').text('<h1>jQuery</h1>'); //괄호 안에 같이 있으면 set()의 의미
                // 3. html(문자열) : jQuery 출력 <h1>을 태그로 인식하여 제목이 됨.
                $('#b').html('<h1>jQuery</h1>');
           });
        </script>
</head>
<body>
    <div id="a"><h3>A</h3></div>
    <div id="b"><h3>B</h3></div>
</body>
~~~

##### append()/prepend() 예제 - DOMappend.html

~~~html
        <style type="text/css">		 	
			#box { width:500px; height: 200px; line-height:200px; 
			                  border:1px solid #000; }
			img {vertical-align:middle;}					
		</style>	
		<script src="jquery-3.6.0.min.js"></script>
		<script type="text/javascript">
			$(document).ready(function() {		  
			   var img = "<img src=\"image/banana.png\">";
               // prepend 버튼 클릭했을 때
               // 선택자 box 내부 요소들 맨 앞에 img 삽입.
               // <img src="image/banana.png"> div 내부 <img src='image/apple.png'>
               $('#prepend').on('click', function() {
                   $('#box').prepend(img);
               });
               // append 버튼 클릭했을 때
               // 선택자 box 내부 요소들 맨 뒤에 img 삽입.
               // div 내부 <img src='image/apple.png'> <img src="image/banana.png"> 
               $('#append').on('click', function() {
                   $('#box').append(img);
               });
               // before 버튼 클릭했을 때
               // 선택자 box 요소 앞에 img 삽입.(<div> 영역 외부에 추가)
               // <img src="image/banana.png"> 
               // <div id="box">
               //     div 내부 <img src='image/apple.png'>
               // </div>  
               $('#before').on('click', function() {
                   $('#box').before(img);
               });
               // after 버튼 클릭했을 때
               // 선택자 box 요소 뒤에 img 삽입.(<div> 영역 외부에 추가)
               // <div id="box">
               //     div 내부 <img src='image/apple.png'>
               // </div>  
               // <img src="image/banana.png"> 
               $('#after').on('click', function() {
                   $('#box').after(img);
               });
                // empty 버튼 클릭했을 때
                // <div id="box"> 태그 안에 들어있는 모든 요소 제거
               $('#empty').on('click', function() {
                   $('#box').empty();
               });
                // remove 버튼 클릭했을 때
                // 박스 앞 / 뒤, 전 / 후 상관 없이 모든 img 태그 자체가 사라짐.
                $('#remove').on('click', function() {
                    $('img').remove();
                // $('#box').remove(); // <div id="box"> 포함해서 box 안에 있는 모든 것들이 사라짐.
               });
               $('#initiate').on('click', function() {
                // img 태그 제거
                $('img').remove();
                // div내부 요소 비우고 추가
                $('#box').empty().append("div 내부 <img src='image/apple.png'>");
               });
			});
		</script>
	</head>

    <body>
        <button id="prepend" >prepend</button> 
        <button id="append" >append</button> 
        <button id="before" >before</button> 
        <button id="after" >after</button> 
        <button id="empty" >empty</button> 
        <button id="remove" >remove</button> 
        <button id=initiate >초기화</button>
        <p>
        <div id="box">
        	div 내부 <img src='image/apple.png'>
        </div>    
    </body>
~~~

## DOM 요소의 추가 및 삭제
- attr('속성명', 값) : 속성 추가
- removeAttr('속성명') : 속성 제거

##### DOM 요소의 추가 및 삭제 예제 - DOMattr.html

~~~html
        <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
                $('#img')
                .on('mouseover', function() {
                    $(this).attr('src', 'image/apple.png');
                })
                .on('mouseout', function() {
                    $(this).attr('src', 'image/heart.png');
                });
           });
        </script>
</head>
<body>
    <h1>DOM 요소 속성 추가</h1>
    <img src="image/heart.png" id="img">
</body>
~~~

##### DOM 요소의 추가 및 삭제 연습문제 - DOMattrIndex.html

~~~html
        <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           //(1) <img> 태그를 선택해서 (객체 변수 생성 생략하고 바로 선택자를 객체로 사용)
				// var $img = $('img'); 해서 배열 객체 생성해도 되고
				// 바로 선택자로 each() 메소드 앞에 적어도 됨 : $('img').each()
				//<img> 4개 : 배열로 객체 생성
				
				//(2) 각 이미지에 마우스 올렸다 뗐을 때 처리 : 각각을 처리해야 하므로 each() 사용
				// each()에는 기본 파라미터 index 가 포함되어 있음
				// 마우스 올렸다 뗐을 때 처리하는 메소드로 hover() 사용
				$('img').each(function(index){
					$(this).hover(
						function() {	// 첫 번재 함수 : 마우스 올렸을 때 처리
							// 이미지 변경 : <img> 태그의 src 속성값을 변경 : attr() 메소드 사용
							$(this).attr('src', "image/img2-" + (index+1) + ".jpg");
						}, 
						function(){  // 두 번째 함수 : 마우스 뗐을 때 처리
							$(this).attr('src', "image/img1-" + (index+1) + ".jpg");
						}
					);					
				});				
        </script>
</head>
<body>
    <img src="image/img1-1.jpg" id="img1">
    <img src="image/img1-2.jpg" id="img2">
    <img src="image/img1-3.jpg" id="img3">
    <img src="image/img1-4.jpg" id="img4">
</body>
~~~

## DOM 요소의 클래스 속성
- CSS 효과 동적 적용
  - CSS의 클래스 선택자에게 적용된 여러 효과를 동적으로 추가하거나 제거
    - addClass('클래스명') : CSS 효과 적용
    - removeClass('클래스명') : 적용된 CSS 효과 제거(해제)
    - toggleClass('클래스명') : addClass()와 removeClass() 번갈아 실행하는 결과

##### DOM 요소의 클래스 속성 예제 - DOMaddClass.html

~~~html
<style type="text/css">        	
        * { text-align:center; }
        .h1Css {
            background-color:gold;
            color:blue;
        }
        .imgCss { 
            opacity:0.5; 
            box-shadow: 5px 5px 10px 1px #777777;
            /* x-position y-position blur color */
        }
        .hidden{ visibility:hidden; }
    </style>
    <script src="jquery-3.6.0.min.js"></script>
    <script type="text/javascript">
        $(document).ready(function() {	
            $('img')
                .on('mouseover', function(){
                    $(this).addClass('imgCss');
                    $('h1').text("여러 CSS 효과 동적으로 적용");
                    $('h1').addClass('h1Css');
                })
                .on('mouseout', function(){
                    $(this).removeClass('imgCss');
                    $('h1').text("이미지에 마우스를 올려보세요.");
                    $('h1').removeClass('h1Css');
                });
            
            // [toggleClass] 버튼 클릭 시 addClass()와 removeClass() 번갈아 적용
            $('#toggle').on('click', function(){
                $('img').toggleClass('hidden'); //hidden 클래스 효과
            });
         });
    </script>
</head>
<body>
    <div id="wrap">
        <h1>이미지에 마우스를 올려보세요.</h1>          
        <img src="image/painting.jpg"><br><br>
        <button id="toggle">toggleClass</button>
    </div>
</body>
~~~

## jQuery 효과
- 공통 인수
  - duration : 효과 진행 속도(slow / normal / fast)
  - callback : 효과 완료 후 수행할 함수
  - easing : 전체 애니메이션(효과)의 적용 시간 비율을 원하는 진행 비율로 매핑
    - swing : sin곡선(느리게 시작해서 중간에 빠르게 진행되다가 나중에 다시 느려지는 효과)
    - linear : 선형 곡선(시작부터 끝까지 일정한 속도)
- jQuery로 가능한 시각적 효과
  - Basic 효과
    - hide() : 요소 숨기기
    - show() : 요소 표시(출력)
    - toggle() : 요소를 숨기거나 표시 (hide() / show() 교대로 실행)
  - Sliding 효과
    - slideDown() : 요소를 슬라이딩 효과로 나타나게 함
    - slideUp() : 요소를 슬라이딩 효과로 숨김
    - slideToggle() : 숨겼다 보였다 교대로 실행(slideDown() / slideUp() 교대로 실행)
  - Fading 효과
    - fadeIn() : 요소를 선명하게 만들면서 나타남
    - fadeOut() : 요소를 흐리게 하면서 숨김(영역도 사라짐)
    - fadeToggle() : fadeIn() / fadeOut() 교대로 실행
    - fadeTo() : 요소의 불투명도 조정, 투명도 0으로 안 보여도 영역은 그대로 남아 있음.
  - Animate 효과
    - animate(속성)
    - 형식
      - 1. $(대상).animate( {속성(CSS)}, duration(효과 진행 속도), 'easing'(진행 효과) );
      - 2. $(대상).animate( {속성(CSS)}, duration(효과 진행 속도), 'easing'(진행 효과), function() { 효과 완료 후 수행할 내용 } );
    - 애니메이션 정지
      - $(선택자).stop(); // false로 입력한 것으로 간주
      - $(선택자).stop(true); // clearQueue
      - $(선택자).stop(true, true); // clearQueue, goToEnd
        - clearQueue : 대기열에 있는 함수 모두 제거, 예약된 애니메이션 초기화(clearQueue() 메소드 실행 효과)
        - goToEnd : 제자리에서 멈추는 것이 아니라 지정한 최종 상태에서 멈춤

##### Basic효과 예제 - basicEffect.html

~~~html
    <style type="text/css">
        #wrap { margin:0 auto;  width:800px; text-align:center; }
        .menuItem { display:inline-block; margin:20px; }		
        hr { margin-bottom:20px; }		
    </style>
    <script src="jquery-3.6.0.min.js"></script>
    <script type="text/javascript">
        $(document).ready(function() {				
            $('#show').on('click', function() {
                $('img').show('slow');
            })
            $('#hide').on('click', () => {
                $('img').hide('fast');
            })
            // toggle1 버튼 : 속도 0.5초
            $('#toggle1').on('click', () => {
                $('img').toggle(500);
            })
            // toggle2 버튼 : 속도 3초 swing
            $('#toggle2').on('click', () => {
                $('img').toggle(3000, 'swing');
            })
            // toggle3 버튼 : 속도 3초 linear
            $('#toggle3').on('click', () => {
                $('img').toggle(3000, 'linear');
            })
         });
    </script>
</head>
<body>
    <div id="wrap">
         <h1>Basic 효과 </h1>
         <div id="menu">
             <div class="menuItem"><a href="#" id="show">show</a></div>
             <div class="menuItem"><a href="#" id="hide">hide</a></div>
             <div class="menuItem"><a href="#" id="toggle1">toggle1 0.5초</a></div>
             <div class="menuItem"><a href="#" id="toggle2">toggle2 3초 'swing'</a></div>
             <div class="menuItem"><a href="#" id="toggle3">toggle3 3초 'linear'</a></div>	
         </div>
         <hr>
         <img src="image/pink.png">         
    </div>
</body>
~~~

##### Sliding효과 예제 - slideEffect.html

~~~html
<style type="text/css">	
			*{ text-align:center;}		
			#menuBox {width:100px; margin:0 auto; margin-bottom:30px;}	
			#menuBox:hover { 
					background-color:orange;
					color:blue;
					font-weight:bold;
				}				
			#subMenuBox {display:none; } 
		</style>
		<script src="jquery-3.6.0.min.js"></script>
		<script type="text/javascript">
			$(document).ready(function() {
				 $('#menuBox').hover(
					 // 메뉴에 마우스 올리면 subMenuBox가 slideDown 되면서 영역이 나타나고 이미지 보임
					 function() {
						 $('#subMenuBox').slideDown(1000);
					 },
					 // 메뉴에 마우스 떼면 subMenuBox가 slideUp 되면서 영역이 사라지고 이미지 안 보임
					 function() {
						$('#subMenuBox').slideUp(1000);
					 }
				 );
			});
		</script>
	</head>
	<body>
    	<div>
            <div><h3>Sliding 효과</h3></div>
            <div id="menuBox">메뉴</div>         
            <div id="subMenuBox">
                <img src="image/black.png">
            </div> 
            <button>버튼의 위치는?</button>             
        </div>
	</body>
~~~

##### Fading 예제 - fadeEffect.html, fadeToEffect.html

~~~html
<style type="text/css">
			h2{
				width:300px; 
				height:40px;
				padding:10px;
				background-color:red;
				color:yellow;
				display:none;
				}
			ul { list-style:none; }	  /* type 없음 */	
			li { display:inline-block; margin-right:30px; }				
		</style>	
		<script src="jquery-3.6.0.min.js"></script>
		<script type="text/javascript">
			$(document).ready(function() {
				$('#fadeIn').on('click', function() {
                    $('h2').fadeIn('slow');
                });
                // 영역도 사라진다.
                $('#fadeOut').on('click', function() {
                    $('h2').fadeOut(2000);
                });
                $('#fadeToggle').on('click', function() {
                    $('h2').fadeToggle(3000, 'linear');
                })
	        });
		</script>
     </head>          
    <body>
        <center>
            <h1>Fading 효과 </h1>
            <ul>
                <li><a href="#" id="fadeIn">fadeIn</a></li>
                <li><a href="#" id="fadeOut">fadeOut</a></li>
                <li><a href="#" id="fadeToggle">fadeToggle</a></li>
            </ul>
            <hr>
            <h2>Have a Nice Day!</h2>
            <h3>난 어디에 놓일까?</h3>
        </center>
	</body>
~~~

~~~html
<style type="text/css">
			ul { list-style:none; }	
			li { display:inline-block; margin-right:30px; }				
		</style>   
		<script src="jquery-3.6.0.min.js"></script>
		<script type="text/javascript">
			$(document).ready(function() {
                // 투명도가 0이 되어 보이지 않아도 영역은 남아 있다.
				$('#off').on('mouseover', function() {
                    $('img').fadeTo(1000, 0);
                });
                $('#on').on('mouseover', function() {
                    $('img').fadeTo(1000, 1);
                });
                $('#50').on('mouseover', function() {
                    $('img').fadeTo(1000, 0.5);
                });
			});
		</script>     
	</head>    
	<body>
		<center>
            <h1>fadeTo() 효과 </h1>
            <ul>
                <li><a href="#" id="off">opacity : 0</a></li>
                <li><a href="#" id="on">opacity : 1</a></li>
                <li><a href="#" id="50">opacity : 0.5</a></li>
            </ul>          
            <hr>
            <img src="image/TakashiAkasaka.jpg"> 
            <h3>난 어디에 놓일까?</h3>
        </center>
	</body>
~~~

##### Animate 예제 - animate1.html, animate2.html, animate3.html

~~~html
 <style type="text/css">			
			div {
				width: 50px; 
				height: 50px;
				line-height:50px;
				text-align:center;
				background-color: rgb(0, 176, 240);
				position: relative;
        	   }		
		</style>
		<script src="jquery-3.6.0.min.js"></script>
		<script type="text/javascript">
			$(document).ready(function() {
				$('div').hover(
					function () {
						$(this).animate({left:500}, 1000);
				},
					function() {
						$(this).animate({left:0}, 4000);
				}
				);
	     	});
		</script>
    </head>        
     <body>    
        <div>1</div><div>2</div>
        <div>3</div><div>4</div>
        <div>5</div><div>6</div> 
    </body>
~~~

~~~html
<script src="jquery-3.6.0.min.js"></script>
		<script type="text/javascript">
			$(document).ready(function() {
				$('#startBtn').on('click', function() {
					$('div').each(function(index) {
						$(this).delay(index * 500).animate( {left:500}, 'slow' );
					});
				});
				$('#backBtn').on('click', function() {
					$('div').each(function(index) {
						$(this).delay(index * 500).animate( {left:0}, 'slow' );
					});
				});
     		});
		</script>
    </head>        
     <body> 
     	<button id="startBtn">이동</button>
        <button id="backBtn">원위치</button><p>
        <div></div><div></div>
        <div></div><div></div>
        <div></div><div></div>
    </body><script src="jquery-3.6.0.min.js"></script>
		<script type="text/javascript">
			$(document).ready(function() {
				$('#startBtn').on('click', function() {
					$('div').each(function(index) {
						$(this).delay(index * 500).animate( {left:500}, 'slow' );
					});
				});
				$('#backBtn').on('click', function() {
					$('div').each(function(index) {
						$(this).delay(index * 500).animate( {left:0}, 'slow' );
					});
				});
     		});
		</script>
    </head>        
     <body> 
     	<button id="startBtn">이동</button>
        <button id="backBtn">원위치</button><p>
        <div></div><div></div>
        <div></div><div></div>
        <div></div><div></div>
    </body>
~~~

~~~html
<script type="text/javascript">			
			$(document).ready(function() {
				$('#box1').animate({left: '+=100'}, 1000)
								.animate({width: '+=100'}, 2000)
								.animate({height: '+=100'}, 2000);
			
				// 6초 후에 함수 실행
				setTimeout(function(){
					$("div").clearQueue();
					$("div").hide();					
				}, 6000);
				
				$('#box2').animate({left: '+=100'}, 1000)
								.animate({width: '+=100'}, 2000)
								.animate({height: '+=100'}, 2000,
									function(){
										$(this).css('transform', 'rotate(30deg)');
									}										
								);
			});
		</script>       
    </head>       
    <body>    
        <div id="box1"></div>
        <div id="box2"></div>
    </body>
~~~

## 응용 예제
- 음성 녹음
  - 음성 녹음 ([녹음] / [정지])
  - <audio> 컨트롤 출력 play
  - 파일로 저장
- WebRTC
  - 별도의 플러그인 없이 웹에서 RTC(Real-Time Communications)를 구현하기 위해 HTML5에 새로 추가된 기능
  - https://webrtc.org

##### 음성 녹음 예제 - voiceRecord.html, voiceRecord.js

~~~html
 <script src="jquery-3.6.0.min.js"></script>
        <script src= "voiceRecord.js"></script>
        <script type="text/javascript">
           
        </script>
</head>
<body>
    <button id="record">녹음</button>
    <button id="stop">정지</button>
    <div id="sound-clips"></div>
</body>
~~~

~~~js
$(document).ready(function(){
	const record = document.getElementById('record');
	const stop = document.getElementById('stop');
	const soundClips = document.getElementById('sound-clips');
	
	if(navigator.mediaDevices){
		var constraints = {
				audio:true
		}
		
		let chunks = []; // 녹음 데이터 저장하기 위한 변수
		
		navigator.mediaDevices.getUserMedia(constraints)
		.then(stream => {
			const mediaRecorder = new MediaRecorder(stream);
			
			// 녹음 버튼 클릭했을 때
			record.onclick = () => {
				mediaRecorder.start(); //녹음 시작
				record.style.background = "red";
				record.style.color = "black";
			};
			
			
			// 정지 버튼 눌렀을 때
			stop.onclick = () => {
				mediaRecorder.stop(); // 녹음 정지
				record.style.background = "";
				record.style.color = "";
			};
			
			mediaRecorder.onstop = e => {
				// (1) <audio> 태그 담을 컨테이너 객체 생성
				const clipcontainer = document.createElement('article');					
				
				// (2) audio 객체 생성 및 속성 설정
				const audio = document.createElement('audio');	
				audio.setAttribute('controls', '');
				
				// (3) 컨테이너에 audio 연결
				clipcontainer.appendChild(audio);
				
				// <div>에  <audio> 태그 출력
				// 이전에 녹음할 때 추가한 childNode가 존재한다면 제거하고
				if(soundClips.hasChildNodes())
					soundClips.removeChild(soundClips.childNodes[0]);
				//추가
				soundClips.appendChild(clipcontainer);
				
				// chunks에 저장된 녹음 데이터를  audio 양식으로 설정
				const blob = new Blob(chunks, {
					'type': 'audio/mp3 codecs=opus'
				});
				
				// chunks 초기화 (초기화 하지 않으면 녹음 내용이 누적 저장됨)
				chunks = [];
				
				// audio 소스 지정
				const audioURL = URL.createObjectURL(blob);
				audio.src = audioURL;
				
				
				// (4) 녹음 내용을 파일로 저장
				// 파일명
                const clipName = "voiceRecord"
                const a = document.createElement('a');
                clipcontainer.appendChild(a);
                a.href = audio.src;

                a.download = clipName;
                a.click();
				};
				
				
				// 녹음 시작 상태가 되면 chunks에   녹음 데이터 저장
				mediaRecorder.ondataavailable = e => {
					chunks.push(e.data);
				};
			
		})
		.catch(err => {
			console.log("오류 발생 : " + err)
		})
	}
});
~~~

## \<canvas>태그
- 도형이나 이미지 출력

##### \<canvas>태그 예제 - canvas.html

~~~html
  <script src="jquery-3.6.0.min.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
                var canvas = document.getElementById('rectCanvas');
                var context = canvas.getContext('2d');

                $('#drawBtn').on('click', () => {
                    // 색상 지정
                    context.fillStyle = 'green';
                    // 테두리만 있는 사각형
                    context.strokeRect(10, 10, 250, 250); // x, y, width, height
                    // 색이 채워진 사각형 그리기
                    context.fillRect(280, 10, 250, 250);
                    // 색상 변경
                    context.fillStyle = 'pink';
                    context.fillRect(530, 10, 250, 250);

                    // 특정 영역 지우기
                    context.clearRect(300, 50, 100, 100);
                })
                $('#clearCanvas').on('click', () => {
                    context.clearRect(0, 0, 800, 800);
                })
                $('#drawImage').on('click', () => {
                    var image = new Image();
                    image.src = "image/apple.png";
                    image.onload = function() {
                        context.drawImage(image, 0, 0, image.width, image.height);
                    }
                })
           });
        </script>
</head>
<body>
    <button id="drawBtn">사각형 그리기</button>
    <button id="clearCanvas">캔버스 지우기</button>
    <button id="drawImage">이미지 출력</button><br><br>
    <canvas id="rectCanvas" width="800" height="600"></canvas>
</body>
~~~

##### \<canvas>태그 문제 - pose.html

~~~html
 <script src="jquery-3.6.0.min.js"></script>
        <script src="pose.js"></script>
        <script type="text/javascript">
           $(document).ready(function() {
                
           });
        </script>
</head>
<body>
    <h2>포즈 인식</h2>
	<button id="showBtn">결과 확인</button><br><br>
	<h3>포즈 인식 결과를 이미지에 좌표로 표시</h3>
	<canvas id="poseCanvas" width="600" height="600"></canvas>
	<div id="resultDiv"></div>
</body>
~~~

~~~js
// $(document).ready(function(){ 축약형
$(function(){
	// [결과 확인] 버튼 클릭하면 서버에서 좌표 받아서
	// 이미지 출력하는 drawCanvas() 함수 호출 : 좌표, 이미지  src 전달
	$('#showBtn').on('click', function() {
		// 서버에서 응답 결과로 좌표 값 받았다고 가정
		var result = {"points": [{"x":0.42, "y":0.20}, {"x":0.49, "y":0.22}, {"x":0.42, "y":0.27}, {"x":0.30, "y":0.33}, 
									   		 {"x":0.32, "y":0.22}, {"x":0.52, "y":0.25}, {"x":0.65, "y":0.31}, {"x":0.72, "y":0.41}, 
						                     {"x":0.61, "y":0.51}, {"x":0.65, "y":0.69}, {"x":0.81, "y":0.82}, {"x":0.51, "y":0.51}, 
                                             {"x":0.29, "y":0.51}, {"x":0.35, "y":0.72}, {"x":0.39, "y":0.18}, {"x":0.49, "y":0.18}]};
		var src = "image/run.jpg";
		drawCanvas(result.points, src);
	});
	function drawCanvas(result, src){
		// 캔버스 생성
		var canvas = document.getElementById('poseCanvas');
		var context = canvas.getContext("2d");
		// 이미지 생성
		var poseImage = new Image();
		poseImage.src = src;
		poseImage.width = canvas.width;
		poseImage.height = canvas.height;

		poseImage.onload = function() {
			context.drawImage(poseImage, 0, 0, poseImage.width, poseImage.height);
			// 색상 배열 지정
			var colors = ["red", "blue", "yellow", "yellow",
								"yellow","green", "green","green", 
								"skyblue","skyblue","skyblue","white",
								"white","white","brown","gold"];
			// 포지션 배열 지정
			var position = ["코", "목", "오른쪽 어깨", "오른쪽 팔굼치", 
									"오른쪽 손목", "왼쪽 어깨", "왼쪽 팔굼치", "왼쪽 손목", 
									"오른쪽 엉덩이", "오른쪽 무릎", "오른쪽 발목", "왼쪽 엉덩이", 
				                    "왼쪽 무릎", "왼쪽 발목", "왼쪽 눈", "왼쪽 귀"];
			var values = "";
			// 각 좌표를 이미지에 표시
			//$.each(배열, 콜백함수)
			$.each(result, function(i){
				if(this.x !=0 || this.y != 0){
					context.strokeStyle = colors[i];
					context.strokeRect(this.x*poseImage.width, this.y*poseImage.height, 2, 2);
					var text = this.x.toFixed(2) + "," + this.y.toFixed(2);
					context.font = '10px';
					context.strokeText(text, this.x*poseImage.width, this.y*poseImage.height);
				}
				values += position[i] + " (" + this.x + ", " + this.y + ") <br>";
			});
			// resultDiv <div>에 포지션(좌표) 출력
			$('#resultDiv').html(values);
		};	
	}//  drawCanvas() 끝
}); 
~~~