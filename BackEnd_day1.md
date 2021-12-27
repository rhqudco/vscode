## 웹(Web) 개념
- 웹 서비스
  - 인터넷을 기반으로 제공되는 서비스
- 웹 애플리케이션
  - 웹을 기반으로 작동되는 프로그램
  - 웹 프로그래밍을 통해 구현
- 퓁 프로그래밍
  - 기본적으로 클라이언트 / 서버 방식
  - 정적인 HTML만으로는 데이터가 실시간으로 변화하는 것을 처리하거나 저장하기에는 불가능
  - 동적으로 변화하는 데이터를 처리하고 표시하기 위해서 개발된 것이 CGI, ASP, PHP, JSP, Servlet

### 정적 웹 프로그래밍
- 웹 서버에서 보여줄 HTML, CSS, 이미지, JavaScript 등의 파일을 미리 저장해 놓고 브라우저에서 요청할 경우 그대로 전달
- 사용자는 페이지가 변경되지 않는 한 고정된 웹 페이지를 보게된다.
- 주로 화면의 디자인을 구성하거나 클라이언트의 이벤트를 처리한다.
- 실시간 또는 데이터베이스를 저장된 데이터를 표시하는데 적합하지 않은 방식

#### 정적 웹 프로그래밍 구성 요소
- 클라이언트
  - 네트워크로 서버에 접속한 후 서버로부터 서비스를 제공받는 컴퓨터 및 소프트웨어(웹 브라우저)
- 웹 서버
  - 각 클라이언트로부터 요청을 받고 서비스를 제공하는 컴퓨터 및 소프트웨어
- HTTP 프로토콜
  - www 서비스를 제공하기 위한 표준 언어
  - Hyper Text Transfer Protocol
  - www 서비스를 제공하는 통신 규약
  - 웹 서버와 클라이언트는 이 프로토콜을 이용해서 정보를 주고 받음
- 자바스크립트 
  - HTML 웹 페이지의 여러 가지 동적인 기능을 제공하는 스크립트 언어
- CSS
  - HTML 페이지의 디자인 관련된 기능 제공 언어

### 동적 웹 프로그래밍
- 관리자의 역할을 웹 애플리케이션 서버(Web Application Server : WAS)가 수행
- 클라이언트의 요청이 있을 때 데이터베이스에 접근해서 실시간 정보를 얻어와서 클라이언트에게 전송 
- 초기 동적 웹 프로그래밍에서 사용하는 방식
  - CGI(Common Gate Interface : 공용 게이트웨이 인터페이스)
    - 대표적인 CGI 언어 : 펄(Perl)
  - 프로세스 방식으로 실행
  - 프로세스 마다 메모리에 로드하는 방식으로 메모리에 과부하 발생하는 문제
- 프로세스 방식의 문제를 해결하면서 나온 기술들이 JSP, ASP, PHP
  - 브라우저 요청 시 스레드 방식으로 실행하기 때문에 CGI보다 효율적으로 기능을 수행
  - 클라이언트 요청을 처리하는 기능은 최초 한번만 메모리에 로드
  - 동일한 기능 요구 시 기존에 사용한 기능을 재사용
  - 따라서 프로세스 방식으로 동작하는 것보다 훨씬 빠르게 수행

#### 동적 웹 프로그래밍 구성 요소
- 웹 브라우저
  - 클라이언트. 사용자의 작업 창 (HW/SW)
- 웹 서버
  - 웹 브라우저의 요청을 받아들이는 곳 (HW/SW)
- 웹 애플리케이션 서버 (WAS)
  - 요청된 페이지의 비즈니스 로직 및 데이터베이스와의 연동을 처리
  - Apache Tomcat
- 데이터베이스
  - 데이터 저장소

### 웹 서비스 구조 및 처리 순서
## 사진


## 웹 서버
- 웹에서 서버 기능을 수행하는 프로그램
- HTTP 프로토콜 기반으로
- 웹 클라이언트(웹 브라우저)로부터 요청을 서비스하는 기능 담당
- 정적인 컨텐츠(HTML, CSS 등) 제공
- 동적인 컨텐츠 요청은 웹 컨테이너에게 보내고 
- 웹 컨테이너가 처리한 결과를 클라이언트에게 응답
- 웹 서버 종류
  - Apache
  - IIS (Internet Information Server) : MS

