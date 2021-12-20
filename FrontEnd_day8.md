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

### 폼 유효성 확인
- \<input>성명을 입력하지 않은 경우
- \<input>id를 입력하지 않은 경우 혹은 길이가 6 ~ 10자가 아닌 경우
- \<input>비밀번호와 비밀번호 확인의 값이 같지 않은 경우
  - var 변수 이름 = document.getElementById('id 속성 값')
  - if(변수 이름.value == "") { 값이 유효하지 않을 때 실행할 문장 };
- \<select> 태그에서 선택하지 않은 경우
  - 목록에 있는 여러 항목 중 선택
  - 항목 선택하면 selectedIndex 속성에 선택된 항목의 인덱스 값 저장(0부터 시작)
  - 하나도 선택하지 않으면 selectedIndex 값은 -1
    - 첫 번째 \<option> 태그를 빈값으로 하고,
    - if(job.selectedIndex == -1) { 선택하지 않았을 때 실행할 문장 };
  - 또는 \<option> 태그 중 하나를 빈 값으로 지정하고, 값이 없으면 선택하지 않은 것으로 처리해도 됨.
    - \<option value = "" selected> 직업선택
    - if(job.value =="") { 선택하지 않았을 때 실행할 문장 }
  - 또는 \<option> 태그 하나를 미리 선택해 놓으면 유효성 확인이 필요 없다.
    - \<option value="프로그래머" selected>프로그래머
- 라디오 버튼 하나도 체크하지 않은 경우
  - \<input type="radio>
  - 그룹에서 여러 개 중 한 개만 선택 가능
  - 그룹에 속한 여러 개의 라디오 버튼의 그룹 이름(name 속성)이 동일하므로 라디오 버튼(객체)는 배열로 사용
  - 배열의 각 원소를 하나씩 확인
    - checked 속성이 true면 확인된 상태
    - false면 체크되지 않은 상태
    - for문 / if 문 사용
  - 미리 체크되어 있게 하면 유효성 검사 필요 없음.
- 체크박스에서 하나도 선택하지 않은 경우
  - \<input type="checkbox">
  - 여러 개 선택 가능
  - checked 속성이 true면 체크된 상태, false면 체크되지 않은 상태
  - 모든 체크박스 확인해야 함.

##### 폼 유효성 확인 예제 - 입력 값 확인 join.html, checkForm.js

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="checkForm.js"></script>
    
