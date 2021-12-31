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

#### 자바 빈 액션 태그 예제2 - studentForm.jsp, newStudentOk.jsp
- 폼에서 입력한 값으로 setProperty 액션 태그를 사용해서 한꺼번에 값을 설정하는 예제
- 전 예제에서 사용했던 StudentBean.java 사용

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>Title</title>
  </head>
  <body>
      <h3>학생 정보 등록</h3>
      <form name="frmStudent" method="post" action="newStudentOk.jsp" >
          <table>
              <tr><td>학번</td><td><input type="text" name="stdNo"></td></tr>
              <tr><td>성명</td><td><input type="text" name="stdName" ></td></tr>
              <tr><td>전화번호</td><td><input type="text" name="stdPhone" ></td></tr>
              <tr><td>주소</td><td><input type="text" name="stdAddress" ></td></tr>
              <tr><td>학년</td>
                  <td><input type="radio" name="stdYear" value="1">1학년
                      <input type="radio" name="stdYear" value="2">2학년
                      <input type="radio" name="stdYear" value="3">3학년
                      <input type="radio" name="stdYear" value="4">4학년</td></tr>
              <tr><td colspan="2"> <input type="submit" value="등록">
                  <input type="reset" value="다시입력"></td></tr>
          </table>
      </form>
  </body>
</html>
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>폼에 입력한 값으로 빈 속성값 한번에 설정</title>
  </head>
  <body>
    <%
        request.setCharacterEncoding("utf-8");

    %>
<%--  StudentBean 사용 / 모든 프로퍼티에 값 설정--%>
    <jsp:useBean id="student" class="main.StudentBean" scope="page">
        <jsp:setProperty name="student" property="*" />
    </jsp:useBean>
<%--  앞에 Form 태그 안의 input태그에서 name 속성값과 StudentBean 클래스의 멤버 필드 명이 동일해야 함--%>
  <h3>학생 정보 출력(Bean 속성 값 출력)</h3>
    학번 : <%= student.getStdNo() %> <br>
    이름 : <%= student.getStdName() %> <br>
    연락처 : <%= student.getStdPhone() %> <br>
    주소 : <%= student.getStdAddress() %> <br>
    학년 : <%= student.getStdYear() %> <br>
  </body>
</html>
~~~

## 표현 언어 : EL(Expression Language)
- JSP 발전 과정
  - 초기 : HTML 태그 중심으로 자바를 이용해서 화면 구현
    - JSP 구성 내용 : HTML + JSP 태그 + 자바 코드
    - 화면에 대한 요구 사항이 복잡해지며 자바 코드를 대체하는 액션태그가 등장
    - 복잡한 자바 코드를 제거하는 방향으로 발전
      - 복잡한 자바 코드로 인해 화면 작업이 어려움
      - 프론트엔드 개발자와 백엔드 개발자 분리
  - 현재 : JSP 페이지는 JSP 태그의 스크립트 요소보다 표현 언어와 JSTL을 사용

### EL(Expression Language)
- 표현 언어
- 자바 코드가 들어가 표현식을 좀 더 편리하게 사용하기 위해 JSP 2.0부터 도입된 데이터 출력 기능
- 표현식 또는 액션태그 대신 값을 표현
- \<%= 값 %> => ${값}
- attribute 또는 parameter 등을 JSP 파일에서 출력할 용도로 사용
  - attribute : ${attribute 이름}
  - parameter : ${param.이름} 또는 ${paramValue[인덱스]}

### EL 연산자
- 산술 연산자 : +, -, *, / %, (div, mod)
- 관계 연산자 : >, >=, <, <=, ==, !=
  - (gt, ge, lt, le, eq, ne)
- 논리 연산자 : &&, ||, !, (and, or, not)
- 조건 연산자 : 수식 ? 참일 때 값 : 거짓일 때 값
- empty 연산자 : 값이 null 이거나 길이가 0이면 참 (true)
  - ${empty 변수} : 변수가 null 이거나 0이면 참
  - ${not empty 변수} : 변수가 null이 아니거나 0이 아니면 참

#### EL을 액션 태그로 사용 예제 - el2.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<jsp:useBean id="student" class="main.StudentBean" scope="page">
    <jsp:setProperty name="student" property="stdName" value="홍길동" />
</jsp:useBean>
<html>
  <head>
      <title>Title</title>
  </head>
  <body>
    <jsp:getProperty name="student" property="stdName" />
    ${student.stdName}
  </body>
</html>
~~~

### EL 내장 객체
- Scope
  - pageScope : page 객체 참조
  - requestScope :  request 객체 참조
  - sessionScope :  session 객체 참조
  - applicationScope : application 객체 참조