### 웹 컨테이너 (Web Container)
- 웹 애플리케이션을 실행할 수 있는 컨테이너
- JSP와 서블릿(Servlet)을 실행시킬 수 있는 소프트웨어
- 서블릿 컨테이너라고도 함
  - 웹 서버가 서블릿 자체를 실행하지 못하므로 JVM을 내장한 컨테이너라고 하는 서블릿 실행 환경이 필요
- 서블릿과 JSP 대한 실행 환경 제공
- 정적 페이지(static page)에 대한 요청도 처리 가능
- 웹 서버에서 JSP를 요청하면 톰캣(웹서버+컨테이너)에서 JSP 파일을 서블릿으로 변환하여 컴파일을 수행하고
- 서블릿 수행 결과를 웹 서버에게 전달
- 서블릿의 생명주기 관리
- Web Application 당 한 개의 Servlet Context 객체 생성

### 웹 컨테이너가 사용자의 요청에 응답하는 순서
1. 클라이언트가 HTTP request를 HTTP service (웹 서버)에게 전송
2. HTTP service는 요청 데이터를 웹 컨테이너에게 전송
3. 웹 컨테이너가 HttpServletRequest 객체와 HttpServletResponse 객체를 생성
4. 웹 컨테이너는 요청된 Servlet 의 서비스 메소드를 호출하여 Servlet 활성화시킴
5. 웹 컨테이너는 Servlet에 의해 생성된 응답 데이터를 HTTP service (웹 서버)에게 전송
6. HTTP service (웹 서버)는 HTTP response를 클라이언트에게 전송

- 클라이언트 요청 -> 웹 서버 -> 웹 컨테이너 (서블릿 활성화)  응답 -> 웹 서버 -> 클라이언트

### 웹 애플리케이션 서버 (Web Application Server : WAS)
- 웹 서버로부터 오는 동적인 요청을 처리하는 서버
- 웹 서버 기능 + 웹 컨테이너 기능
- 기타 기능
  - 트랜잭션, 보안, 트래픽 관리, DB 커넥션 풀, 사용자 관리 등 다양한 기능 제공
- Apache Tomcat은 WAS

### 웹 컨테이너에서 웹 애플리케이션 요청 처리
- HTML / CSS / 자바스크립트 실습 시 톰캣을 server로 생성해서 사용
  - HTML 파일 입력하고 서버 실행
  - 웹 브라우저에서결과 확인
  - http://localhost:8080/HTML01/start.html
- 서버로 데이터 전송 못했고, 서버로부터 데이터 받지 못한다.
- 이후 JSP와 서블릿, DB 연동을 통해 서버 페이지와 데이터 주고 받는다.

## JSP와 Servlet
- JSP (Java Server Pages)
  - HTML 내에 Java 언어를 삽입한 문서
  - .jsp
- Servlet (Server + Applet)
  - Java 언어로 이루어진 웹 프로그래밍 문서
  - 자바 코드에 의존적
  - .java

### JSP 페이지의 실행 과정
## 사진

## 서블릿(Servlet)
- 서버 측에서 실행되면서 클라이언트의 요청에 따라 동적으로 서비스를 제공하는 자바 클래스(응답 : HTML 형식)
- 자바 플랫폼에서 컴포넌트 기반의 웹 애플리케이션을 개발하는 핵심 기술(동적 웹 애플리케이션 컴포넌트)
- 컨테이너 종류에 상관없이 실행됨(플랫폼 독립적)
- 독자적으로 실행되지 못하고 톰캣과 같은 JSP/Servlet 컨테이너에서 실행
- 자바로 만들어졌기 때문에 자바의 특징(객체 지향)을 가짐
- 스레드 기반
- JSP 페이지처럼 화면에 내용을 표시할 목적으로 사용하는 것이 아니라 MVC 패턴에서 로직인 모델과 화면에 결과를 표시하는 뷰 사이에서 제어를 담당하는 컨트롤로 사용됨
- Servlet을 많이 사용하는 이유는 빠른 응답 속도 때문
  - 최초 요청 시 객체가 만들어져 메모리에 로드되고 이후 요청 시 기존 객체 재활용하기 때문에 동작 속도가 빠르다.
- 장점
  - 신뢰성
  - 확장성(기능 확장 용이)
  - 플랫폼과 서버에 독립적(자바 기반)
    - 한 번 개발된 애플리케이션은 다양한 서버 환경에서 실행 가능
  - Java에서 제공되는 다른 기술 사용 가능
    - 예 : Servlet + JDBC 연동
