## JSP(Java Server Page)
- HTML 내에 Java 언어를 삽입한 문서
- .jsp
- Java 기반
- HTML 문서 내에 자바 코드를 삽입해서 웹 서버에서 동적으로 웹 페이지를 생성해서 클라이언트(웹 브라우저)에게 반환해 주는 언어
- 서버 사이드 스크립트 언어
- JSP를 통해 HTML과 동적으로 생성된 컨텐츠(DB 연동된 실시간 데이터)를 혼합해서 사용 가능
- Servlet을 보완한 스크립트 방식 표준 언어
- Servlet 기능 + 추가 기능
- JSP(.jsp)는 실행되면서 Servlet(.java)으로 변환되어 컴파일 되서 클래스 파일(.class) 파일로 만들어져 실행
- View를 담당하는 페이지로 사용
- 점차 JSP 페이지에서 자바 코드가 사라지고 있는 추세
- El과 JSTL로 표현

### JSP와 Servlet 차이점
- JSP : HTML 내부에 Java 소스 코드가 들어 있는 형식
  - 사용하기 편리하고 쉽다.
- Servlet : Java 코드 내에 HTML 코드가 들어 있는 형식
  - 읽고 쓰기 불편하다.

### JSP 페이지 구조
- 정적 페이지 + 동적 페이지
- 정적 페이지 구현
  - HTML 태그 사용
- 동적 페이지 구현
  - \<%@  %>
  - \<%  %>
  - \<%!  %>
  - \<%=  %>

### JSP 태그
- \<%로 시작하고 %>로 종료
  - @, !, =, -- 문자를 추가하여 태그의 의미 부여
  - 지시어 \<%@ %> : JSP 페이지의 속성 지정
  - 선언부 \<%! %> : 변수 선언 및 메소드 정의
  - 표편식 \<%= %> : 계산식, 함수 호출 결과 등 출력
  - 스크립트릿 \<% %> : 자바 코드 기술
  - 주석 \<%-- --%> : JSP 페이지에 설명 추가
  - 액션 태그 \<jsp:액션></jsp:액션> : 자바 빈, include / forward / param 등

### JSP 페이지의 기본 구성 요소
- JSP 페이지 내용
  - HTML 문서 내용 + JSP 태그 + 자바 코드
- JSP 페이지 구성
  - 지시어 : page, include, taglib
  - 스크립트 요소
    - 선언문 (Declaration)
      - JSP 페이지의 멤버 필드(변수)나 메소드를 정의할 때 사용
      - 선언문에서 선언된 변수는 페이지 전체에서 사용(전역변수의 의미)
      - 메소드 선언은 반드시 선언부에서 정의
      - 형식 : \<%! 선언 %>
      - 예 : \<%! int a = 10; %>
    - 표현식 (Expression)
      - 변수 값, 계산 결과, 메소드 호출 결과를 직접 출력하기 위해 사용
      - 형식 : \<%= 수식 %> or \<%= 변수 %>
      - 예 : \<%= 3*5 %> or \<%= name %>
    - 스크립트릿 (Scriptlet)
      - 자유롭게 자바 코드를 기술할 수 있는 영역
      - 메소드 선언은 반드시 선언부에서 정의(스크립트릿 영역에서 정의하면 오류 발생)
      - 형식 : \<% 자바코드 %>
      - 스크립트릿에서 선언된 변수는 지역변수의 개념
        - 선언된 이후부터 사용가능
  - 액션 태그