- 요청 파라미터
  - param : 요청 파라미터 참조
  - paramValues : 요청 파라미터(배열) 참조
- 쿠키 값
  - Cookis : cookie 객체 참조
- JSP 내용
  - pageContext : pageContext 객체 참조(페이지 정보)
- 초기 파라미터
  - initParam : web.xml의 context 초기화 파라미터 참조

#### param 내장 객체 예제 - studentForm2.jsp, newStudentOk2.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>Title</title>
  </head>
  <body>
      <h3>학생 정보 등록</h3>
      <form name="frmStudent" method="post" action="newStudentOk2.jsp" >
          <table>
              <tr><td>학번</td><td><input type="text" name="stdNo"></td></tr>
              <tr><td>성명</td><td><input type="text" name="stdName" ></td></tr>
              <tr><td>전화번호</td><td><input type="text" name="stdPhone" ></td></tr>
              <tr><td>주소</td><td><input type="text" name="stdAddress" ></td></tr>
              <tr><td>학년</td>
                  <td><input type="radio" name="stdYear" value="1">1학년
                      <input type="radio" name="stdYear" value="2">2학년
                      <input type="radio" name="stdYear" value="3">3학년
                      <input type="radio" name="stdYear" value="4">4학년</td></tr>
              <tr><td colspan="2"> <input type="submit" value="등록">
                  <input type="reset" value="다시입력"></td></tr>
          </table>
      </form>
  </body>
</html>
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>폼에 입력한 값으로 빈 속성값 한번에 설정</title>
  </head>
  <body>
    <%
        request.setCharacterEncoding("utf-8");
    %>
    <h3>학생 정보 출력(EL param 객체 사용)</h3><br>
        학번 : ${param.stdNo} <br>
        성명 : ${param.stdName} <br>
        전화번호 : ${param.stdPhone} <br>
        주소 : ${param.stdAddress} <br>
        학년 : ${param.stdYear} <br>
  </body>
</html>
~~~

### pageContext 내장 객체
- 컨텍스트 이름(프로젝트명) 가져오기
- getContextPath() 메소드 이용해서 컨텍스트 이름 가져오기 했던 것을 pageContext 내장 객체 사용 해서 컨텍스트 이름 가져올 수 있음
- \<a href=”/JSP01/sec01/login.jsp”>로그인\</a>
- \<a href=”<%=request.getContextPath()%>/sec01/login.jsp”>로그인\</a>
- \<a href=”${pageContext.request.contextPath}/sec01/login.jsp”>로그인\</a>

#### pageContext 내장 객체 예제 로그인 페이지로 이동(4가지 방법) - newStudentOk2.jsp
- url 사용 : “http://localhost:8080/JSP01/sec01/login.jsp”
- \<a>에서  ContextPath + ServletPath (URI) 사용
  - ”/JSP01/sec01/login.jsp”
- getContextPath() 메소드 이용
  - request.getContextPath()
- pageContext 내장 객체 사용
  - ${pageContext.request.contextPath}

### EL (표현 언어)로 바인딩 속성 출력하기
- request, session, application 내장 객체에 속성을 바인딩한 후 다른 서블릿이나 JSP에 전달 가능
- 자바 코드 사용하지 않고 바인딩된 속성 이름으로 바로 값 출력
- request.setAttribute("id", "hong");
- 서블릿 : getAttribute("id") 해서 값 가져와서 사용
- EL : ${id}

#### EL (표현 언어)로 바인딩 속성 출력하기 예제 - el-forward.jsp, el-forward-result.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <%
            request.setAttribute("id", "Hong");
            request.setAttribute("pwd", "1234");
            request.setAttribute("name", "홍길동");
            request.setAttribute("email", "Hong@test.com");
        %>
        <jsp:forward page="el-forward-result.jsp" />
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
        %>
        id : ${id }<br>
        pwd : ${pwd }<br>
        name : ${name }<br>
        email : ${email }<br>
    </body>
</html>
~~~

### 빈 객체 바인딩
- StudentBean 사용
  - StudentBean student = new StudentBean(생성자로 초기화);
  - requset.setAttribute("student", student);
  - ${student.stdNo}

#### 빈 객체 바인딩 예제 - el-forward2.jsp, el-forward-result2.jsp

~~~jsp
<%@ page import="main.StudentBean" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>Title</title>
  </head>
  <body>
    <%
        StudentBean student = new StudentBean("2001003", "이몽룡", "010", "서울시 강남구", "4학년");
        request.setAttribute("student", student);
    %>
  <jsp:forward page="el-forward-result2.jsp" />
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
    학번 : ${student.stdNo } <br>
    성명 : ${student.stdName } <br>
    전화번호 : ${student.stdPhone} <br>
    주소 : ${student.stdAddress } <br>
    학년 : ${student.stdYear } <br>
    </body>