- 생성 과정
  1. Servlet 클래스 생성
  2. Servlet 생명주기 메소드 구현
  3. Servlet 매핑 작업
  4. 웹 브라우저에서 Servlet 매핑 이름으로 요청
  - 서블릿 매핑(mapping)
    - 서블릿 경로 연결 (url 주소에 출력될 경로 이름 설정)
    - 서블릿 파일 경로 노출로 인한 보안 문제를 없애고, url을 간단하게 줄일 수 있음 
    - 웹 브라우저에서 서블릿을 요청하기 위해서는 서블릿 매핑 필요
    - 방법
      -  web.xml에서 설정
      -  어노테이션 이용 (이클립스에서 자동 지정 ) : 변경 가능

### 서블릿 처리 순서
- 동일한 Servlet class에 대한 요청을 처리하는 모든 thread(스레드)는 같은 Servlet 객체를 공유해서 동시성 문제가 발생할 수 있지만, 로컬 변수는 각 요청 스레드마다 각각의 스택 영역에 저장되기 때문에 동시성 문제를 발생시키지 않음
1. 클라이언트에서 서블릿 요청이
2. 서버에서 서블릿 컨테이너 만들고 스레드 생성(요청 시 마다 스레드 생성)
3. 서블릿 컨테이너는 스레드를 가동하려 서블릿 객체 생성
4. 서블릿 실행 결과가 웹 서버로 전송
5. 결과를 웹 서버가 웹 브라우저에게 전송
6. 서블릿 객체의 실행이 종료되면 스레드 종료되고 반환

## 서블릿 처리 사진

## 서블릿 라이프사이클 사진

### 서블릿 패키지
- javax.servlet.* 
  - 서블릿 작성을 위한 인터페이스와 클래스 제공
- javax.servlet.http.*
  - HTTP 프로토콜은 이용한 서블릿 작성에 필요한 인터페이스 제공(GET/POST)

### 서블릿 클래스
- Servlet 인터페이스
- GenericServlet 추상 클래스
- HttpServlet 클래스 상속 받음
- HttpServlet -> GenericServlet -> Servlet

### 서블릿 생성 과정
1. Servlet 클래스 생성
2. 서블릿 생성주기 메소드 구현
3. 서블릿 매핑 작업
4. 웹 브라우저에서 서블릿 매핑 이름으로 요청

### 서블릿 매핑 (mapping)
- 서블릿 경로 연결 (url 주소에 출력될 경로 이름 설정)
- 서블릿 파일 경로 노출로 인한 보안 문제를 없애고 url을 간단하게 줄일 수 있음 
- 웹 브라우저에서 서블릿을 요청하기 위해서는 서블릿 매핑 필요
- http://localhost:8080/프로젝트명/서블릿 매핑 이름/
- 서블릿  매핑 방법
  - web.xml에서 설정
  - 어노테이션 이용 (이클립스에서 자동 지정 ) : 변경 가능

### HttpServletRequest request, HttpServletResponse response
- 톰캣에서 request 객체와 response 객체 생성해서 doGet() 메소드 안에 인자 값으로 넣어줌
- request 객체 :  요청 처리 객체
  - 클라이언트에서 입력한 데이터가  request 객체에 담겨져서 서버로 전달
- response 객체 : 응답 처리 객체
  - 서버 측에서 처리한 결과를 response 객체에 담아서 클라이언트로 전달
- doGet()과 doPost() 둘 다 매개변수로 request/ response 객체를 갖음
  - 클라이언트 요청 처리
  - 클라이언트에게 응답 처리

### 서블릿 동작 과정
## 사진

### 컨텍스트 (Context)
- 톰캣의 server.xml에 등록하는 웹 애플리케이션을 컨텍스트(Context)라고 함
  - 즉, 톰캣 입장에서 인식하는 한 개의 웹 애플리케이션에 해당
- 웹 애플리케이션 당 하나의 컨텍스트가 등록됨
- 웹 애플리케이션 이름과 같을 수도 다를 수도 있음
- 컨텍스트 이름은 중복되면 안 됨 (유일한 이름)
- 대소문자 구분
- server.xml에 등록
- 이클립스에서 프로젝트 생성하면 자동으로 server.xml에 추가됨
- 최종 실행 시 포함된 프로젝트가 Context로 남게 됨
- \<Context docBase="Servlet01" path="/Servlet01" reloadable="true" source="org.eclipse.jst.jee.server:Servlet01"/>
- 구성 요소
  - path : 웹 애플리케이션의 컨텍스트 이름, 웹 애플리케이션 이름과 다를 수도 있으며 웹 브라우저에서 실제 웹 애플리케이션을 요청하는 이름
  - docBase : 컨텍스트에 대한 실제 웹 애플리케이션이 위치한 경로. WEB-INF 상위 폴더 까지의 경로를 나타낸다.
  - reloadable : 실행 중 소스 코드가 수정될 경우 바로 갱신할지를 설정. 만약 false로 설정하면 톰캣을 다시 실행해야 추가한 소스 코드의 기능이 반영