### 지시어
- JSP 페이지의 전체적인 속성을 지정할 때 사용
- JSP 컨테이너에게 전달하는 JSP 페이지 관련 메시지
- \<%@ 지시어 속성1=값, 속성2=값, … %>
- page, include, taglib 등 사용
  - __page 지시어 : \<%@ page %>__
    - JSP 페이지에 대한 속성 설정
    - language="java"
    - contentType="text/html; charset=UTF-8"
    - pageEncoding="UTF-8"
  - __include 지시어 : \<%@ include %>__
    - <%@ include file="포함될 파일의 url" %>
    - 포함시킬 파일명을 file 속성의 값으로 기술
    - (공통적으로)포함될 내용을 가진 파일을 해당 JSP 페이지 내에 삽입하는 기능 제공
    - 중첩 지정 가능
      - 한 JSP 페이지에서 다른 JSP 페이지를 포함하거나
      - 포함된 JSP 페이지가 또 다른 JSP 페이지에 중첩 포함 가능
    - 두 개의 파일이 하나의 파일로 합쳐진 후 하나의 파일로서 변환되고 컴파일
  - __taglib 지시어 : \<%@ taglib %>__
    - \<%@ taglib prefix="c" url="......" %>
    - 커스텀 태그를 JSP 페이지 내에 사용할 때 이용

#### 변수 선언 예제 - variable.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>Title</title>
  </head>
  <body>
    <%!
      // 선언문
      // 변수 선언 및 초기화만 가능
      int x = 10;
      long y;
      // y = 100; 이 경우 오류(서넌부에서는 값을 지정할 수 없음. 선언과 동시에 초기화만 가능)
      float floatValue = 3.14f;
      double doubleValue = 3.14;

      char ch = 'a';
      String myJob = "프로그래머";

      boolean b = true;
    %>
    <%
      y = 100; // 스크립트릿 영역에서 값 지정
      String name = "홍길동";
    %>
    <h3>변수 값 출력</h3>
      x : <%= x %><br>
      y : <%= y %><br>
      floatValue : <%= floatValue %><br>
      doubleValue : <%= doubleValue %><br>
      ch : <%= ch %><br>
      myJob : <%= myJob %><br>
      b : <%= b %><br>
      name : <%= name %><br>
  </body>
</html>
~~~

#### 메소드 예제 - method.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>선언문 예제 - 메소드 정의(선언)</title>
  </head>
  <body>
    <h3>선언문 예제 - 메소드 정의(선언)</h3>
    <%!
      String id = "abcd";

      public String getId() {
        return id;
      }
    %>
    id : <%= id %><br>
    getId 메소드 호출 결과 : <%= getId() %>
  </body>
</html>
~~~

#### 표현식 예제 - expression.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>선언문 예제 - 메소드 정의(선언)</title>
  </head>
  <body>
    <h3>선언문 예제 - 메소드 정의(선언)</h3>
    <%!
      String id = "abcd";
      // 메소드는 반드시 선언부에서 정의
      public String getId() {
        return id;
      }
    %>
    id : <%= id %><br>
    getId 메소드 호출 결과 : <%= getId() %>
  </body>
</html>
~~~

#### include 지시어 예제 - top.jsp, bottom.jsp, jspinclude.jsp

~~~jsp
<%@ page import="java.util.Date" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%
    Date date = new Date();
%>
<html>
    <head>
        <title>top.jsp</title>
    </head>
    <body>
        <font color='blue' size="3pt">
            top.jsp 입니다.<p>
            <%= date.toLocaleString() %>
    </body>
</html>
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>bottom.jsp</title>
    </head>
    <body>
        <font color='red' size="3pt">
            bottom.jsp 입니다.<p>
            작성자 <b> <%= name %> <b> 입니다.
            <%-- name :  선언되지 않은 변수이기 때문에 오류 발생 --%>
            <%-- 다른 페이지에 포함되어서 선언되어 있는 name 변수 사용 시 오류 없음 --%>
    </body>
</html>

~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%!
    String name = "홍길동";
%>
<html>
    <head>
        <title>include.jsp</title>
    </head>
    <body>
        <%-- top --%>
        이 부분에 top.jsp 내용이 포함될 것입니다.<p>
        <%@ include file="top.jsp" %>
        <hr>
        <%-- 본문 --%>
        <h3>본문</h3>
        이 부분은 include.jsp의 내용입니다.
        <hr>
        <%-- bottom --%>
        이 부분에 bottom.jsp 내용이 포함될 것입니다.<p>
        <%@ include file="bottom.jsp" %>
    </body>
</html>
~~~

#### include 지시어 예제2 (하나의 페이지로 합쳐지기 때문에 top과 bottom 페이지에 HTML 태그 필요 없음) - top2.jsp, bottom2.jsp, jspinclude2.jsp