</html>
~~~

#### 빈 객체 바인딩 예제 ArrayList - el-forward3.jsp, el-forward-result3.jsp

~~~jsp
<%@ page import="main.StudentBean" %>
<%@ page import="java.util.ArrayList" %>
<%@ page import="java.util.List" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <%
            StudentBean student1 = new StudentBean("2001003", "이몽룡", "010", "서울시 강남구", "4학년");
            StudentBean student2 = new StudentBean("2001001", "홍길동", "010", "서울시 강남구", "3학년");
            StudentBean student3 = new StudentBean("2001002", "성춘향", "010", "서울시 강남구", "2학년");

            List studentList = new ArrayList();
            studentList.add(student1);
            studentList.add(student2);
            studentList.add(student3);

            request.setAttribute("stdList", studentList);
        %>
        <jsp:forward page="el-forward-result3.jsp" />
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
<!--        바인딩된 ArrayList에서 인덱스 사용하여 데이터 출력-->
    <table border="1">
        <tr><th>학번</th><th>성명</th><th>전화</th><th>주소</th><th>학년</th></tr>
        <tr><td>${stdList[0].stdNo}</td><td>${stdList[0].stdName}</td><td>${stdList[0].stdPhone}</td><td>${stdList[0].stdAddress}</td><td>${stdList[0].stdYear}</td></tr>
        <tr><td>${stdList[1].stdNo}</td><td>${stdList[1].stdName}</td><td>${stdList[1].stdPhone}</td><td>${stdList[1].stdAddress}</td><td>${stdList[1].stdYear}</td></tr>
        <tr><td>${stdList[2].stdNo}</td><td>${stdList[2].stdName}</td><td>${stdList[2].stdPhone}</td><td>${stdList[2].stdAddress}</td><td>${stdList[2].stdYear}</td></tr>
    </table>
    </body>
</html>
~~~

### scope : 스코프 우선순위
- request, session, application 내장 객체에서는 데이터를 바인딩해서 다른 JSP 페이지로 전달
- 각 내장 객체에 바인딩되는 속성 이름이 같은 경우 각 내장 객체에 지정된 출력 우선순위에 따라 순서대로 속성에 접근
  - 높음 page < request < session < application 낮음
- pageScope : 현재 페이지 영역의 변수
- requestScope : 이전 페이지에서 받아온 영역의 변수
- sessionScope : session 영역의 변수
- applicationScope : application 영역의 변수

#### 스코프 우선순위 예제 - scope-priority.jsp, scope-priority-result.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>Title</title>
  </head>
  <body>
    <%
      // request -> session -> application
      session.setAttribute("name", "세션");
      request.setAttribute("name", "request");
      application.setAttribute("name", "애플리케이션");
    %>
  <jsp:forward page="scope-priority-result.jsp" />
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
        <h3>누가 더 높나?</h3><br>
        scope : ${name}
    </body>
</html>
~~~

=============================================================================

## JSTL (JSP Standard Tag Library)
- JSP 표준 태그 라이브러리
- \<%@ taglib prefix="c" uri="http:....." %>
- JSP와 HTML을 같이 사용함으로서 가독성이 떨어지는 것을 보완하고자 만들어진 태그 라이브러리
- JSP 페이지 내에서 자바 코드를 사용하지 않고 태그를 사용하도록 함
- JSP 페이지의 로직을 담당하는 부분인 제어문 및 데이터베이스 처리 등을 표준 커스텀 태그로 제공

### JSTL 라이브러리 구성
- Core (코어)
  - URI : http://java.sun.com.jsp/jstl/core
  - Prefix : c
  - 제공 기능
    - 변수 선언 및 삭제 등 변수와 관련된 작업
    - if, for 문 등과 같은 제어문
    - URL 처리 및 그 밖의 예외처리 및 화면 출력
  - 변수 지원 
    - \<c:set>
      - 변수 지정
      - setAttribute()와 같은 역할
    - \<c:remove>
      - 지정된 변수 제거
  - 흐름 제어
    - \<c:if> : 조건문
    - \<c:choose>
      - switch문에 해당
      - \<c:when>, \<c:otherwise>  서브 태그
    - \<c:forEach> : 반복문
    - \<c:forTokens> : 구분자로 분리된 각 토큰 처리
  - URL 처리
    - \<c:import> : 다른 자원 추가
    - \<c:redirect> : sendRedirect() 기능
    - \<c:rul> : url 생성 (페이지 이동)
  - 기타
    - \<c:catch> : 예외 처리
    - \<c:out> : 출력