</head>
    <body>
    	<div id="wrap">
              <div id="joinBox">                     
                  <h2  align="center">회원가입</h2>
                  <hr>
                   <form name="newMemberForm" id="joinForm" method="post" action="newMemberOk.jsp">
                       <table align="center">	
                           <tr>
                               <td>성명</td>
                               <td><input type="text" name="names" id="name"></td>
                           </tr>
                           <tr>
                               <td>아이디</td>
                               <td><input type="text" name="id" id="id" border=0> 
                               <input type="button" value="ID중복체크"> (영문자+특수문자: 6~10자)</td>
                           </tr>
                           <tr>
                               <td>비밀번호</td>
                               <td><input type="password" name="password" id="password" size="21"> 
                               (영문자+숫자+특수문자: 10~20자)</td>
                           </tr>
                           <tr>
                               <td>비밀번호 확인</td>
                               <td><input type="password" name="passwordCheck" id="passwordCheck" size="21"></td>
                           </tr>	
                           <tr>
                               <td>생년월일 </td>
                               <td>
                                   <input type="text" name="birthYear" id="birthYear" size="4">년
                                   <select name="birthMonth">
                                       <option value="1">1
                                       <option value="2">2
                                       <option value="4">3
                                       <option value="4">4
                                       <option value="5">5
                                       <option value="6">6
                                       <option value="7">7
                                       <option value="8">8
                                       <option value="9">0
                                       <option value="10">10
                                       <option value="11">11
                                       <option value="12">12 
                                   </select> 월
                                   <select name="birthDay">
                                       <option value="1">1
                                       <option value="2">2
                                       <option value="4">3
                                       <option value="4">4
                                       <option value="5">5
                                       <option value="6">6
                                       <option value="7">7
                                       <option value="8">8
                                       <option value="9">0
                                       <option value="10">10
                                       <option value="11">11
                                       <option value="12">12
                                       <option value="13">13
                                       <option value="14">14
                                       <option value="15">15
                                       <option value="16">16
                                       <option value="17">17
                                       <option value="18">18
                                       <option value="19">19
                                       <option value="20">20
                                       <option value="21">21
                                       <option value="22">22
                                       <option value="23">23
                                       <option value="24">24
                                       <option value="25">25
                                       <option value="26">26
                                       <option value="27">27
                                       <option value="28">28
                                       <option value="29">29
                                       <option value="30">30
                                       <option value="31">31 
                                   </select> 일
                                   <input type="radio" name="solar" value="양력" checked>양력
                                   <input type="radio" name="solar" value="음력">음력
                               </td>
                           </tr>        
                           <tr>
                               <td>전화번호 </td>
                               <td><select name="tel1">
                                   <option value="02" selected>02
                                   <option value="031">031
                                   <option value="043">043
                                   </select>
                                    - <input type="text" name="tel2" id="tel2" size="4">
                                    - <input type="text" name="tel3" id="tel3"size="4">
                               </td>
                           </tr>
                           <tr>
                               <td>휴대폰번호 </td>
                               <td><select name="hp1">
                                   <option value="000">000
                                   <option value="010" selected>010
                                   </select>
                                    - <input type="text" name="hp2"  id="hp2"size="4">
                                    - <input type="text" name="hp3"  id="hp3"size="4">
                               </td>
                           </tr>
                           <tr>
                               <td>주소 </td>
                               <td><input type="text" name="zipcode" id="zipcode"readonly> 
                               <input type="button" value="우편번호찾기"><br>
                               <input type="text" name="address1" id="address1" size="40"><br>
                               <input type="text" name="address2" id="address2" size="40">상세 주소 입력
                               </td>
                           </tr>                                    
                           <tr>
                               <td>성별</td>
                               <td>
                                   <input type="radio" name="sex" value="남" checked>남
                                   <input type="radio" name="sex" value="여">여
                               </td>
                           </tr>		
                           <tr>
                               <td valign="top">직업</td>
                               <td>
                                   <select name="job" id="job">
                                       <option value="">직업선택
                                       <option value="웹디자이너">웹디자이너
                                       <option value="프로그래머">프로그래머
                                       <option value="회사원">회사원
                                       <option value="학생">학생
                                       <option value="영화감독">영화감독
                                       <option value="웹마스터">웹마스터
                                   </select>
                               </td>
                           </tr>
                           <tr>
                               <td valign="top">이메일</td>
                               <td>
                                   <input type="text" name="email1"  id="email1" size="6">@<select name="email">
                                       <option value="naver"  selected>naver.com
                                       <option value="gmail">gmail.com
                                       <option value="nate">nate.com
                                       <option value="hanmail">hanmail.net
                                   </select>
                               </td>
                           </tr>
                           <tr>
                               <td>이메일 수신 여부</td>
                               <td>
                                   <input type="radio" name="emailRcv" value="yes">예
                                   <input type="radio" name="emailRcv" value="no">아니오
                               </td>
                           </tr>       
                            <tr>
                               <td>동의</td>
                               <td>
                                   <label><input type="checkbox" id="agreement1" value="프론트엔드">모든 약관에 동의</label>
							        <label><input type="checkbox" id="agreement2" value="백엔드">개인 정보 이용 동의</label>
                               </td>
                           </tr>		
                           <tr>
                               <td colspan="2" align="center">
                                   <input type="submit" value="회원가입">
                                   <input type="reset" value="취    소">
                               </td>
                           </tr>
                       </table>	
                   </form>
             </div>    
        </div>
	</body>
</html>
~~~