### URL / URI / ContextPath / ServletPath
- URL : 전체 주소
  - http://localhost:8080/Servlet01/second
  - 프로토콜 + IP + 포트 번호 + URI
- URI : ContextPath + ServletPath
  - /Servlet01/second
  - 프로젝트명 + 서블릿 매핑 이름
- ContextPath : 프로젝트명
  - /Servlet01
- ServletPath : 서블릿 매핑 이름 (원래 : 패키지명 + 파일명) 임의로 변경해서 용
  - /second
  - 간결성 / 보안 유지

## 서블릿 요청 API
- 서블릿 기본 기능
  1. 클라이언트로부터 요청을 받음
  2. 데이터베이스 연동과 같은 비즈니스 로직 처리
  3. 처리된 결과를 클라이언트에게 응답
- 서블릿 요청과 응답 수행 API
  - javax.servlet.http 패키지에 포함
  - 요청과 관련된 API : javax.servlet.http.HttpServletRequest 클래스
  - 응답과 관련된 API : javax.servlet.http.HttpServletResponse 클래스
  - doGet() / doPost() 메소드에서 request, response 객체 사용

### \<form> 태그로 서블릿 요청
- \<form> 태그를 이용해 브라우저에서 서블릿으로 사용자의 요청이나 데이터를 전송
- 서블릿 데이터를 웹 브라우저로 전송
- \<form> 태그
  - action 속성 : 서블릿 또는 JSP 이름 지정
  - method 속성 : GET 또는 POST (디폴트 GET)
- \<input>태그
  - name 속성 사용
  - name 속성명과 속성값 쌍으로 전송
- 서블릿에서 클라이언트 요청에 사용되는 메소드
  - HttpServletRequest 클래스의 여러 메소드를 이용해서 전송된 데이터를 얻음
  - \<form> 태그로 전송된 데이터를 받아오는 메소드
  - String getParameter(String name) : name의 값을 알고 있을 때 그리고 name에 대한 전송된 값을 받아오는 데 사용
  - String[] getParameterValues(String name) : 같은 name에 대해 여러 개의 값을 얻을 때 사용
  - Enumeration getParameterNames() : name 값을 모를 때 사용

#### \<form> 태그를 사용해서 HttpServletRequest 요청 처리 예제 - login.html, LoginServlet.java

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form name="frmLogin" method="post" action="login" >
    아이디  :<input type="text" name="user_id"><br>
    비밀번호:<input type="password" name="user_pw" ><br>
    <input type="submit" value="로그인">  <input type="reset" value="다시입력">
</form>
</body>
</html>
~~~

~~~java
package com.example.servlet4;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;

@WebServlet("/login")
public class LoginServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }

    protected void doProcess(HttpServletRequest request, HttpServletResponse response)  throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");

        String id =  request.getParameter("user_id");
        String pw =  request.getParameter("user_pw");
        System.out.println("아이디 : " + id);
        System.out.println("비밀번호 : " + pw);
    }
}
~~~

## GET / POST
- POST 방식 전송
  - http://localhost:8080/Servlet01/login
  - 서블릿에게 데이터 전송할때 TCP/IP 프로코콜 데이터의 HEAD 영역에 숨겨진 채 전송
  - 보안에 유리
  - 전송 데이터 용량 무제한
  - 서블릿에서 처리시 GET 방식보다 느림
  - 서블릿에서 doPost() 메소드를 이용해서 처리
- GET 방식 전송  
  - http://localhost:8080/Servlet01/login?user_id=abcd&user_pw=1111
  - 서블릿에게 데이터를 전송할 때 데이터가 URL 뒤에 name=value 형태로 전송
  - 여러 개의 데이터를 전송할 때는 ‘&’로 구분해서 전송
  - 보안에 취약
  - 전송할 수 있는 데이터는 최대 255자 (길이 제한)
  - 기본 전송 방식으로 쉬움
  - 웹 브라우저에서 직접 입력해서 전송 가능 (디폴트 GET  방식)
  - 서블릿에서는 doGet() 메소드를 이용해서 처리

