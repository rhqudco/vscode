## 자바스크립트로 서블릿에 요청

### DOM 사용 예제 - login.html, LoginServlet3.java

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        /* DOM 사용 */
        window.onload = function() {
            document.getElementById('frmLogin').onsubmit = function() {

                var id = document.getElementById('user_id');
                var pw = document.getElementById('user_pw');

                if(id.value == "" || pw.value == ""){
                    alert("아이디와 비밀번호는 필수입니다.");
                }else {
                    frmLogin.method = "post";
                    frmLogin.action = "login3";
                    frmLogin.submit();
                }

            };	 // onsubmit 끝
        };  // window.onload 끝
    </script>
</head>
<body>
<form id = "frmLogin" name = "frmLogin">
    아이디  : <input type="text" name="user_id" id="user_id"><br>
    비밀번호: <input type="password" name="user_pw" id="user_pw"><br>
    <input type="submit" value="로그인">  <input type="reset" value="다시입력">
</form>
</body>
</html>
~~~

~~~java
package com.example.servlet4;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/login3")
public class LoginServlet3 extends HttpServlet {
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

### name 속성 사용 예제 - login4.html, LoginServlet4.java

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        function fn_validate() {
            var frmLogin = document.frmLogin;
            var id = frmLogin.user_id.value;
            var pw = frmLogin.user_pw.value;

            if(id.value == "" || pw.value == ""){
                alert("아이디와 비밀번호는 필수입니다. 4");
                return false;
            }else {
                frmLogin.method = "post";
                frmLogin.action = "login4";
                frmLogin.submit();
            }
        }
    </script>
</head>
<body>
<form id = "frmLogin" name = "frmLogin">
    아이디  : <input type="text" name="user_id"><br>
    비밀번호: <input type="password" name="user_pw"><br>
    <input type="button" value="로그인" onclick="fn_validate()">  <input type="reset" value="다시입력">
</form>
</body>
</html>
~~~

~~~java
package com.example.servlet4;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/login4")
public class LoginServlet5 extends HttpServlet {
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

### jQuery 사용 - login5.html, LoginServlet5.java

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="jquery-3.6.0.min.js"></script>
    <script>
        $(document).ready(function () {
            $('#login').on('click', function () {
                var id = $('#user_id').val();
                var pw = $('#user_pw').val();
                if(id == "" || pw == ""){
                    alert("아이디와 비밀번호는 필수입니다. 5");
                    return false;
                }else {
                    // $('#frmLogin').attr('method', 'post').attr('action', 'login5').submit();
                    $('#frmLogin').attr({
                        method:'post',
                        action:'login5'
                    }).submit();
                }
            })
        })
    </script>
</head>
<body>
<form id = "frmLogin" name = "frmLogin">
    아이디  : <input type="text" name="user_id" id="user_id"><br>
    비밀번호: <input type="password" name="user_pw" id="user_pw"><br>
    <input type="button" value="로그인" id="login">  <input type="reset" value="다시입력">
</form>
</body>
</html>
~~~

~~~java
package com.example.servlet4;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/login5")
public class LoginServlet5 extends HttpServlet {
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

## 서블릿 DB 연동

### 서블릿의 비즈니스 로직 처리
- 데이터베이스 관련 작업
- 다른 서버 연동해서 데이터 얻는 작업 등
- 예
  - 회원 등록 요청 처리(DB에 회원 정보가 저장)
  - 로그인 처리 (DB에 있는 회원 정보와 입력하여 전송된 로그인 정보가 일치하는지 검사)
  - 쇼핑몰 주문 처리 작업
- 비즈니스 로직 처리 과정
  - 클라이언트로부터 요청
  - 데이터베이스 연동과 같은 비즈니스 로직 처리
  - 결과를 클라이언트에게 응답
  - HTML로 요청 -> 서블릿에서 요청 받음 -> DAO에서 비즈니스 로직 처리. 결과 반환 -> 서블릿에서 결과 받아서 클라이언트에게 응답 -> 클라이언트에서 결과 출력
- 나중에 스프링에서 처리하는 과정
  - JSP로 요청 -> 컨트롤러가 요청 받음 -> DAO에서 비즈니스 로직 처리. 결과 반환 -> 컨트롤러가 결과 받아서 클라이언트에게 응답 -> 클라이언트에서 결과 출력

### DTO vs VO
- DTO (Data Transfer Object)
  - 데이터 저장 (전송) 담당 클래스
  - Controller, Service, View 등 계층간 데이터 교환을 위해 사용되는 객체
  - 비즈니스 로직을 갖지 않는 순수한 데이터 객체
  - getter, setter 메소드만 포함
  - 가변의 성격 (setter를 사용해서 데이터 변경 가능)
-  VO (Value Object)
   - 데이터 저장 담당 클래스
   - DTO와 혼용해서 사용되지만
   - VO는 값(Value)을 위해 사용되는 객체로 불변(read only)의 속성
   - 보통 getter의 기능만 포함
   - 일반적으로 DTO와 같은 용도로 사용

#### 서블릿 DB연동 예제 - MemberDAO.java, MemberVO.java, MemberSelectServlet.java

~~~java
package com.example.servlet4.sec04;

import java.sql.*;
import java.util.ArrayList;
import java.util.Date;

public class MemberDAO {
    // DB 연결 담당 메소드
    public Connection connDB() {
        Connection con = null;

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");

            String url = "jdbc:mysql://localhost:3306/servletdb?serverTimezone=UTC";
            String user = "root";
            String pwd = "";

            con = DriverManager.getConnection(url, user, pwd);
            if(con != null) {
                System.out.println("연결 성공");
            }
        } catch(Exception e) {
            System.out.println("연결 오류 발생!");
            e.printStackTrace();
        }
        return con;
    }