~~~js
window.onload = function() {
    // 폼에서 id가 joinForm인 폼의 submit 버튼이 눌러졌을 때 수행되는 이벤트 처리
    document.getElementById('joinForm').onsubmit = function() {
        // 성명을 입력하지 않은 경우 경고창 띄우기
        // 성명 입력 칸의 id를 찾아오기
        var name = document.getElementById('name')
        // 값이 비었는지 확인 후 비었으면 경고 출력, 입력란에 포커스, 서버로 전송되지 않게(다음 페이지로 이동 못하게)
        if(name.value == "") {
            alert("성명을 입력하세요.");
            name.focus();
            return false; // 서버로 전송되지 않게 함.
        } // 이름 검증 끝

        var id = document.getElementById('id');
        if(id.value == "") {
            alert("아이디를 입력하세요.");
            id.focus();
            return false;
        } // 아이디 입력 됐는지 검사

        if(id.value.length < 6 || id.value.length > 10) { // 글자 수 검사
            alert("아이디는 6~10자로 입력하세요.");
            id.focus();
            id.value = "";
            return false;
        } // 아이디 검증 끝

        var password = document.getElementById('password');
        if(password.value == "") {
            alert("비밀번호를 입력하세요.");
            password.focus();
            return false;
        } // 비밀번호 입력 됐는지 검사

        var passwordCheck = document.getElementById('passwordCheck');
        if(passwordCheck.value == "") {
            alert("비밀번호 확인을 입력하세요.");
            passwordCheck.focus();
            return false;
        } // 비밀번호 확인 입력 됐는지 검사

        if(password.value != passwordCheck.value) {
            alert("비밀번호와 비밀번호 확인이 일치하지 않습니다.");
            password.focus();
            password = "";
            passwordCheck = "";
            return false;
        } // 비밀번호와 비밀번호 확인이 일치하는지 검사

        // 직업을 선택하지 않은 경우 검사
        var job = document.getElementById('job');
        if(job.value == "") {
            alert("직업을 선택해 주세요.");
            return false;
        } // 직업 선택 검사 완료
        // if(job.selectedIndex == 0) {
        //     alert("직업을 선택해 주세요.");
        //     return false;
        // } // 직업 선택 검사 완료

        // radio 버튼 검사.
        // radio 버튼의 경우 id 속성을 사용하지 않고 그룹 이름인 name 속성 사용
        // 동일 그룹에 속한 여러 라디오 버튼(객체)는 동일한 name : 배열로 처리
        // 체크 여부를 저장할 변수 선언
        var chk = false;
        for(var i = 0; i < joinForm.emailRcv.length; i++) {
            if(joinForm.emailRcv[i].checked == true) {
                chk = true; // 하나라도 체크되면 true값 저장
                // 하나도 체크되지 않으면 false 값 그대로 유지.
            }
        }
        if(chk == false) { // 하나도 체크되지 않았을 경우
            alert("이메일 수신 여부를 선택해 주세요.")
            return false;
        }  // radio 버튼 검사 끝.

        // 체크박스를 하나도 선택하지 않은 경우 검사
        var agreement1 = document.getElementById('agreement1');
        var agreement2 = document.getElementById('agreement2');
        if(agreement1.checked == false && agreement2.checked == false) {
            alert("두 약관 중 하나의 약관이라도 동의해 주세요.")
            return false;
        }
    }; // onsubmit 끝
}; // window.onload 끝
~~~

## getElementById() 사용
- DOM 요소가 로드된 상태라면 getElementById() 사용하지 않고 id 속성만으로 요소 사용 가능
  - 동일한 이름의 전역 변수가 존재한다면 작동 안 됨.

## 사용자 정의 객체
- 사용자가 직접 필요한 객체를 생성해서 사용
- 사용자 정의 객체 생성 방법
  - 리터럴 이용
  - 생성자 함수(function()) 이용
  - new Object() 이용
  - class 정의하고 객체 생성

### 리터럴 이용
- 객체 선언 : 멤버 추가
  - 프로퍼티(속성) : 속성값
  - 멤버 메소드 추가
- 형식
~~~js
var 객체 = {
    // 변수 :프로퍼티(속성)
    프로퍼티명(속성명)1 : 값1,
    프로퍼티명(속성명)2 : 값2

    // 멤버 메소드
    메소드 명 : function() {
        수행 코드
    }
};
// 예시
var person = {
    name : "홍길동",
    age : 20,
    getName = function() {
        return this.name;
    }
};
// 객체 사용
객체.프로퍼티;
객체.메소드();
// 예시
person.getName(); // 객체의 멤버 메소드 사용(호출);
~~~

##### 리터럴 객체 이용 예제 - object-literal.html

~~~html
        <script type="text/javascript">
            // 객체 생성
            var person = {
                name : "홍길동",
                age : 20,
                getName : function() {
                    return this.name;
                }
            };
            // 객체 사용
            console.log(person.name);
            console.log(person.age);
            console.log(person.getName());
            // 프로퍼티 존재 여부 확인
            console.log("name" in person);
            // @@출력문@@
            // 홍길동
            // 20
            // 홍길동
            // true

            // 객체 생성 : 프로퍼티만 존재
            let car = {
                no : "11가 1111",
                name : "소나타",
                maker : "현대",
                cc : 2000,
                year : 2021
            };
            // 전체 프로퍼티값 출력
            for(let i in car) {
                console.log(car[i]);
            }
            // @@출력문@@
            // 11가 1111
            // 소나타
            // 현대
            // 2000
            // 2021

            // 객체 생성 : 
            var circle = {
                center : {x:1.0, y:2.0},
                radius : 2.5,
                getArea : function() {
                    return this.radius * this.radius * 3.14;
                }
            };
            console.log(circle.center.x, circle.center.y);
            console.log(circle.getArea());
            // @@출력문@@
            // 1 2
            // 19.625

            // 호이스팅도 가능.
            // 두 점 사이의 거리를 구하는 예
            // 두 점 사이의 거리를 구해서 반환하는 함수
            var p1 = {x:1, y:2};
            var p2 = {x:4, y:5};
            var distance = getDistance(p1, p2);
            console.log(distance.toFixed(2)); // 4.24

            function getDistance(p1, p2) {
                var dx = p2.x - p1.x;
                var dy = p2.y - p1.y;
                return Math.sqrt(dx*dx + dy*dy); // 두 점 사이의 거리 구해서 반환
            }