#### \<c:set> 태그 : 변수 선언 예제 - c_set.jsp

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!--  변수 설정 -->
<c:set var="id" value="hong" scope="page" />
<c:set var="pwd" value="1234" scope="page" />
<c:set var="name" value="${'홍길동' }" scope="page" />
<c:set var="age" value="${20 }" scope="page" />
<!--  value 값으로 EL 사용해도 됨 -->

<c:set var="contextPath" value="${pageContext.request.contextPath }" />
<!-- 복잡한 속셩명을 짧게 줄여서 사용 -->

<html>
	<head>
		<meta charset="UTF-8">
		<title>c:set 태그</title>
	</head>
	<body>
		${id } <br>
		${pwd } <br>
		${name } <br>
		${age } <br><br>
		
		<a href="${contextPath}/login.jsp">로그인</a>
	</body>
</html>
~~~

#### \<c:if> 태그 : 조건문 (else문 없을 경우의 if문) - c_if.jsp

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!--  변수 설정 -->
<c:set var="id" value="hong2" scope="page" />
<c:set var="pwd" value="1234" scope="page" />
<c:set var="name" value="${'홍길동' }" scope="page" />
<c:set var="age" value="${20 }" scope="page" />
<c:set var="height" value="${170 }" scope="page" />

<html>
	<head>
		<meta charset="UTF-8">
		<title>c:if 태그</title>
	</head>
	<body>
		<c:if test="${true }">
			<h3>항상 참입니다</h3>
		</c:if>
		<c:if test="${(id=='hong') && (name=='홍길동')}">
			<h3>아이디는 ${id }이고, 이름은 ${name }입니다</h3>
		</c:if>
	</body>
</html>
~~~

#### \<c:choose> 태그 : switch문 기능 - c_choose.jsp

~~~jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<c:set var="id" value="hong" scope="page" />
<c:set var="pwd" value="1234" scope="page" />
<c:set var="name" value="${'홍길동'}" scope="page" />
<c:set var="age" value="${20}" scope="page" />
<c:set var="height" value="${170}" scope="page" />
<html>
  <head>
      <title>Title</title>
  </head>
  <body>
    <table border="1" align="center">
      <tr align="center" bgcolor="#90ee90">
        <td width="7%">아이디</td>
        <td width="7%">비밀번호</td>
        <td width="7%">이름</td>
        <td width="7%">나이</td>
        <td width="7%">키</td>
        <c:choose>
          <c:when test="${empty name}">
            <tr align="center"><td colspan="5">이름이 없습니다.</td></tr>
          </c:when>
          <c:otherwise>
            <tr align="center">
              <td>${id}</td>
              <td>${pwd}</td>
              <td>${name}</td>
              <td>${age}</td>
              <td>${height}</td>
            </tr>
          </c:otherwise>
        </c:choose>
      </tr>
    </table>
  </body>
</html>
~~~

#### \<c:forEach> 태그 : 반복문 수행 예제 - c_forEach.jsp
- \<c:forEach var=”변수명 items=”반복할 객체명” begin=”시작값” end=”마지막값” step=”증가값” varStatus=”반복상태변수명”>
- \</c:forEach>
- varStatus : 반복 상태 속성 지정
  - index : 인덱스 번호 반환 (일반적으로 0부터 시작. begin 값을 1로 설정하면 인덱스도 1부터 시작)
  - count : 몇 번째 반복인지 숫자 반환
  - first: 첫 번째 여부 (boolean 값 반환)
  - last : 마지막 여부(boolean 값 반환)

~~~jsp
<%@ page import="java.util.ArrayList" %>
<%@ page import="java.util.List" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%
  List dataList = new ArrayList();
  dataList.add("hello");
  dataList.add("world");
  dataList.add("안녕하세요");
%>
<html>
  <head>
      <title>Title</title>
  </head>
  <body>
    <c:forEach var="i" begin="1" end="10" step="1" varStatus="loop">
      i = ${i} &nbsp;&nbsp; 반복회수 : ${loop.count}
      &nbsp;&nbsp; 인덱스 : ${loop.index}
      &nbsp;&nbsp; 첫 번째 : ${loop.first}
      &nbsp;&nbsp; 마지막 : ${loop.last} <br>
    </c:forEach> <br>

    <c:set var="list" value="${dataList}" />
    <c:forEach var="data" items="${list}">
      ${data} <br>
    </c:forEach>

    <c:set var="fruits" value="사과, 수박, 바나나, 망고, 귤" />
    <c:forTokens items="${fruits}" delims="," var="token">
      ${fruits} <br>
    </c:forTokens>
  </body>