    // 회원 정보 조회 메소드(전체 회원 정보 select : MemberVO 반환)
    // MemberVO를여러 행 반환 : ArrayList<MemberVO>
    public ArrayList<MemberVO> memberSelect() {
        Connection con = null;
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;

        ArrayList<MemberVO> memList = new ArrayList<MemberVO>();

        try {
            con = connDB();
            String query = "select * from member";
            preparedStatement = con.prepareStatement(query);
            resultSet = preparedStatement.executeQuery(query);

            while(resultSet.next()) { // 결과 세트에서 한 행씩 처리
                // 한 행(회원 1명당) 처리
                String id = resultSet.getString("memId");
                String pwd = resultSet.getString("memPwd");
                String name = resultSet.getString("memName");
                String email = resultSet.getString("memEmail");
                Date joinDate = resultSet.getDate("memJoinDate");
                // 한 행 정보 가져와 memberVO에 Setter 이용하여 저장
                MemberVO vo = new MemberVO();
                vo.setId(id);
                vo.setPwd(pwd);
                vo.setName(name);
                vo.setEmail(email);
                vo.setJoinDate(joinDate);
                // 각 memberVO를 ArrayList에 저장
                memList.add(vo);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                resultSet.close();
                preparedStatement.close();
                con.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
        return  memList;
    }
}
~~~

~~~java
package com.example.servlet4.sec04;

import java.util.Date;

public class MemberVO {
    private String id;
    private String pwd;
    private String name;
    private String email;
    private Date joinDate;

    // 디폴트 생성자
    public MemberVO() { }
    // 현재는 매개변수 있는 생성자 필요 없다.
    public MemberVO(String id, String pwd, String name, String email, Date joinDate) {
        this.id = id;
        this.pwd = pwd;
        this.name = name;
        this.email = email;
        this.joinDate = joinDate;
    }

    // Getter / Setter
    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getPwd() {
        return pwd;
    }

    public void setPwd(String pwd) {
        this.pwd = pwd;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public Date getJoinDate() {
        return joinDate;
    }

    public void setJoinDate(Date joinDate) {
        this.joinDate = joinDate;
    }
}
~~~

~~~java
package com.example.servlet4.sec04;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.ArrayList;
import java.util.Date;

//@WebServlet(name = "MemberSelectServlet", value = "/MemberSelectServlet")
@WebServlet("/sec04/MemberSelectServlet")
public class MemberSelectServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }
    protected void doProcess(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");
        // 서버에서 클라이언트로 데이터 전송에 자바 IO스트림 이용
        PrintWriter out = response.getWriter();

        MemberDAO dao = new MemberDAO();
        ArrayList<MemberVO> memList = dao.memberSelect();
        out.print("<html><head></head><body>");
        out.print("<table border=1><tr align='center' bgcolor='gold'>");
        out.print("<td>아이디</td><td>비밀번호</td><td>이름</td><td>이메일</td>" +
                "<td>가입일</td></tr>");
        for(int i = 0; i < memList.size(); i++) {
            // 오브젝트 반환 MemberVO 타입으로 형변환
            MemberVO vo = (MemberVO)memList.get(i);
            String id = vo.getId();
            String pwd = vo.getPwd();
            String name = vo.getName();
            String email = vo.getEmail();
            Date joinDate = vo.getJoinDate();
            // 한 행씩 출력
            out.print("<tr><td>" + id + "</td><td>" +
                                    pwd + "</td><td>" +
                                    name + "</td><td>" +
                                    email + "</td><td>" +
                                    joinDate + "</td></tr>");
        }
        out.print("</table></body></head>");
    }
}
~~~

#### 서블릿 DB연동 연습문제 - BookDAO.java, BookVO.java, BookSelectServlet.java

~~~java
package com.example.servlet4.sec05;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.ArrayList;
import java.util.Date;

public class BookDAO {
    // DB 연결 담당 메소드
    public Connection connDB() {
        Connection con = null;

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");

            String url = "jdbc:mysql://localhost:3306/servletdb?serverTimezone=UTC";
            String user = "root";
            String pwd = "";

            con = DriverManager.getConnection(url, user, pwd);
            if(con != null) {
                System.out.println("연결 성공");
            }
        } catch(Exception e) {
            System.out.println("연결 오류 발생!");
            e.printStackTrace();
        }
        return con;
    }