~~~

### 생성자 함수 (function) 이용
- 함수 선언과 같은 방식으로 function 키워드 사용하여 선언(정의)
- 함수를 클래스처럼 사용
  - function 함수명() : 생성자 기능
- 프로퍼티 사용 : this.프로퍼티
- new 연산자를 사용해서 객체 생성
- 형식

~~~js
// 함수(클래스로 이용) 선언 (생성자 기능)
function 함수명() {
    // 프로퍼티 추가
    this.프로퍼티 : 값 1,
    this.프로퍼티 : 값 2,
    // 메소드 추가
    this.메소드 = function() {
        수행 코드;
    };
}
// 객체 생성
var 객체(인스턴스) = new 함수명(); // 생성자 생성하듯.
객체.메소드();
객체.프로퍼티1;

// 함수(클래스로 이용) 선언 (생성자 기능)
function People() {
    //프로퍼티 추가
    this.name : "홍길동",
    this.age = 20,
    // 메소드 추가
    this.getName = function() {
        return this.name;
    };
}
// 객체 생성
var person = new People(); // 생성자 처럼 사용
person.getName(); // 메소드 호출
~~~

##### 생성자 함수 이용 예제 - object2-function.html

~~~html
        <script type="text/javascript">
            // 멤버변수 : 프로퍼티(속성)
            function People() {
                this.name = "홍길동";
                this.age = 20;
                this.getName = function() {
                    return this.name;
                };
            }
            // new 연산자를 사용해서 객체(인스턴스) 생성
            var person = new People();
            console.log(person.name);
            console.log(person.age);
            console.log(person.getName());
            // 홍길동
            // 20
            // 홍길동

            // 생성자 함수를 변경하지 않고도 function() { } 외부에서 프로퍼티(속성) 추가 가능.
            person.address = "서울";
            // 메소드 추가
            person.getAddress = function () {
                return this.address;
            }
            // 새로 추가된 메소드 호출
            console.log(person.address);
            console.log(person.getAddress());
            // 서울
            // 서울

            // person2 객체 새로 생성
            // address는 person에만 추가한 것이기 때문에 person2에는 없다 -> 호출하면 오류 발생
            var person2 = new People();
            // console.log(person2.getAddress());

            function Book(title, author, price, date) {
                this.title = title;
                this.author = author;
                this.price = price;
                this.date = date;

                // 메소드
                this.getBook = function() {
                    return this.title + " " + this.author + " " + this.price + " " + this.date;
                }
            }

            let book = new Book("자바스크립트", "홍길동", 2000, "2021-11-11");
            console.log(book.getBook());
            // 자바스크립트 홍길동 2000 2021-11-11

            // 함수이므로 호이스팅 가능
            // function Book(title, author, price, date) {
            //     this.title = title;
            //     this.author = author;
            //     this.price = price;
            //     this.date = date;

            //     // 메소드
            //     this.getBook = function() {
            //         return this.title + " " + this.author + " " + this.price + " " + this.date;
            //     }
            // }
        </script>
~~~

##### 생성자 함수 이용 예제 ul태그 객체 생성 - object3-function2.html

~~~html
        <script type="text/javascript">
            // 생성자 함수를 이용해서 객체 정의(선언)
            function ListTag() {
                //프로퍼티 지정
                this.ulTag = document.createElement("ul");
                this.ulTag.type = "square";
                // li 태그 생성해서 ul 태그에 추가
                for(var i = 1; i <= 5; i++) {
                    var listItem = document.createElement("li");
                    var itemInput = prompt("꽃" + i  + "입력");
                    listItem.innerHTML = itemInput;
                    // u l태그에 li 추가
                    this.ulTag.appendChild(listItem);
                }
                // 멤버 메소드
                this.getListItem = function() {
                    return this.ulTag;
                }
            }
            // 객체 생성
            window.onload = function() {
                var list = new ListTag(); // 객체 생성
                // div 태그에 ul 태그(객체) 추가
                var box = document.getElementById('box');
                box.appendChild(list.getListItem());
            }
        </script>
</head>
<body>
    <div id="box"></div>
</body>
~~~

### 프로토타입
- 객체를 만드는 원형
- 함수도 객체이고, 객체인 함수가 기본으로 갖고 있는 프로퍼티
- 함수의 객체가 생성될 때 모든 객체가 공유하는 공간
- 자바의 static 개념
- 프로토타입 멤버 정의
  - 멤버를 함수 외부에 선언
  - 여러 객체가 공유하게 하는 방법