#### \<form> 태그를 이용해 서블릿에 데이터 전송 및 출력 연습문제 - bookForm.html, BookServlet.java

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>bookForm 예제</title>
	</head>
	<body>
				<h2>도서정보 출력</h2>
			<form method="post" action="bookInsert">
				<table>
					<tr>
						<th>도서번호</th>
						<td>
						<input type="text" name="bookNo">
					</tr>
					<tr>
						<th>도서명</th>
						<td>
						<input type="text" name="bookName">
					</tr>
					<tr>
						<th>저자</th>
						<td>
						<input type="text" name="bookAuthor">
					</tr>
					<tr>
						<th>가격</th>
						<td>
						<input type="text" name="bookPrice">
					</tr>
					<tr>
						<th>발행일</th>
						<td>
						<input type="text" name="bookYear" size="4">년
						<input type="text" name="bookMonth" size="2">월
						<input type="text" name="bookDate" size="2">일
					</tr>
					<tr>
						<th>재고</th>
						<td>
						<input type="text" name="qtyNo">
					</tr>
					<tr>
						<th>출판사번호</th>
						<td>
						<input type="text" name="pubNo">
					</tr>
					<tr>
						<td>
							<input type="submit" name="submit" value="등록">
							<input type="reset" name="reset" value="취소">
						</td>
					</tr>
				</table>
			</form>	
	</body>
</html>
~~~

~~~java
package com.example.servlet4;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/bookInsert")
public class BookServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doProcess(request, response);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doProcess(request, response);
	}

	protected void doProcess(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		request.setCharacterEncoding("utf-8");

		String bookNo = request.getParameter("bookNo");
		String bookName = request.getParameter("bookName");
		String bookAuthor = request.getParameter("bookAuthor");
		String bookPrice = request.getParameter("bookPrice");
		String bookYear = request.getParameter("bookYear");
		String bookMonth = request.getParameter("bookMonth");
		String bookDate = request.getParameter("bookDate");
		String qtyNo = request.getParameter("qtyNo");
		String pubNo = request.getParameter("pubNo");

		System.out.println("도서 번호: " + bookNo );
		System.out.println("도서 명: " + bookName );
		System.out.println("저자: " + bookAuthor );
		System.out.println("가격: " + bookPrice );
		System.out.println("발행일: " + bookYear+"-"+ bookMonth +"-"+bookMonth);
		System.out.println("재고: " + qtyNo );
		System.out.println("출판사 번호: " + pubNo );
	}
}
~~~

### 여러 개의 값을 전송할 때 요청 처리
- \<input> 태그에서 text 또는 radio 버튼의 경우 1개의 값을 전송하지만 체크박스인 경우 여러 개의 값을 선택해서 여러 개 전송
- getParameterValues() 메소드 사용해서 배열로 받음

#### 여러 개의 값을 전송할 때 요청 처리 예제 - input.html, InputServlet.java

~~~html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>여러 가지 input 타입 표시창</title>
</head>
<body>
<form name="frmInput" method="post" action="input">
   아이디  :<input type="text" name="user_id"><br>
   비밀번호:<input type="password" name="user_pw"><br>
   이메일 수신 여부 : <input type="radio" name="emailRcv" value="yes" checked>예
           <input type="radio" name="emailRcv" value="no">아니오<br>
   <input type="checkbox" name="subject" value="java" checked >자바
   <input type="checkbox" name="subject" value="C언어">C언어
   <input type="checkbox" name="subject" value="JSP">JSP
   <input type="checkbox" name="subject" value="안드로이드">안드로이드 
   <br><br>
   <input type="submit" value="전송">   
   <input type="reset" value="초기화">
  </form>
</body>
</html>

~~~

~~~java
package com.example.servlet4;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/input")
public class InputServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doProcess(request, response);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doProcess(request, response);
	}
	
	protected void doProcess(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		request.setCharacterEncoding("utf-8");

		String id = request.getParameter("user_id");
		String pw = request.getParameter("user_pw");
		String emailRcv = request.getParameter("emailRcv");
		String[] subject = request.getParameterValues("subject");
		
		System.out.println("아이디 : " + id);
		System.out.println("비밀번호 : " + pw);
		System.out.println("이메일 수신 여부 : " + emailRcv);
		
		System.out.print("관심분야 : ");
		for(String sub : subject) {
			System.out.print(sub + " ");
		}
		System.out.println();
	}
}
~~~

#### 여러 개의 값을 전송할 때 요청 처리 문제 - newMember.html, NewMemberServlet.java