~~~jsp
<%@ page import="java.util.Date" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%
    Date date = new Date();
%>
        <font color='blue' size="3pt">
            top2.jsp 입니다.<p>
            <%= date.toLocaleString() %>
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
        <font color='red' size="3pt">
            bottom2.jsp 입니다.<p>
            작성자 <b> <%= name %> <b> 입니다.
            <%-- name :  선언되지 않은 변수이기 때문에 오류 발생 --%>
            <%-- 다른 페이지에 포함되어서 선언되어 있는 name 변수 사용 시 오류 없음 --%>
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%!
    String name = "홍길동";
%>
<html>
    <head>
        <title>include.jsp</title>
    </head>
    <body>
        <%-- top --%>
        이 부분에 top2.jsp 내용이 포함될 것입니다.<p>
        <%@ include file="top2.jsp" %>
        <hr>
        <%-- 본문 --%>
        <h3>본문</h3>
        이 부분은 include2.jsp의 내용입니다.
        <hr>
        <%-- bottom --%>
        이 부분에 bottom2.jsp 내용이 포함될 것입니다.<p>
        <%@ include file="bottom2.jsp" %>
    </body>
</html>
~~~

## JSP 내장 객체
- 클라이언트에서 웹 서버에 JSP 페이지를 요청하면 자동으로 생성
- 객체 생성하지 않고 바로 사용 가능

### 내장 객체 종류
- 입출력 : request / response / out
  - request 객체 : javax.servlet.http.HttpServletRequest
    - 클라이언트(웹 브라우저)의 요청 정보를 전달하기 위한 객체
    - 주로 클라이언트에서 전송된 쿼리 문자열, 쿠키 정보, 다른 페이지에서 전송된 값에 대한 정보 등을 추출할 수 있는 메소드 제공
      - request 객체 파라미터 관련 메소드
      - 가장 많이 사용되는 중요한 메소드
        - getParameter(String name) : name에 해당하는 파라미터 값 반환 (1개 값 반환)
        - getParameterValues(String name) : name에 해당하는 모든 값을 배열로 반환
        - getParameterNames() : 모든 파라미터 이름 반환
  - response 객체 : javax.servlet.http.HttpServletResponse
    - 요청에 대한 처리 결과를 응답
    - JSP 페이지에서 처리한 결과를 웹 브라우저에게 응답할 때 사용
    - 헤더 설정,  코드 상태, 쿠키 등의 정보 포함
    - 응답 컨텐츠 설정, 응답 헤더 설정, 상태 코드 설정 등과 관련된 메소드 제공
    - request 객체 파라미터 관련 메소드
      - addCookie(Cookie) : 쿠키 지정
      - setContentType(type) : 웹 브라우저의 요청 결과로 보일 페이지의 contentType을 설정
      - sendRedirect(uri) : 페이지 이동
  - out 객체 : javax.servlet.jsp.JspWriter
    - 현재 JSP 페이지에 대한 클래스 정보
    - 웹 서버에서 웹 브라우저에게 출력 스트림으로 응답하기 위해 사용
    - out.println(“출력 문자열”);
      - 표현식(<%=  출력 문자열 %>)과 동일
- 서블릿 : page /config
- 컨텍스트 : session / application / pageContext
- 예외 처리 : exception

#### request 객체 예제 - request.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <%
            out.println("서버 : " + request.getServerName() + "<br>");
            out.println("포트 번호 : " + request.getServerPort() + "<br>");
            out.println("요청 방식 : " + request.getMethod() + "<br>");
            out.println("프로토콜 : " + request.getProtocol() + "<br>");
            out.println("URL : " + request.getRequestURL() + "<br>");
            out.println("URI : " + request.getRequestURI() + "<br>");
            out.println("ContextPath : " + request.getContextPath() + "<br>");
            out.println("ServletPath : " + request.getServletPath() + "<br>");
        %>
    </body>
</html>
~~~