    // 회원 정보 조회 메소드(전체 회원 정보 select : BookVO 반환)
    // BookVO를 여러 행 반환 : ArrayList<BookVO>
    public ArrayList<BookVO> bookSelect() {
        Connection con = null;
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;

        ArrayList<BookVO> bookList = new ArrayList<BookVO>();

        try {
            con = connDB();
            String query = "select * from book";
            preparedStatement = con.prepareStatement(query);
            resultSet = preparedStatement.executeQuery(query);

            while(resultSet.next()) { // 결과 세트에서 한 행씩 처리
                // 한 행(책 한 개당) 처리
                String bookNo = resultSet.getString("bookNo");
                String bookName = resultSet.getString("bookName");
                String bookAuthor = resultSet.getString("bookAuthor");
                int bookPrice = resultSet.getInt("bookPrice");
                Date bookDate = resultSet.getDate("bookDate");
                String pubNo = resultSet.getString("pubNo");
                // 한 행 정보 가져와 BookVO에 Setter 이용하여 저장
                BookVO vo = new BookVO();
                vo.setBookNo(bookNo);
                vo.setBookName(bookName);
                vo.setBookAuthor(bookAuthor);
                vo.setBookPrice(bookPrice);
                vo.setBookDate(bookDate);
                vo.setPubNo(pubNo);
                // 각 BookVO를 ArrayList에 저장
                bookList.add(vo);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                resultSet.close();
                preparedStatement.close();
                con.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
        return bookList;
    }
}
~~~

~~~java
package com.example.servlet4.sec05;

import java.util.Date;

public class BookVO {
    private String bookNo;
    private String bookName;
    private String bookAuthor;
    private int bookPrice;
    private Date bookDate;
    private String pubNo;

    public BookVO() { }

    public BookVO(String bookNo, String bookName, String bookAuthor, int bookPrice, Date bookDate, String pubNo) {
        this.bookNo = bookNo;
        this.bookName = bookName;
        this.bookAuthor = bookAuthor;
        this.bookPrice = bookPrice;
        this.bookDate = bookDate;
        this.pubNo = pubNo;
    }

    public String getBookNo() {
        return bookNo;
    }

    public void setBookNo(String bookNo) {
        this.bookNo = bookNo;
    }

    public String getBookName() {
        return bookName;
    }

    public void setBookName(String bookName) {
        this.bookName = bookName;
    }

    public String getBookAuthor() {
        return bookAuthor;
    }

    public void setBookAuthor(String bookAuthor) {
        this.bookAuthor = bookAuthor;
    }

    public int getBookPrice() {
        return bookPrice;
    }

    public void setBookPrice(int bookPrice) {
        this.bookPrice = bookPrice;
    }

    public Date getBookDate() {
        return bookDate;
    }

    public void setBookDate(Date bookDate) {
        this.bookDate = bookDate;
    }

    public String getPubNo() {
        return pubNo;
    }

    public void setPubNo(String pubNo) {
        this.pubNo = pubNo;
    }
}
~~~

~~~java
package com.example.servlet4.sec05;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.ArrayList;
import java.util.Date;

@WebServlet("/sec05/BookSelectServlet")
public class BookSelectServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }
    protected void doProcess(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");
        // 서버에서 클라이언트로 데이터 전송에 자바 IO스트림 이용
        PrintWriter out = response.getWriter();

        BookDAO dao = new BookDAO();
        ArrayList<BookVO> bookList = dao.bookSelect();
        out.print("<html><head></head><body>");
        out.print("<table border=1><tr align='center' bgcolor='gold'>");
        out.print("<td>도서번호</td><td>도서명</td><td>저자</td><td>가격</td>" +
                "<td>발행일</td><td>출판사번호</td></tr>");
        for(int i = 0; i < bookList.size(); i++) {
            // 오브젝트 반환 MemberVO 타입으로 형변환
            BookVO vo = (BookVO)bookList.get(i);
            String bookNo = vo.getBookNo();
            String bookName = vo.getBookName();
            String bookAuthor = vo.getBookAuthor();
            int bookPrice = vo.getBookPrice();
            Date bookDate = vo.getBookDate();
            String pubNo = vo.getPubNo();
            // 한 행씩 출력
            out.print("<tr><td>" + bookNo + "</td><td>" +
                    bookName + "</td><td>" +
                    bookAuthor + "</td><td>" +
                    bookPrice + "</td><td>" +
                    bookDate + "</td><td>" +
                    pubNo + "</td></tr>");
        }
        out.print("</table></body></head>");
    }
}
~~~

## Connection Pool(커넥션 풀 : DBCP(DataBase Connection Pool))
- 등장 배경
  - 기존 데이터베이스 연결 방법의 문제점
    - 애플리케이션에서 데이터베이스 연결 과정에서 시간이 많이 소요
  - 해결 방안
    - 애플리케이션 실행 시 미리 Connection 객체를 생성하고, 미리 데이터베이스 연결을 해 놓음
    - 애플리케이션은 데이터베이스 연동 작업 발생 시 미리 생성되어 있는 Connection객체를 이용해 작업
### 커넥션 풀
## 사진
- 일정량의 DB Connection 객체를 Pool에 저장해 두고 클라이언트 요청이 있을 때 마다 가져다 사용하고 반환
- 클라이언트에서 다수의 요청이 발생될 경우 요청마다 DB Connection 객체를 생성하게 되면 데이터베이스에 부하가 발생하기 때문에 커넥션 풀 기법 이용
  - JDBC를 통하여 DB에 연결하게 되면 사용자의 요청이 있을 때마다 매번 드라이버를 로드하고 커넥션 객체를 생성하여 연겨라고 종료하는 작업을 반복하면 비효율적
- 장점
  - 풀 속에 미리 커넥션이 생성되어 있기 때문에 커넥션 생성에 시간이 걸리지 않음
  - 커넥션을 계속 사용하고 반환하기 때문에 재사용 가능하므로 많은 수의 커넥션을 만들지 않아도 된다.
  - 매번 커넥션을 생성하고 해제하는데 시간이 소요되지 않으므로 애플리케이션 실행 속도가 빨라진다.
  - 생성되는 커넥션 수를 제어하기 때문에 동시 접속자 수가 증가해도 애플리케이션이 쉽게 Down되지 않는다.
  - 접속 시 사용할 커넥션이 없으면 대기 상태로 전환되고, 반환되면 대기 순서대로 커넥션 제공
- 동작 과정
  - 톰캣 컨테이너를 실행한 후 응용프로그램 실행
  - 톰캣 컨테이너 실행 시 ConnectionPool 객체 생성
  - 생성된 커넥션객체는 DBMS와 미리 연결
  - 데이터베이스 연동 작업이 필요할 경우 응용 프로그램은 ConnectionPool에서 제공하는 메소드를 
  - 호출하여 연동
- context.xml, web.xml에 추가

~~~xml
<!-- context.xml -->
    <Resource
            name="jdbc/mysql"
            type="javax.sql.DataSource"
            auth="Container"
            driverClassName="com.mysql.cj.jdbc.Driver"
            url="jdbc:mysql://localhost:3306/servletdb?serverTimezone=UTC"
            username="root"
            password=""
            maxActive="50"
            maxWait="1000"
    />
    <!-- maxWait : 커넥션이 없을 때 대기 시간 (1000 : 1초) 음수이면 무한 대기
<Resource 