- 프로토타입 사용 시 이점
  - 생성자 함수 이용해서 객체를 생성할 때 프로퍼티와 메소드는 객체마다 생성
    - 사용하지 않을 때도 생성되기 때문에 메모리 낭비가 생길 수 있다.
  - 프로퍼티와 메소드를 미리 만들어놓지 않고 필요 시 추가한 후 모든 객체에서 공유함으로써 메모리 낭비 줄일 수 있다.

##### 프로토타입 예제 - object4-prototype.html

~~~html
        <script type="text/javascript">
            function People() {
                this.age = 20;
            }
            var person1 = new People();
            var person2 = new People();
            var person3 = new People();

            // person1 객체에 메소드 추가
            person1.setAge = function() {
                this.age += 10;
            }

            // 프로토타입 프로퍼티에 setAge() 메소드 정의
            People.prototype.setAge = function() { // People의 모든 객체에 사용하는 것.
                this.age += 1;
            }

            // 프로토타입 프로퍼티에 getAge() 메소드 정의
            People.prototype.getAge = function() { // People의 모든 객체에 사용하는 것.
                return this.age;
            }

            person1.setAge(); // person1.setAge() 호출됨
            person2.setAge(); // People.prototype.setAge() 호출
            person3.setAge(); // People.prototype.setAge() 호출

            // console.log(person1.age); // 30
            // console.log(person2.age); // 21
            // console.log(person3.age); // 21

            console.log(person1.getAge()); // 30
            console.log(person2.getAge()); // 21
            console.log(person3.getAge()); // 21
        </script>
~~~

### new Object() 이용
- new Object()로 빈 객체 생성 후 프로퍼티 추가
- 멤버 메소드 추가
- 객체.메소드() // 객체의 멤버 메소드 사용
- 형식

~~~js
var 객체 = new Object(); // 빈 객체 생성(new는 생략 가능)
// 프로퍼티 추가
객체.프로퍼티 = 값;
// 멤버 메소드 추가
객체.메소드명 = function() {
    코드
}
// 객체의 멤버 메소드 호출
객체.메소드();
~~~

##### new Object() 예제 - object5-Object.html

~~~html
        <script type="text/javascript">
            // new Object() 이용해서 빈 객체 생성
            var person = new Object();
            // 프로퍼티 추가
            person.name = "홍길동";
            person.age = 20;

            // 멤버 메소드 추가
            person.getName = function() {
                return this.name;
            }

            console.log(person.getName()); // 홍길동
            console.log(person.age); // 20
        </script>
~~~

### class 정의하고 객체 생성
- class 키워드 사용
- 생성자 / Getters / Setters 사용 가능
  - Getters : 함수명 앞에 get이라고 붙이면 됨
    - 프로퍼티 사용 시 앞에 언더바(_)를 붙여서 사용
  - Setters : 함수명 앞에 set이라고 붙이면 됨
    - 프로퍼티 사용 시 앞에 언더바(_)를 붙여서 사용
  - Getter, Setter 호출 시 괄호 안 붙임
    - 객체.메소드;
- 호이스팅 불가
- 형식

~~~js
class 클래스명 {
    생성자() { }
    Getters
    Setters
    메소드();
}
// 객체 생성
let 객체 = new 클래스명();
객체.메소드();
~~~

##### class 정의 후 객체 생성 예제 - object6-Class.html

~~~html
        <script type="text/javascript">
            class Person {
                // 생성자
                constructor(name, age) {
                    // 프로퍼티 정의
                    this.name = name;
                    this.age = age;
                }
                // Getter : 프로퍼티 반환
                get name() {
                    return this._name;
                }
                get age() {
                    return this._age;
                }
                // Setter : 프로퍼티 값 설정
                set name(name) {
                    this._name = name;
                }
                set age(age) {
                    this._age = age;
                }
                // 필요한 메소드 추가
                toString() {
                    return this.name + "은 " + this.age + "살 입니다.";
                }
            }
            // 호이스팅 불가 : 클래스 생성 이전 객체 생성 불가
            let person1 = new Person("홍길동", 25);
            let person2 = new Person("이몽룡", 30);
            // getter 호출
            console.log("성명 : " + person1.name + " 나이 : " + person1.age); // 성명 : 홍길동 나이 : 25
            console.log("성명 : " + person2.name + " 나이 : " + person2.age); // 성명 : 이몽룡 나이 : 30
            // toString() 메소드 호출
            console.log(person1.toString()); // 홍길동은 25살 입니다.
            console.log(person2.toString()); // 이몽룡은 30살 입니다
            // setter 호출 : 괄호 없음
            person1.age = 27;
            console.log(person1.toString()); // 홍길동은 27살 입니다.
            person2.name = "성춘향";
            person2.age = 20;
            console.log(person2.toString()); // 성춘향은 20살 입니다.
        </script>
~~~

##### Class 정의 후 객체 생성 연습 문제 - object7-ClassEx.html