</html>
~~~

### \<c:url> 태그 
- \<c:url var=”변수명” value=”url경로” [scope] />
- \<c:url var="url1" value="/sec01/login.jsp" />
  - /가 있어서야   ContextPath (/JSP01)부터 찾음
  - / 없는 경우 :  현재 페이지가 들어 있는 sec02부터 찾음
    - <c:url var="url1" value="sec01/login.jsp" />
    - /JSP01/sec02/sec01/login.jsp

~~~jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<c:url var="url1" value="login.jsp" />
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <a href="${url1}">로그인 화면으로 이동</a>
    </body>
</html>
~~~

### \<c:redirect> 태그 
- response.sendRedirect() 기능
- 매개변수 전달 가능

~~~jsp
<c:redirect url=”redirect할 url”>
<c:param name=”id” value=”${‘hong’}” />
</c:redirect>
~~~

#### \<c:redirect> 태그 예제 - c_redirect.jsp, c_redirect_result.jsp

~~~jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <c:redirect url="c_redirect_result.jsp">
            <c:param name="name" value="${'HongGilDong'}"/>
            <c:param name="email" value="${'hong@test.com'}"/>
        </c:redirect>
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
    <h3>redirect 할 때 전달된 param 받기</h3>
    성명 : ${param.name} <br>
    이메일 : ${param.email}
  </body>
</html>
~~~

### 포매팅 태그 라이브러리
- 숫자, 날짜, 통화 관련 포매팅 태그 라이브러리
- \<fmt:formatDate>
- \<fmt:formatNumber>
- \<fmt:timeZone>

#### 포매팅 예제 - format_taglib.jsp

~~~jsp
<%@ page import="java.util.Date" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h3>formatNumber</h3>
    <c:set var="price" value="100000000"/>
    <fmt:formatNumber type="number" value="${price}" var="priceNumber"/>
    일반 숫자로 표현 : ${priceNumber}<br>
    통화로 표현 : <fmt:formatNumber type="currency" value="${price}" currencySymbol="$" /><br>
<!--천 단위 구분 표시 : groupingUsed="ture" or "false" (default : true)-->
    퍼센트로 포현 : <fmt:formatNumber type="percent" value="${price}" groupingUsed="true" /><br>
    <h3>formatDate</h3>
    <c:set var="now" value="<%= new Date()%>" />
    일반 날짜로 표현 : ${now} <br>
    포매팅 스타일없이 : <fmt:formatDate value="${now}" type="date" /> <br>
    포매팅 full : <fmt:formatDate value="${now}" type="date" dateStyle="full" /> <br>
    포매팅 short : <fmt:formatDate value="${now}" type="date" dateStyle="short" /> <br>
    포매팅 type:time : <fmt:formatDate value="${now}" type="time" /> <br>
    포매팅 type:both : <fmt:formatDate value="${now}" type="both" /> <br>
    포매팅 type:both dateStyle:full timeStyle:full : <fmt:formatDate value="${now}" type="both" dateStyle="full" timeStyle="full" /> <br>
    패턴 yyyy-MM-dd hh:mm:ss <fmt:formatDate value="${now}" pattern="yyyy-MM-dd hh:mm:ss" /> <br>

    한국 현재 시간 : <fmt:formatDate value="${now}" type="both" dateStyle="full" timeStyle="full" /> <br>
    뉴욕 현재 시간 : <fmt:formatDate value="${now}" timeZone="GMT-5" type="both" dateStyle="full" timeStyle="full" />
</body>
</html>
~~~

### 문자열 처리 함수
- 함수 기능 태그 라이브러리
- \<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions" %>

#### 함수 기능 태그 라이브러리 - fn_string.jsp

~~~jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>Title</title>
  </head>
  <body>
    <c:set var="title1" value="hello world" />
    <c:set var="title2" value="쇼핑몰 중심 JSP 입니다" />
    <c:set var="str" value="중심" />
    title1 : ${title1} <br>
    title2 : ${title2} <br>
    str : ${str} <br>

  ${title1}의 문자열 길이 : ${fn:length(title1)} <br>
  title1 3 ~ 5 번째 문자열 추출 : ${fn:substring(title1, 2, 5)} <br>
  공백을 /로 변환 : ${fn:replace(title1, " ", "/")}<br>
  title1에 '중심' 단어 포함 여부 : ${fn:contains(title1, str)}<br>
  title2에 '중심' 단어 포함 여부 : ${fn:contains(title2, str)}<br>
  </body>
</html>
~~~