   name="데이터베이스 이름"
   auth="Container" 
   driverClassName="oracle.jdbc.driver.OracleDriver" 
   type="javax.sql.DataSource" 
   url="jdbc:oracle:thin:@ip주소:포트번호:전역 데이터베이스 이름" 
   username="데이터베이스 아이디"
   password="데이터베이스 비밀번호" 
   maxActive="20" 
   maxIdle="10" 
   maxWait="5000"  />
 -->
~~~

~~~xml
<!-- web.xml -->
    <resource-ref>
        <description>Connection</description>
        <res-ref-name>jdbc/mysql</res-ref-name>
        <res-type>javax.sql.DataSource</res-type>
        <res-auth>Container</res-auth>
    </resource-ref>

    <!-- 
    <resource-ref>
    <description>Connection</description>
    <res-ref-name>자신의 데이터베이스 이름</res-ref-name>
    <res-type>javax.sql.DataSource</res-type>
    <res-auth>Container</res-auth>
    </resource-ref>          
    -->
~~~

#### 커넥션 풀 예제 - MemberDAO.java, MemberVO.java, MemberSelectServlet.java

~~~java
public class MemberDAO {
    private Connection con = null;
    DataSource dataSource = null;
    // 생성자에서 DB연결 설정
    public MemberDAO() {
        try {
            Context init = new InitialContext();
            dataSource = (DataSource)init.lookup("java:comp/env/jdbc/mysql");
            System.out.println("연결 성공");
        } catch (Exception e) {
            System.out.println("연결 실패");
            e.printStackTrace();
        }
    }
~~~

~~~java
package com.example.servlet4.sec06;

import java.util.Date;

public class MemberVO {
    private String id;
    private String pwd;
    private String name;
    private String email;
    private Date joinDate;