~~~html
        <script type="text/javascript">
            class Rectangle {
                constructor(width, height) {
                    this.width = width;
                    this.height = height;
                }
                get width() {
                    return this._width;
                }
                get height() {
                    return this._height;
                }
                set width(width) {
                    this._width = width;
                }
                set height(height) {
                    this._height = height;
                }
                getArea() {
                    return "사각형의 넓이 : " + this.width*this.height;
                }
            }
            let rectangle1 = new Rectangle();
            rectangle1.width = 30;
            rectangle1.height = 10;
            console.log("가로길이 : " + rectangle1.width + " 세로 길이 : " + rectangle1.height);
            console.log(rectangle1.getArea());
            rectangle1.width = 20;
            rectangle1.height = 30;
            console.log(rectangle1.getArea());
        </script>
~~~

## JSON(JavaScript Object Notation)
- 자바스크립트 객체 표기법
- key-value 쌍으로 구성된 형태의 객체 표기법
- 클라이언트와 서버 사이 데이터 교환 목적으로 사용
- 웹 서버에서 수신하는 데이터는 문자열인데, 문자열 데이터를 JSON 파싱 함수를 사용해서 자바스크립트 객체로 변환 가능
- 최근 브라우저들은 전부 내장 객체로 JSON 변환 기능 지원
- JSON 데이터 형식
  - {key : value}
  - {"name" : "홍길동"}

## 자바스크립트 객체 JSON 변환
- 자바스크립트 객체 to JSON data로 변환
  - stringify() 메소드 사용
    - 결과 : JSON 형태의 문자열
- JSON data to 자바스크립트로 변환 
  - parse() 메소드
    - 결과 : object

##### JSON parsing 예제 - json-Parsing.html

~~~html
        <script type="text/javascript">
            let car = {
                no : "11가 1111",
                name : "소나타",
                maker : "현대",
                cc : 2000,
                year : 2021
            };
            // 자바스크립트 객체를 JSON 데이터로 변환

            console.log(car)
            // {no: '11가 1111', name: '소나타', maker: '현대', cc: 2000, year: 2021}

            var json = JSON.stringify(car);
            console.log(json);
            // {"no":"11가 1111","name":"소나타","maker":"현대","cc":2000,"year":2021}

            // JSON 데이터를 자바스크립트 객체로 변환
            var obj = JSON.parse(json);
            console.log(obj);
            // {no: '11가 1111', name: '소나타', maker: '현대', cc: 2000, year: 2021}
            console.log(obj.no); // 11가 1111
            console.log(obj.name); // 소나타

            for(var i in obj) {
                console.log(obj[i]);
            }
            // 11가 1111
            // 소나타
            // 현대
            // 2000
            // 2021
        </script>
~~~

##### JSON parsing 연습문제 - jsonEx.html

~~~html
<script type="text/javascript">
            // 이미 json 값임.
            let result = {"version":"v2","userId":"U47b00b58c90f8e47428af8b7bddc1231heo2","timestamp":1621444015108,"bubbles":[{"type":"text","data":{"description":"저는 독서 지도사입니다"},"information":[{"key":"chatType","value":"TEXT"},{"key":"chatType","value":"TEXT"},{"key":"score","value":"1.0"},{"key":"scenarioName","value":"자기 소개"},{"key":"conversationTypes","value":"소개␞직업␞일␞역할␞담당␞누구"},{"key":"matchingType","value":"exactMatch"},{"key":"domainCode","value":"ai_chatbot_ex"}],"context":[]}],"scenario":{"name":"자기 소개","chatUtteranceSetId":3305931,"intent":["소개","직업","일","역할","담당","누구"]},"entities":[],"keywords":[],"event":"send"};
            console.log(result);
            var bubbles = result.bubbles;
            // 저는 독서 지도사입니다. 추출
            for(var i in bubbles) {
                console.log(bubbles[i].data.description);
            }
            // scenario.name에서 "자기소개" 추출
            var scenario = result.scenario.name;
            console.log(scenario);
            // 소개, 직업, 일, 역할, 담당, 누구 추출
            var intent = result.scenario.intent;
            for(var i in intent) {
                console.log(intent[i]);
            }

            let result2 = {"version":"v2","userId":"U47b00b58c90f8e47428af8b7bddc1231heo2","timestamp":1621393563377,"bubbles":[{"type":"template","data":{"cover":{"type":"image","data":{"imageUrl":"https://clovachatbot.ncloud.com/ib496e504bl244-0639-439d-93b0-ec4d72655cf8","imagePosition":"top","action":{"type":"link","data":{"url":"https://www.multicampus.com/cs/map/mapMain?p_menu=MTA1I01BSU4=&p_gubun=Qw==&req=0"}}}}}}],"scenario":{"name":"독서 모임 장소 약도 문의","chatUtteranceSetId":3306432,"intent":["장소","위치","지도","약도"]},"entities":[],"keywords":[],"event":"send"};
            var bubbles2 = result2.bubbles;
            for(var i in bubbles2) {
                console.log(bubbles2[i].data.cover.data.imageUrl);
            }
        </script>