#### request 객체 파라미터 관련 메소드 예제 requestForm.jsp, requestFormOk.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <meta charset="UTF-8">
    <title>회원가입 폼</title>
    <style>
        #id, #pwd { width: 100px;}
        table { margin:0 auto; width:600px; }
    </style>

</head>
<body>
<div id="wrap">
    <h3 align="center">회원 가입</h3>
    <hr>
    <form id="newMemberForm" name="newMemberForm" method="post" action="requestFormOK.jsp">
        <table>
            <tr><td> 성명</td><td><input type="text" id="name" name="name"></td></tr>
            <tr><td> ID</td><td><input type="text" id="id" name="id"></td></tr>
            <tr><td>비밀번호</td><td><input type="password" id="pwd" name="pwd"></td></tr>
            <tr><td>휴대폰 번호</td><td><input type="text" id="hp1" name="hp1" size="3">
                - <input type="text" id="hp2" name="hp2" size="4">
                - <input type="text" id="hp3" name="hp3" size="4"></td></tr>
            <tr><td>학년</td><td><input type="radio" id="year1" name="year" value="1" >1학년
                <input type="radio" id="year2" name="year" value="2">2학년
                <input type="radio" id="year3" name="year" value="3">3학년
                <input type="radio" id="year4" name="year" value="4">4학년</td></tr>
            <tr><td>관심분야</td>
                <td><input type="checkbox"  id="web" name="interest" value="웹 프로그래밍">웹 프로그래밍
                    <input type="checkbox"  id="design" name="interest" value="파이썬">파이썬
                    <input type="checkbox"  id="bigdata" name="interest" value="빅데이터">빅데이터
                    <input type="checkbox"  id="java" name="interest" value="자바">자바 프로그래밍</td></tr>
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
</html>
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>request 객체 관련 메소드 예제</title>
  </head>
  <body>
    <%!
    // 선언부에 변수 선언(스크립트릿에 변수 선언해도 됨)
      String name, id, pwd, hp1, hp2, hp3, year, department;
      String[] interest;
    %>
    <%
      // 스크립트릿 영역
      // 폼에서  전송된 데이터 받아서 변수에 저장
      request.setCharacterEncoding("utf-8");
      name = request.getParameter("name");
      id = request.getParameter("id");
      pwd = request.getParameter("pwd");
      hp1 = request.getParameter("hp1");
      hp2 = request.getParameter("hp2");
      hp3 = request.getParameter("hp3");
      year = request.getParameter("year");
      interest = request.getParameterValues("interest");
      department = request.getParameter("department");
    %>
<%--  변수에 저장된 값 출력  --%>
<%--  배열은 for문 사용해서 각 요소에 반복하여 출력  --%>
    이름 : <%= name %><br>
    아이디 : <%= id %><br>
    비밀번호 : <%= pwd %><br>
    전화번호 : <%= hp1 + "-" + hp2 + "-" + hp3 %><br>
    학년 : <%= year %><br>
    관심분야 : <%
                for(int i = 0; i < interest.length; i++) {
                        %>
                        <%= interest[i] + " "%>
                <%
                        }
                %><br>
    학과 : <%= department %><br>
  </body>
</html>
~~~

#### response 객체 예제 -response.jsp, responseOK.jsp, pass.jsp, fail.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>Title</title>
  </head>
  <body>
    <form method="post" action="responseOK.jsp">
      대한민국의 수도는?
      <input type="text" name="answer" size="10">
      <input type="submit" value="전송">
    </form>
  </body>
</html>
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <%
            request.setCharacterEncoding("utf-8");
            String answer = request.getParameter("answer");

            // 서울이면 pass.jsp
            if(answer.equals("서울")) {
                response.sendRedirect("pass.jsp");
            }
            else {
                response.sendRedirect("fail.jsp");
            }
            // 아니면 fail.jsp
        %>
    </body>
</html>
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>Title</title>
  </head>
  <body>
    <h1>정답입니다.</h1>
  </body>
</html>
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <h1>오답입니다. 대한민국의 수도는 서울 입니다.</h1>
    </body>
</html>
~~~

### 전송되는 데이터의 타입
- 모두 문자열
  - String answer = request.getParameter("answer");