    // 디폴트 생성자
    public MemberVO() { }
    // 현재는 매개변수 있는 생성자 필요 없다.
    public MemberVO(String id, String pwd, String name, String email, Date joinDate) {
        this.id = id;
        this.pwd = pwd;
        this.name = name;
        this.email = email;
        this.joinDate = joinDate;
    }

    public MemberVO(String id, String pwd, String name, String email) {
        this.id = id;
        this.pwd = pwd;
        this.name = name;
        this.email = email;
    }

    // Getter / Setter
    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getPwd() {
        return pwd;
    }

    public void setPwd(String pwd) {
        this.pwd = pwd;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public Date getJoinDate() {
        return joinDate;
    }

    public void setJoinDate(Date joinDate) {
        this.joinDate = joinDate;
    }
}

~~~

~~~java
package com.example.servlet4.sec06;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.ArrayList;
import java.util.Date;

//@WebServlet(name = "MemberSelectServlet", value = "/MemberSelectServlet")
@WebServlet("/sec06/MemberSelectServlet")
public class MemberSelectServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }
    protected void doProcess(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");
        // 서버에서 클라이언트로 데이터 전송에 자바 IO스트림 이용
        PrintWriter out = response.getWriter();

        MemberDAO dao = new MemberDAO();
        ArrayList<MemberVO> memList = dao.memberSelect();
        out.print("<html><head></head><body>");
        out.print("<table border=1><tr align='center' bgcolor='gold'>");
        out.print("<td>아이디</td><td>비밀번호</td><td>이름</td><td>이메일</td>" +
                "<td>가입일</td></tr>");
        for(int i = 0; i < memList.size(); i++) {
            // 오브젝트 반환 MemberVO 타입으로 형변환
            MemberVO vo = (MemberVO)memList.get(i);
            String id = vo.getId();
            String pwd = vo.getPwd();
            String name = vo.getName();
            String email = vo.getEmail();
            Date joinDate = vo.getJoinDate();
            // 한 행씩 출력
            out.print("<tr><td>" + id + "</td><td>" +
                                    pwd + "</td><td>" +
                                    name + "</td><td>" +
                                    email + "</td><td>" +
                                    joinDate + "</td></tr>");
        }
        out.print("</table></body></head>");
    }
}
~~~

#### 커넥션 풀 연습 - MemberDAO.java, MemberVO.java, MemberSelectServlet2.java, MemberInsertServlet.java, MemberDeleteServlet.java

~~~java
package com.example.servlet4.sec06;

import javax.naming.Context;
import javax.naming.InitialContext;
import javax.naming.NamingException;
import javax.sql.DataSource;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.ArrayList;
import java.util.Date;

public class MemberDAO {
    private Connection con = null;
    DataSource dataSource = null;
    // 생성자에서 DB연결 설정
    public MemberDAO() {
        try {
            Context init = new InitialContext();
            dataSource = (DataSource)init.lookup("java:comp/env/jdbc/mysql");
            System.out.println("연결 성공");
        } catch (Exception e) {
            System.out.println("연결 실패");
            e.printStackTrace();
        }
    }