~~~html
<!DOCTYPE html>
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
	        <form id="newMemberForm" name="newMemberForm" method="post" action="newMember">
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

~~~java
package com.example.servlet4;

import java.io.IOException;
import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/newMember")
public class NewMemberServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public void init(ServletConfig config) throws ServletException {

	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doProcess(request, response);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doProcess(request, response);
	}
	
	protected void doProcess(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		request.setCharacterEncoding("utf-8");
		
		String name = request.getParameter("name");
		String id = request.getParameter("id");
		String pwd = request.getParameter("pwd");
		String hp1 = request.getParameter("hp1");
		String hp2 = request.getParameter("hp2");
		String hp3 = request.getParameter("hp3");
		String year = request.getParameter("year");
		String[] interest = request.getParameterValues("interest");
		String department = request.getParameter("department");
		
		System.out.println("이름 : " + name);
		System.out.println("아이디 : " + id);
		System.out.println("비밀번호 : " + pwd);
		System.out.println("휴대폰 번호 : " + hp1+"-" + hp2+"-" + hp3 );
		System.out.println("학년 : " + year + "학년");
		
		System.out.print("관심분야 : ");
		 for (String inter : interest ) { 
			 System.out.print(inter + " ");
		 }
		 System.out.println();
		 System.out.println("학과 : " + department);
	}
}
~~~

### 서블릿 응답 처리
- 서블릿의 응답 처리
  1. setContentType()을 이용해 MIME-TYPE 지정
  2. 데이터를 출력할 PrintWriter 객체 생성
  3. 출력 데이터를 HTML 형식으로 작성
  4. PringWriter의 print()나 println()을 이용해 데이터 출력(웹 브라우저로 전송되어 출력)
- 서블릿 응답 처리 방법
  - doGet() 또는 doPost() 메소드 안에서 처리
  - javax.servlet.http.HttpServletResponse 객체 이용
  - setContentType()을 이용해서 클라이언트에게 전송할 데이터 종류(MIME-TYPE) 지정
    - response.setContentType(‘text/html;charset=utf-8”);
  - 클라이언트(웹 브라우저)와 서블릿 통신은 자바 I/O 스트림을 이용 (서버에서 클라이언트로 데이터 전송에 자바 I/O 스트림을 이용)
    - PrintWriter 클래스 사용
    - PrintWriter out = response.getWriter();
    - out.print(data); 
    - data : 웹 브라우저로 보내는 데이터
      - HTML 형식으로 출력되어야 하므로 
      - data에 HTML 태그 포함시켜서 전송
      - HTML 문서 형식을 제대로 작성해서 전송
      - 전송된 HTML 형식으로 출력
- MIME-TYPE
  - 톰캣 컨테이너에 미리 지정해 놓은 데이터 종류로 서블릿에서 브라우저로 전송 시 설정해서 사용
  - HTML로 전송 시 : text/html
    - 웹 브라우저는 기본적으로 HTML을 인식하므로 text/html로 지정
  - 일반 텍스트로 전송 시 : text/plain
  - XML 데이터로 전송 시 : application/xml

#### 서블릿의 응답 처리 예제 - login.html, LoginServlet.java

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form name="frmLogin" method="post" action="login2" >
    아이디  : <input type="text" name="user_id"><br>
    비밀번호: <input type="password" name="user_pw" ><br>
    <input type="submit" value="로그인">  <input type="reset" value="다시입력">
</form>
</body>
</html>
~~~

~~~java
package com.example.servlet4;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/login2")
public class LoginServlet2 extends HttpServlet {
        private static final long serialVersionUID = 1L;

        @Override
        protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            doProcess(request, response);
        }

        @Override
        protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            doProcess(request, response);
        }

        protected void doProcess(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            // 클라이언트 요청 처리
            // 클라이언트 -> 서버 인코딩
            request.setCharacterEncoding("utf-8");

            String id =  request.getParameter("user_id");
            String pw =  request.getParameter("user_pw");
            System.out.println("아이디 : " + id);
            System.out.println("비밀번호 : " + pw);
            // 응답처리
            // 서버 - > 클라이언트로 setContentType
            response.setContentType("text/html;charset=utf-8");

            // 서버에서 클라이언트로 데이터 전송에 자바 IO스트림 이용
            PrintWriter out = response.getWriter();
            // HTML 문서 형식으로 데이터 전송
            out.println("<html><head></head><body>");
            out.println("아이디 :" + id + "<br>" +  "비밀번호 : " + pw);
            out.println("</body></html>");
        }
    }
~~~