- 숫자 연산을 할 경우 숫자형으로 형변환 필요
  - Integer.parseInt(문자열 변수)
  - Integer.parseInt(answer)
  - int a = Integer.parseInt(request.getParameter("answer"))

#### 타입 변환 예제 - typeConversion.jsp, typeConversionOK.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>Title</title>
  </head>
  <body>
    <form method="post" action="typeConversionOK.jsp">
      가로 길이 : <input type="text" name="width" size="10"> <br>
      세로 길이 : <input type="text" name="height" size="10"> <br>
      <input type="submit" value="계산">
    </form>
  </body>
</html>
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>Title</title>
  </head>
  <body>
   <%
       String width = request.getParameter("width");
       String height = request.getParameter("height");
       int area = Integer.parseInt(width) * Integer.parseInt(height);
       out.print("<h1>넓이는 " + area + "m^2 입니다.</h1>");
   %>
  </body>
</html>
~~~

### JSP 제어문(Java와 동일)
- if문
- for문
- while문

#### for문 연습문제 구구단 출력 - forFomr.jsp, forResult.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <form method="post" action="forFormOK.jsp">
            출력할 구구단 단수 입력
            <input type="text" name="num" size="10">
            <input type="submit" value="출력">
        </form>
    </body>
</html>
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>Title</title>
  </head>
  <body>
    <%
        int num = Integer.parseInt(request.getParameter("num"));
        out.print("<table border=1>");
        out.print("<th>" + num + "단</th>");
        for(int i = 1; i < 10; i++) {
            out.print("<tr>" +
                    "<td>" + num  + " * " + i  + num*i + "</td>" +
                    "</tr>");
        }
        out.print("</table>");
    %>
  </body>
</html>
~~~

## 액션 태그
- JSP 페이지 내에서 어떤 동작을 지시하는 태그
- 기능 
  - 어떤 동작 또는 액션이 일어나는 시점에 페이지와 페이지 사이에서의 제어 이동
  - 다른 페이지의 실행 결과를 현재 페이지에 포함
- 종류
  - include
  - forward
  - useBean
  - setProperty
  - getProperty

### include 액션태그 : \<jsp:include>
- 다른 페이지의 실행 결과를 현재 페이지에 포함시킬 때 사용
- 페이지를 모듈화 할 때 사용
- \<jsp:include page="포함될 페이지" flush="ture" />
  - page 속성 : 결과가 포함될 페이지명
  - flust 속성 : 포함될 페이지로 이동될 때 현재 포함하는 페이지가 지금까지 출력 버퍼에 저장한 결과를 처리하는 방법을 결정
    - true : 현재 페이지가 지금까지 버퍼에 저장한 내용 웹 브라우저에 출력하고 버퍼를 비움
- include 액션태그와 include 지시어의 차이
  - 형식
    - 액션태그 : \<jsp:include page="포함될 페이지" />
    - 지시어 : \<%@ include file="포함될 페이지" %>
  - 처리 시점
    - 액션태그 : 실행 시
    - 지시어 : 자바 소스로 변환 시
  - 기능
    - 액션태그 : 별도의 파일로 처리, 제어권이 이동했다가 다시 돌아옴
    - 지시어 : 현재 파일에 삽ㅇ비(합쳐서 하나의 java 파일 생성)
  - 데이터 구성
    - 액션태그 : 동적 데이터로 구성
    - 지시어 : 정적 데이터로 구성
  - 용도
    - 액션태그 : 화면 레이아웃 모듈화 할 때
    - 지시어 : 여러 페이지에서 사용하는 변수를 지정하고 include 시킴

## 사진

#### include 액션 태그 예제 - includeAction1.jsp, includeAction2.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>includeAction1</title>
    </head>
    <body>
        <h3>includeAction1.jsp 입니다</h3>
        <hr>
        <jsp:include page="includeAction2.jsp" flush="true"/>
    </body>
</html>
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>includeAction2</title>
  </head>
  <body>
    <h3>includeAction2.jsp 입니다</h3>
  </body>
</html>
~~~