    // 회원 정보 조회 메소드(전체 회원 정보 select : MemberVO 반환)
    // MemberVO를여러 행 반환 : ArrayList<MemberVO>
    public ArrayList<MemberVO> memberSelect() {
        Connection con = null;
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;

        ArrayList<MemberVO> memList = new ArrayList<MemberVO>();

        try {
            con = dataSource.getConnection();
            String query = "select * from member";
            preparedStatement = con.prepareStatement(query);
            resultSet = preparedStatement.executeQuery(query);

            while(resultSet.next()) { // 결과 세트에서 한 행씩 처리
                // 한 행(회원 1명당) 처리
                String id = resultSet.getString("memId");
                String pwd = resultSet.getString("memPwd");
                String name = resultSet.getString("memName");
                String email = resultSet.getString("memEmail");
                Date joinDate = resultSet.getDate("memJoinDate");
                // 한 행 정보 가져와 memberVO에 Setter 이용하여 저장
                MemberVO vo = new MemberVO();
                vo.setId(id);
                vo.setPwd(pwd);
                vo.setName(name);
                vo.setEmail(email);
                vo.setJoinDate(joinDate);
                // 각 memberVO를 ArrayList에 저장
                memList.add(vo);
            }
            System.out.println("회원 조회 성공");
        } catch (Exception e) {
            e.printStackTrace();
            System.out.println("회원 조회 실패");
        } finally {
            try {
                resultSet.close();
                preparedStatement.close();
                con.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
        return  memList;
    }
    // 회원 정보 등록하는 메소드
    public void memberInsert(MemberVO memberVO) {
        try {
            con = dataSource.getConnection();

            String sql = "insert into member values(?, ?, ?, ?, default)";
            PreparedStatement preparedStatement = con.prepareStatement(sql);

            preparedStatement.setString(1, memberVO.getId());
            preparedStatement.setString(2, memberVO.getPwd());
            preparedStatement.setString(3, memberVO.getName());
            preparedStatement.setString(4, memberVO.getEmail());
            int result = preparedStatement.executeUpdate();
            if (result > 0) {
                System.out.println("회원 정보 입력 성공");
            }
            preparedStatement.close();
            con.close();
        } catch (Exception e) {
            System.out.println("insert 오류 발생!");
            e.printStackTrace();
        }
    }

    // 회원 정보 삭제 메소드
    public void memberDelete(String id ) {

        try {
            con = dataSource.getConnection();

            String sql = "delete from member where memId=?";
            PreparedStatement preparedStatement = con.prepareStatement(sql);

            preparedStatement.setString(1, id);
            // 쿼리문 실행 : 영향을 받은 행의 수 반환
            //select : executeQuery - 결과 행 resultSet 반환.
            //insert / update / delete : executeUpdate() - 영향을 받은 행의 수 반환
            int result = preparedStatement.executeUpdate();

            if(result > 0) {
                System.out.println("회원 정보 삭제 성공!");
            }
            // 모든 객체 close() : 리소스 반납
            preparedStatement.close();
            con.close();
        } catch (Exception e) {
            System.out.println("delete 발생!");
            e.printStackTrace();
        }
    }
}
~~~

~~~java
package com.example.servlet4.sec06;

import java.util.Date;

public class MemberVO {
    private String id;
    private String pwd;
    private String name;
    private String email;
    private Date joinDate;

    // 디폴트 생성자
    public MemberVO() { }
    // 현재는 매개변수 있는 생성자 필요 없다.
    public MemberVO(String id, String pwd, String name, String email, Date joinDate) {
        this.id = id;
        this.pwd = pwd;
        this.name = name;
        this.email = email;
        this.joinDate = joinDate;
    }

    public MemberVO(String id, String pwd, String name, String email) {
        this.id = id;
        this.pwd = pwd;
        this.name = name;
        this.email = email;
    }

    // Getter / Setter
    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getPwd() {return pwd;}

    public void setPwd(String pwd) {
        this.pwd = pwd;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public Date getJoinDate() {
        return joinDate;
    }

    public void setJoinDate(Date joinDate) {
        this.joinDate = joinDate;
    }
}
~~~

~~~java
package com.example.servlet4.sec06;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.ArrayList;
import java.util.Date;

//@WebServlet(name = "MemberSelectServlet", value = "/MemberSelectServlet")
@WebServlet("/sec06/MemberSelectServlet2")
public class MemberSelectServlet2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }
    protected void doProcess(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");
        // 서버에서 클라이언트로 데이터 전송에 자바 IO스트림 이용
        PrintWriter out = response.getWriter();

        MemberDAO dao = new MemberDAO();
        ArrayList<MemberVO> memList = dao.memberSelect();
        out.print("<html><head></head><body>");
        out.print("<table border=1><tr align='center' bgcolor='gold'>");
        out.print("<td>아이디</td><td>비밀번호</td><td>이름</td><td>이메일</td>" +
                "<td>가입일</td><td>삭제</td></tr>");
        for(int i = 0; i < memList.size(); i++) {
            // 오브젝트 반환 MemberVO 타입으로 형변환
            MemberVO vo = (MemberVO)memList.get(i);
            String id = vo.getId();
            String pwd = vo.getPwd();
            String name = vo.getName();
            String email = vo.getEmail();
            Date joinDate = vo.getJoinDate();
            // 한 행씩 출력
            out.print("<tr><td>" + id + "</td><td>" +
                                    pwd + "</td><td>" +
                                    name + "</td><td>" +
                                    email + "</td><td>" +
                                    joinDate + "</td><td>" +
                                    "<a href='/MemberDeleteServlet?id=" + id + "'>삭제</a></td></tr>");
        }
        out.print("</table></body></head>");
    }
}
~~~

~~~java
package com.example.servlet4.sec06;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Date;
import java.util.Scanner;

@WebServlet("/sec06/MemberInsertServlet")
public class MemberInsertServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }

    protected void doProcess(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");

        String id = request.getParameter("user_id");
        String pwd = request.getParameter("user_pw");
        String name = request.getParameter("user_name");
        String email = request.getParameter("user_email1");

        MemberVO memberVO = new MemberVO();
        memberVO.setId(id);
        memberVO.setPwd(pwd);
        memberVO.setName(name);
        memberVO.setEmail(email);
        // or
        // MemberVO memberVO = new MemberVO(id, pwd, name,email);
        MemberDAO memberDAO = new MemberDAO();
        memberDAO.memberInsert(memberVO);
    }
}
~~~

~~~java
package com.example.servlet4.sec06;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;

//@WebServlet("/MemberDeleteServlet")
@WebServlet(name = "MemberDeleteServlet", value = "/MemberDeleteServlet")
public class MemberDeleteServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }

    protected void doProcess(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        String id = request.getParameter("id");

        MemberDAO dao = new MemberDAO();
        dao.memberDelete(id);
        // select 결과 페이지로 포워딩
        response.sendRedirect("sec06/MemberSelectServlet2");
    }
}
~~~