~~~

## jQuery
- 자바스크립트 라이브러리
- 자바스크립트를 이용해 만든 다양한 함수들의 집합
- 무료 사용 가능한 오픈 소스 라이브러리
- 모든 웹 브라우저에서 동작
- 특징
  - 용량이 약 100KB로 가벼움
  - 동적으로 HTML이나 CSS 컨트롤 능력 탁월
  - 짧고 간결하게 코딩 가능
  - 웹 표준과 타 브라우저 호환성 뛰어남
  - 편리한 Ajax 호출 방법
  - 메소드 체인 방식(여러 메소드를 연결하여 사용)으로 효율적인 코딩 가능, 간결하고 효과적인 코드 수정 가능
  - 다양한 플러그인 제공
- 목적
  - 쉬운 DOM cjfl
  - 쉽고 일관된 이벤트 연결 구현
  - 쉬운 시작적 효과 구현
  - Ajax 기능 쉽게 구현
- 기능
  - DOM 처리
  - 이벤트 처리
  - 시각 효과 구현
  - Ajax 기능 구현
- 개발 환경
  - 파일 다운로드 방식
  - CDN 이용하는 방식

##### jQuery 시작 예제 - jQuery-Start.html

~~~html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
        <script src="jquery-3.6.0.min.js"></script>
        <script src="start.js"></script>
</head>
~~~

##### jQuery 시작 예제 - jQuery-StartExternal.html, start.js

~~~html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
        <script src="jquery-3.6.0.min.js"></script>
        <script src="start.js"></script>
</head>
~~~

~~~js
$(document).ready(function() {
    alert("jQuery 시작 - external 방식");
});
~~~

## jQuery 코드 형태
- 객체 구조로 객체.메소드 형태
- 객체 선택
  - %('선택자').메소드
  - $('p').css('color', 'red') : 모든 \<p> 태그 선택하고 스타일 적용
- 사용자가 생성한 객체 사용
  - 객체.메소드
  - var obj = $('선택자').메소드;
  - obj.메소드
- 메소드 체이닝
  - 여러 개의 메소드를 연결해서 사용
  - 객체.메소드1.메소드2.@@@@.메소드n;
- jQuery 치환
  - jQuery의 모든 함수 및 객체는 jQuery에서 제공되는 것이라는 점을 나타내기 위해 코드 앞에 jQuery라는 키워드를 사용
    - jQuery(document).ready( function(){ alert("jQuery 시작 - external 방식"); } );
  - 쉽게 하기 위헤 $로 치환해서 사용
    - $(document).ready( function(){ alert("jQuery 시작 - external 방식"); } );
- $(document).ready(함수) 명령어
  - 화면에 페이지가 로딩된 후 실행
  - HTML 문서가 화면에 보여진 후 자동으로 포함된 함수 실행
  - 자바스크립트의 window.onload와 동일하게 사용
    - window.onload = function() { @@@ };
- $(document).ready()와 window.onload = function()
  - 공통점
    - 콜백 함수가 호출되는 시점에서 DOM 요소에 접근 가능
  - 차이점
    - $(document).ready()는 DOM 요소가 load 되었을 때 이벤트 발생하며 호출(외부 리소스, 이미지, 또는 음악 등이 로드 되기 전)
    - window.onload = function()은 DOM 요소 뿐 아니라 외부 리소스, 이미지 또는 음악 등 모든 컨텐츠의 로드가 끝나는 시점에서 이벤트 발생하며 호출
- $(document).ready(함수)의 단축 형태
  - $(function() { @@@ });

### jQuery 선택자
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

##### 태그 선택자 - tag-Select.html

~~~html
    <script src="jquery-3.6.0.min.js"></script>
    <script type="text/javascript">
       $(document).ready(function() {
           // 태그 선택자
            $('h1').css('color', 'red');
            $('h1').css('background', 'black');
            //메소드 체인 방식
            $('h1').css('width', '50%').css('height', '40px');
       });
    </script>
</head>
<body>
    <h1>Header1</h1>
    <h1>Header2</h1>
    <h1>Header3</h1>
</body>
~~~

##### 아이디 선택자 - id-Select.html

~~~html
    <script src="jquery-3.6.0.min.js"></script>
    <script type="text/javascript">
       $(document).ready(function() {
           // 아이디 선택자
            $('#h1').css('color', 'red');
            $('#h2').css('background', 'black');
            //메소드 체인 방식
            $('h1').css('width', '50%').css('height', '40px');
       });
    </script>