### forward 액션 태그 : \<jsp:forward>
- 현재 페이지에서 다른 특정 페이지로 전환
- 웹 페이지 간의 제어를 이동시킬 때 사용
- \<jsp:forward page=”포워딩할 JSP 페이지”>

#### forward 액션 태그 예제 - login.jsp, loginResult.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>login</title>
    </head>
    <body>
<%--        <%--%>
<%--            String user_id = request.getParameter("user_id");--%>
<%--            // 값이 null인경우 출력은 되지만 null로 무언가 하려고 하면 NullPointerException 출력--%>
<%--        %>--%>
<%--        <%= user_id %>--%>
        <%
            String user_id = request.getParameter("user_id");
            if(user_id == null) {
        %>
        <h2 name="h2login">로그인</h2>
        <%
            } else {
        %>
        <h2>아이디를 입력하지 않았습니다. 아이디를 입력해 주세요.</h2>
        <%
            }
        %>
        <form name="frmLogin" method="post" action="loginResult.jsp" >
        아이디  :<input type="text" name="user_id"><br>
        비밀번호:<input type="password" name="user_pw" ><br>
        <input type="submit" value="로그인">  <input type="reset" value="다시입력">
        </form>
    </body>
</html>
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <%
            request.setCharacterEncoding("utf-8");
            // 아이디를 입력하지 않았으면 login.jsp 페이지로 포워딩
            String user_id = request.getParameter("user_id");
            if(user_id.length() == 0) {
        %>
        <jsp:forward page="login.jsp"/>
        <%
            }
        %>
    <h2>환영합니다 <%= user_id%> 님!</h2>
    </body>
</html>

~~~


### param 액션 태그 : \<jsp:param>
- 이동하는 페이지에 파라미터 값을 전달할 때 사용
- forward  및 include 액션 태그에서 데이터를 전달하기 위해 사용
- name과 value로 구성
  - \<jsp:param name="id" value="abcd" />
  - 받을 때
    - request.getParameter("id");

#### forward 액션 태그 예제 - paramLogin.jsp, paramLoginResult.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>paramLogin</title>
    </head>
    <body>
        <%
            request.setCharacterEncoding("utf-8");
            String msg = request.getParameter("msg");
            if(msg == null) {
        %>
            <h3>로그인</h3>
        <%
            } else {
        %>
            <h3><%= msg %></h3>
        <%
            }
        %>
        <form name="frmLogin" method="post" action="paramLoginResult.jsp" >
            아이디  :<input type="text" name="user_id"><br>
            비밀번호:<input type="password" name="user_pw" ><br>
            <input type="submit" value="로그인">  <input type="reset" value="다시입력">
        </form>
    </body>
</html>
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>paramLoginResult</title>
  </head>
  <body>
    <%
        request.setCharacterEncoding("utf-8");
        String msg = "아이디를 입력하지 않았습니다. 아이디를 입력해 주세요.";
        String user_id = request.getParameter("user_id");
        //  user_id 값이 비었으면 paramLogin.jsp로 포워딩 (msg 전송)
        if(user_id.length() == 0) {
    %>
    <jsp:forward page="paramLogin.jsp">
        <jsp:param name="msg" value="<%= msg %>"/>
    </jsp:forward>
    <%
        }
    %>

    <h3>환영합니다. <%= user_id %> 님!</h3>
  </body>
</html>
~~~

## 자바 빈 관련 액션 태그

### useBean 액션 태그 : \<jsp:useBean>
- 자바 빈(JavaBeans)
  - DTO / VO와 같은 개념
  - 데이터를 다루기 위해 자바로 작성되는 소프트웨어 컴포넌트로 재사용 가능
  - 입력 폼의 데이터와 데이터베이스의 데이터 처리 부분에서 활용
  - 클래스로 만들어짐
    - 멤버 필드(변수)로 속성(Property)이 있고
    - 멤버 메소드로 Getter / Setter 메소드 포함
    - setXXX() : 프로퍼티에 값 저장
    - getXXX() : 프로퍼티 값 반환
  - 속성 접근 제이자는 private
  - Getter / Setter 메소드와 클래스는 public