</head>
<body>
    <h1 id="h1">Header1</h1>
    <h1 id="h2">Header2</h1>
    <h1>Header3</h1>
</body>
~~~

##### 클래스 선택자 - classSelector.html

~~~html
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
				});
		</script>
	</head>
	<body>
		<div id="box1">
			<div class="group1">A</div>
			<div class="group2">A</div>
			<div class="group1">B</div>
			<div class="group2">B</div>
			<div class="group1">C</div>
			<div class="group2">C</div>
		</div>
	</body>
~~~

##### 인접 관게 선택자 - childSelector.html

~~~html
        <script src= "jquery-3.6.0.min.js"></script>
		<script type="text/javascript">
		$(function(){ //$(document).ready(함수)의 단축 형태
			//1. <ol> 태그의 모든 자손 <li> 태그 글자색 red
			$('ol li').css('color', 'red');

			//2. <ol> 태그의 자식 <li> 태그 글자색 blue
			$('ol>li').css('color', 'blue');

			//3. 아이디가 children인 요소의 자식 <li> 태그 밑줄
			$('#children>li').css('textDecoration', 'underline');
			
			//4. 클래스가 method 요소의 모든 자손 요소의 글자색을 black
			//find() 메소드 사용
			$('.method').find('li').css('color', 'black');				

			//5. 클래스가 method 요소의 자식 요소에 속성 2개 설정
			//children() 메소드 사용
			$('.method').children('li').css({'color':'green', 'font-style':'italic'});
		});	
		</script>        		
    </head>
    <body>        
        <h3>자식/자손 선택자</h3>
        <ol>
        	<li>자손 요소의 선택 방법</li>
                <ul>
                       <li>&#36;(“선택자 선택자”)</li>
                       <li>$(“ol li”)</li>
                       <li>ol 의 자손인 모든 li 태그 선택 : 글자색(red)</li>
                </ul> 
            <li>자식 요소의 선택 방법</li>
                <ul id="children">
                   <li>$(“선택자>선택자”)</li>
                   <li>$(“ol>li”)</li>
                   <li>ol의 자식인 li 태그 선택 : 글자색(blue)</li>
                   <li>$(“ul>li”)</li>
                   <li>ul의 자식인 li 태그 선택 : 글자(underline)</li>
                </ul>               
             <li>메소드를 사용하는 방법</li>   
                 <ol class="method">
                   <li>자손 요소 선택 : find()</li>
                   	<ul>
                       <li>$(“선택자”).find(“선택자”)</li>
                       <li>$(“.method).find(“li”)</li>
                       <li>클래스 method 모든 자손 li 태그 선택 : 글자색(black)</li>
                    </ul>       
                   <li>자식 요소 선택 : children()</li>
                   	<ul>
                       <li>$(“선택자”).children(“선택자”)</li>
                       <li>$(“.method).children(“li”)</li>
                       <li>클래스 method 자식 선택 : 글자색(green)</li>
                    </ul>
                 </ol>            
        </ol>
    </body>
~~~

##### 전체, 태그, ID, 클래스 선택자 - directSelector.html

~~~html
        <script src= "jquery-3.6.0.min.js"></script>
		<script type="text/javascript">
			$(document).ready(function(){
				//1. 전체 선택자 : 문서 전체의 글자색 변경
				$("*").css("color", "red");
			
				//2. 태그 선택자 : h3 태그에 밑줄 그리기
				$('h3').css('textDecoration','underline');
					 
				//3. 태그 선택자 : h3, h4 태그에 배경색 pink 지정하기
				$('h3, h4').css('backgroundColor','pink');
				
				//4. ID 선택자 : id가 idSelector인 태그의 글자 색상을 blue/#0000ff/#00f
				//id가 jQuery인 태그의 글자 색상을 green으로 설정
				$("#idSelector").css('color','blue'); 
				$("#jQuery").css('color','green'); 
					 
				//5. 클래스 선택자 : class가 selector인 태그의 글자를 이탤릭체로,
				//class가 web인 태그의 글자를 굵게
				$(".selector").css('font-style', 'italic'); 
				$(".web").css('font-weight', 'bold');  				
			});
		</script>        
	</head>
	<body>		
        <h3>jQuery 직접 선택자 (selector)</h3>        
        <div class="selector">
            <ol>
                <li>전체 선택자</li>
                <li>태그 선택자</li>
                <li  id="idSelector">ID 선택자 </li>
                <li>클래스 선택자</li>
            </ol>
        </div>	        
        
        <h4>웹 프로그래밍</h4>
        <div class="web">
            <ol type="A">
                <li>JSP</li>
                <li>Javascript</li>
                <li  id="jQuery">jQuery</li>
                <li>Ajax</li>
            </ol>
        </div>	
	</body>
~~~