- 자바 빈을 JSP 페이지에서 사용할 때 사용
- \<jsp:useBean id="빈 이름" class="클래스" scope="유효범위" />
  - \<jsp:useBean id="student" class="sec01.StudentBean" scope="page" />
  - id : 자바빈 이름
  - class : 패키지명을 포함한 클래스 이름
  - scope : 자바빈의 유효 범위
    - page : 생성된 페이지 내에서만 사용 가능. (디폴트)
    - request : 요청이 수행되는 페이지에서만 사용 가능
    - session : 객체가 생성된 세션에서 수행되는 페이지에서 사용 웹 브라우저의 생명주기와 동일하게 사용 가능
    - application : 객체가 생성된 애플리케이션에 포함된 페이지에서 사용 웹 애플리케이션 생명주기와 동일하게 사용 가능

### setProperty 액션 태그 : \<jsp:setProperty>
- 프로퍼티(변수) 값을 세팅할 때 사용 (setter)
- 데이터 저장
- \<jsp:setProperty name=”빈 이름” property=”속성이름” value=”속성값” />
  - \<jsp:setProperty name=”student” property=stdNo value=2021001 />

### getProperty 액션 태그 : \<jsp:getProperty>
- 프로퍼티(변수) 값을 얻어올 때 사용 (getter)
- \<jsp:getProperty name=”빈 이름” property=”속성이름”>
  - <jsp:getProperty name=”student” property=”stdNo”>

#### 자바 빈 액션 태그 예제 - StudentBean.java, studentBean.jsp
- 빈 클래스 : StudentBean.java  (DTO/VO와 동일)
  - Getters / Setters
- studentBean.jsp
  - useBean 액션 태그
  - setProperty 액션 태그
  - getProperty 액션 태그

~~~java
package main;

public class StudentBean {
    private String stdNo;
    private String stdName;
    private String stdPhone;
    private String stdAddress;
    private String stdYear;

    public String getStdNo() { 
        return stdNo; 
    }
    public void setStdNo(String stdNo) {
        this.stdNo = stdNo;
    }
    public String getStdName() {
        return stdName;
    }
    public void setStdName(String stdName) {
        this.stdName = stdName;
    }
    public String getStdPhone() {
        return stdPhone;
    }
    public void setStdPhone(String stdPhone) {
        this.stdPhone = stdPhone;
    }
    public String getStdAddress() {
        return stdAddress;
    }
    public void setStdAddress(String stdAddress) { 
        this.stdAddress = stdAddress; 
        }
    public String getStdYear() {
        return stdYear;
    }
    public void setStdYear(String stdYear) {
        this.stdYear = stdYear;
    }
}
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<jsp:useBean id="student" class="main.StudentBean" scope="page"></jsp:useBean>
<html>
  <head>
      <title>자바 빈 액션 태그</title>
  </head>
  <body>
    <h3>빈 속성 값 설정(setProperty)</h3>
    <jsp:setProperty name="student" property="stdNo" value="2021001" />
    <jsp:setProperty name="student" property="stdName" value="홍길동" />
    <jsp:setProperty name="student" property="stdPhone" value="010-1111-1111" />
    <jsp:setProperty name="student" property="stdAddress" value="서울시 종로구" />
    <jsp:setProperty name="student" property="stdYear" value="4" />

    <h3>빈 속성 값 출력(getProperty)</h3>
    학번 : <jsp:getProperty name="student" property="stdNo"/> <br>
    이름 : <jsp:getProperty name="student" property="stdName"/> <br>
    연락처 : <jsp:getProperty name="student" property="stdPhone"/> <br>
    주소 : <jsp:getProperty name="student" property="stdAddress"/> <br>
    학년 : <jsp:getProperty name="student" property="stdYear"/>

    <h3>빈 속성 값 출력(Getter 사용)</h3>
    학번 : <%= student.getStdNo() %> <br>
    이름 : <%= student.getStdName() %> <br>
    연락처 : <%= student.getStdPhone() %> <br>
    주소 : <%= student.getStdAddress() %> <br>
    학년 : <%= student.getStdYear() %> <br>
  </body>
</html>
~~~