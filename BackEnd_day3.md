## 서블릿 포워드
- 서블릿에서 다른 서블릿이나 JSP, 웹 브라우저로 요청을 전달하는 기능
- 요청에 대한 추가 작업을 다른 서블릿에게 수행하게 하는 역할
- 요청에 포함된 정보를 다른 서블릿이나 JSP와 공유
- 요청에 정보를 포함시켜서 다른 서블릿에 전달
- 모델2 개발 시 서블릿에서 JSP로 데이터 전달하는데 사용

### 서블릿 포워드 방법
1. redirect
   - HttpServletResponse 객체의 sendRedirect() 메소드 사용
   - 웹 브라우저에게 재요청하는 방식
   - 형식 : sendRedirect(“포워드할 서블릿 또는 JSP”);
2. Refresh
   - HttpServletResponse 객체의 addHeader() 메소드 사용
   - 웹 브라우저에게 재요청하는 방식
   - 형식 : response.addHeader("Refresh", 경과시간(초);url=요청할 서블릿 또는 JSP0)
3. location
   - 자바스크립트 location 객체의 href 속성 이용
   - 자바스크립트에서 재요청하는 방식
   - 형식 : location.href = "요청할 서블릿 또는 JSP";
4. dispatch
   - 일반적으로 포워딩 기능 지칭
   - 서블릿이 직접 요청하는 방식
   - 내용은 출력 되지만 URL이 바뀌지 않음
   - RequestDispatcher 클래스의 forward() 메소드 사용
   - 형식
     - RequestDispatcher dis = request.getRequestDispatcher("포워드할 서블릿 또는 JSP");
     - dis.forward(request, response);
- redirect, refresh, location
  - 서블릿이 웹 브라우저를 거쳐 다른 서블릿이나 JSP에게 요청하는 방법
- dispatch
  - 클라이언트 거치지 않고 서블릿에서 바로 다른 서블릿에게 요청하는 방법

#### redirect 이용한 포워딩(GET 방식 : URL 사용한 포워딩) - FirstServlet01.java, SecondServlet01.java

~~~java
package com.example.servlet4.sec08;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;

@WebServlet("/sec08/first01")
public class FirstServlet01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        response.sendRedirect("second01");
    }
}
~~~

~~~java
package com.example.servlet4.sec08;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/sec08/second01")
public class SecondServlet01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        PrintWriter out = response.getWriter();
        out.print("<html><body>");
        out.print("sendRedirect를 이용한 redirect 포워딩");
        out.println("</body></html>");
    }
}
~~~

#### refresh 이용한 포워딩(GET 방식 : URL 사용한 포워딩) - FirstServlet02.java, SecondServlet02.java

~~~java
package com.example.servlet4.sec08;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;

@WebServlet("/sec08/first02")
public class FirstServlet02 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.addHeader("Refresh", "2;url=second02");
        // response.addHeader("Refresh", "시간(초);url=매핑이름");
    }
}
~~~

~~~java
package com.example.servlet4.sec08;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/sec08/second02")
public class SecondServlet02 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        PrintWriter out = response.getWriter();
        out.print("<html><body>");
        out.print("refresh를 이용한 포워딩");
        out.println("</body></html>");
    }
}
~~~

#### location 이용한 포워딩(GET 방식 : URL 사용한 포워딩) - FirstServlet03.java, SecondServlet03.java

~~~java
package com.example.servlet4.sec08;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/sec08/first03")
public class FirstServlet03 extends HttpServlet {
    private static final long serialVersionUID = 1L;
    // location을 이용한 포워딩
    // 자바스크립트의 location 객체 사용
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        PrintWriter out = response.getWriter();
        out.print("<script type='text/javascript'>");
        out.print("location.href='second03';");
        out.println("</script>");
    }
}
~~~

~~~java
package com.example.servlet4.sec08;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/sec08/second03")
public class SecondServlet03 extends HttpServlet {
    private static final long serialVersionUID = 1L;
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        PrintWriter out = response.getWriter();
        out.print("<html><body>");
        out.print("location을 이용한 포워딩");
        out.println("</body></html>");
    }
}
~~~

#### 포워딩 하면서 데이터 전달(redirect 이용)(GET 방식 : URL 사용한 포워딩)  - FirstServlet04.java, SecondServlet04.java

~~~java
package com.example.servlet4.sec08;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/sec08/first04")
public class FirstServlet04 extends HttpServlet {
    private static final long serialVersionUID = 1L;
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.sendRedirect("second04?name=hong");
    }
}
~~~

~~~java
package com.example.servlet4.sec08;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/sec08/second04")
public class SecondServlet04 extends HttpServlet {
    private static final long serialVersionUID = 1L;
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        PrintWriter out = response.getWriter();
        // url 뒤에 붙어서 전송된 데이터 받기
        String name = request.getParameter("name");
        out.print("<html><body>");
        out.print("redirect 이용한 포워딩으로 데이터 전달 받기<br>");
        out.print("이름 : " + name);
        out.println("</body></html>");
    }
}
~~~

#### dispatch 이용한 포워딩(GET 방식 : URL 사용한 포워딩) - FirstServlet05.java, SecondServlet05.java

~~~java
package com.example.servlet4.sec08;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;

@WebServlet("/sec08/first05")
public class FirstServlet05 extends HttpServlet {
    private static final long serialVersionUID = 1L;
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        RequestDispatcher dispatcher = request.getRequestDispatcher("second05?name=lee");
        dispatcher.forward(request, response);
    }
}
~~~

~~~java
package com.example.servlet4.sec08;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/sec08/second05")
public class SecondServlet05 extends HttpServlet {
    private static final long serialVersionUID = 1L;
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        PrintWriter out = response.getWriter();
        // url 뒤에 붙어서 전송된 데이터 받기
        String name = request.getParameter("name");
        out.print("<html><body>");
        out.print("dispatcher 이용한 포워딩으로 데이터 전달 받기<br>");
        out.print("이름 : " + name);
        out.println("</body></html>");
    }
}
~~~

### GET 방식으로 데이터 전달 시 문제
- 대량의 데이터를 전달할 때 GET방식의 문제
  - 길이 제한, 안전성, 불편 등
- 바이딩(binding) 기능 사용으로 해결
  - 웹 프로그래밍 실행 시 자원(데이터)을 서블릿 객체에 저장하는 방법 사용
  - 저장된 데이터는 서블릿이나 JSP에서 공유
  - 방법
    - 포워딩할 때 setAttribute(“바인딩이름”, 데이터) 메소드 사용해서 바인딩이름과 데이터를 묶어서 설정한 후 포워딩된 문서에서 getAttribute("바인딩 이름") 메소드를 이용해서 바인딩된 데이터를 추출해서 사용
  - redirect 방식으로는 서블릿에서 바인딩한 데이터를 다른 서블릿으로 전송할 수 없다.
    - dispatch 포워딩 방법일 경우에만 바인딩 가능

#### redirect 방식을 통한 바인딩 예제(바인딩 안되는 예시) - FirstServlet06.java, SecondServlet06.java

~~~java
package com.example.servlet4.sec08;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;

// sendRedirect() 사용해서 바인딩
@WebServlet("/sec08/first06")
public class FirstServlet06 extends HttpServlet {
    private static final long serialVersionUID = 1L;
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");

        request.setAttribute("address", "서울시 강남구");
        response.sendRedirect("second06");
    }
}
~~~

~~~java
package com.example.servlet4.sec08;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/sec08/second06")
public class SecondServlet06 extends HttpServlet {
    private static final long serialVersionUID = 1L;
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");
        PrintWriter out = response.getWriter();
        // url 뒤에 붙어서 전송된 데이터 받기
        String address = (String)request.getAttribute("address");
        out.print("<html><body>");
        out.print("redirect 이용한 바인딩<br>");
        out.print("주소 : " + address);
        out.println("</body></html>");
//        redirect 이용한 바인딩
//        주소 : null
    }
}
~~~

#### dispatch 방식을 통한 바인딩 예제 - FirstServlet07.java, SecondServlet07.java

~~~java
package com.example.servlet4.sec08;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;

@WebServlet("/sec08/first07")
public class FirstServlet07 extends HttpServlet {
    private static final long serialVersionUID = 1L;
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");

        request.setAttribute("address", "서울시 강남구");
        request.setAttribute("name", "홍길동");
        RequestDispatcher requestDispatcher = request.getRequestDispatcher("second07");
        requestDispatcher.forward(request, response);
    }
}
~~~

~~~java
package com.example.servlet4.sec08;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/sec08/second07")
public class SecondServlet07 extends HttpServlet {
    private static final long serialVersionUID = 1L;
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");

        PrintWriter out = response.getWriter();
        // url 뒤에 붙어서 전송된 데이터 받기
        String address = (String)request.getAttribute("address");
        String name = (String)request.getAttribute("name");
        out.print("<html><body>");
        out.print("dispatch 이용한 바인딩<br>");
        out.print("주소 : " + address + "<br>");
        out.print("이름 : " + name);
        out.println("</body></html>");
//        URL 변경 없음
//        http://localhost:8080/sec08/first07
    }
}
~~~

#### 데이터베이스의 회원 정보를 ArrayList객체에 저장 후 바인딩 - MemberVO.java, MemberDAO.java, MemberBindingServlet.java, MemberViewServlet.java

~~~java
package com.example.servlet4.sec09;

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
package com.example.servlet4.sec09;

import javax.naming.Context;
import javax.naming.InitialContext;
import javax.sql.DataSource;
import java.sql.Connection;
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
package com.example.servlet4.sec09;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.util.ArrayList;

@WebServlet("/sec09/memBinding")
public class MemberBindingServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doProcess(request, response);
    }
    protected void doProcess(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        MemberDAO dao = new MemberDAO();
        ArrayList<MemberVO> memList = dao.memberSelect();

        request.setAttribute("memList", memList); // name, data
        RequestDispatcher requestDispatcher = request.getRequestDispatcher("memView");
        requestDispatcher.forward(request, response);
    }
}

~~~

~~~java
package com.example.servlet4.sec09;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;

@WebServlet("/sec09/memView")
public class MemberViewServlet extends HttpServlet {
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
//      비즈니스 로직 처리 : 바인딩 된 값 추출
        List memList = (List)request.getAttribute("memList");
//        ArrayList<MemberVO> memList = (ArrayList<MemberVO>)request.getAttribute("memList");
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

## 쿠키와 세션
- 클라이언트와 서버 간에 정보를 교환하는데 클라이언트 PC 또는 서버의 메모리에 저장해 두고 사용하면 프로그램 속도를 향상시킬 수 있음
### HTTP 프로토콜
- 서버-클라이언트 통신 시 stateless 방식으로 통신
- 브라우저에서 새 웹페이지를 열면 기존의 웹페이나 서블릿에 관한 어떤 연결 정보도 유지 않음
- 새로 열린 페이지에서 어떤 정보도 알 수 없음
- 페이지가 서로 독립적이어서 서로의 상태를 알 수 없음
- 웹 페이지 사이 또는 서블릿 간 상태나 정보를 공유하려면 웹 페이지를 연결시키는 기능 필요
  - 세션 트래킹이라고 함
    - 방법
      1. \<hidden> 태그 사용
           - \<input type=’hidden’ value=’${id}’>
           - 현재 페이지에 데이터 숨겨놓고 연결된 다음 페이지로 데이터를 보내는 방법
           - 두 웹페이지가 데이터 공유
           - request.getParameter()로 받아서 사용할 수 있음
           - GET 방식으로 전송 : 데이터 노출, 길이 제한, 보안 문제
      2. URL Rewrite
           - GET 방식으로 전송할 때 데이터가 URL 뒤에 붙여서 다음 페이지로 전송
           - second02?name=lee
           - GET 방식으로 전송 : 데이터 노출, 길이 제한, 보안 문제
      3. 쿠키 
      #### 사진있음
           - 클라이언트 PC의 Cookie 파일에 정보를 저장한 후 웹 페이지 공유
           - 서버 측에서 클라이언트 측에 상태 정보를 저장하고 추출하기 위한 메커니즘
           - 서버에서 생성하여, 클라이언트 측에 저장됨
           - 서버에 요청할 때마다 쿠키의 속성 값을 참조하거나 변경
           - 크기는 4kb 용량
           - 클라이언트에 300개까지 저장 가능
           - 하나의 도메인 당 20개의 값만 저장
           - 클라이언트에 저장되므로 보안상 문제 발생
             - 따라서 민감한 정보는 쿠키 내에 저장하지 않음
           - 쿠키는 사용자가 거부할 수 있으며 256문자 이하의 text 데이터만 저장됨
           - __생성 및 저장 과정__
             - __서버에서 쿠키 생성__
               - Cookie cookie = new Cookie(이름, 값); (Cookie 클래스로부터 쿠키 객체 생성)
             - __속성 설정__
               - setter 사용해서 쿠키 객체의 유효기간 설정
                 - cookie.setMaxAge(유효기간);
             - __클라이언트에 전송되어 자장__
               - response 내장 객체의 addCookie() 메소드로 전송
             - __쿠키 관련 주요 메소드__
               - setMaxAge() : 유효 기간 설정
               - setValue() : 쿠키 값 설정
               - sevVersion() : 쿠키 버전 설정
               - setPath(0 : 쿠키 사용의 유효 디렉터리 설정
               - getMaxAge() : 유효 기간 반환
               - getName() : 쿠키 이름 반환
               - getValue() : 쿠키 값 반환
               - __쿠키 제거__ 
                 - cookie.setMaxAge(0) 으로 설정
               - __클라이언트에 전송되어 변경된 값으로 저장__
                 - response.addCookie(cookie)
               - __쿠키 유형__
                 - __Persistence 쿠키__
                   - setMaxAge(양수) 메소드를 사용해서 양수값으로 지정해서 파일로 저장하면 지속해서 남아있음
                   - 유효 기간 동안 지속됨
                 - __Session 쿠키__
                   - 브라우저가 사용하는 메모리에 생성되는 쿠키로 브라우저가 종료되면 메모리의  Session 쿠키도 자동으로 소멸
                   - setMaxAge(음수) : Session 쿠키로 생성
      4. 세션
            - 서버 메모리에 정보를 저장한 후 웹페이지 공유
            - 클라이언트와 웹 서버 간에 네트워크로 연결이 지속적으로 유지되고 있는 상태
            - 쿠키와 마찬가지로 서버와의 관계를 유지하기 위한 수단
            - 쿠키와 달리 클라이언트 측에 저장되는 것이 아니라 서버 상에 객체로 존재
              - 따라서 세션은 서버에서만 접근이 가능하여 보안이 좋음
            - 서버에서 사용자의 정보를 유지 관리
            - 사용자 인증 후 여러 페이지에 걸쳐 정보를 공유해서 사용할 수 있게 해줌
            - Session은 서버 측에서만 설정이 가능
            - 브라우저 당 한 개씩 생성
            - __세션 생성 및 사용 과정__
              - 클라이언트가 서버에 페이지 요청
              - Session 자동 생성
              - Session 속성 설정
                - session 내부 객체의 메소드 사용
            - __세션 ID__
              - 클라이언트가 처음 접속하면 서버(컨테이너)로 부터 유일한 ID를 부여 받게 되는데 이를 세션 ID라고 하고 클라이언트가 재 접속했을 때 클라이언트를 구분하기 위한 수단이 된다.
              - 서블릿에서 생성된 세션 id는, 브라우저로 전송되어 세션 쿠키에 쿠키 이름 sessionID로 저장됨
              - F12 개발자도구 / Application / Cookies에서 확인 가능
            - __세션 관련 메소드__
              - setAttribute(이름, 값) : 세션 이름과 값 설정
              - getAttribute(이름) : 이름에 해당된 값 반환
              - getAttributeNames() : 모든 세션 이름 반환
              - getId() : 세션 ID 반환
              - isNew() : 새로 생성되었는지 여부 반환
              - getMaxInactiveInterval() : 설정된 유효기간 반환
              - removeAttribute() : 설정된 속성값 제거
              - invalidate() : 실행 중인 세션 종료. 모든 데이터 삭제. 로그아웃 시 사용
              - isRequestedSessionIdValid() : 유효한 세션 ID가 있는 여부 반환
            - __세션 값 설정__
              - session.setAttribute(“SID”, “abcd”)
              - session : 내장 객체 
            - __세션 값 알아오기__
              - Object obj = session.getAttribute(“SID”);
              - Object 타입 반환 (사용 시 형 변환)
            - __세션 속성 제거__
              - session.invalidate()
              - 또는 설정된 유효 기간이 만료되면 종료
            - __세션 무효화__
              - invalidate() 메소드를 사용해서 바로 무효화시킬 수 있음
              - web.xml 파일에서 session-timeout 설정해서 시간을 정할 수 있음
              - setMaxInactiveInterval()를 사용해서 시간 지정 가능
              - 기본 세션은 마지막 요청으로부터 30분 경과 후 자동 소멸됨
                - 세션 유효 기간을 따로 설정하지 않으면 톰캣에서 설정한 기본 유효 시간 30분이 적용

#### hidden 방식 예제 - LoginHiddenServlet.java, login-hidden.html

~~~java
package com.example.servlet4;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;
import java.net.URLEncoder;

@WebServlet("/loginrewrite")
public class LoginRewriteServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");
        PrintWriter out = response.getWriter();

        String user_id = request.getParameter("user_id");
        String user_pw = request.getParameter("user_pw");
        String user_address = request.getParameter("user_address");
        String user_email = request.getParameter("user_email");
        String user_hp = request.getParameter("user_hp");
        if (user_id != null && user_id.length() != 0) {
            String data = "<html><body>";
            data += "안녕하세요!<br> 로그인하셨습니다.<br><br>";
            data += "아이디 : " + user_id + "<br>";
            data += "비밀번호 : " + user_pw + "<br>";
            data += "주소 : " + user_address + "<br>";
            data += "이메일 : " + user_email + "<br>";
            data += "휴대전화 : " + user_hp;
            out.print(data);

            // URL Rewriting 방식 이용
            user_address = URLEncoder.encode(user_address, "utf-8");
           // 인코딩 하면 서울시+종로구 라고 나오고 하지 않으면 서울시%종로구 라고 나옴
            out.print("<br><br><a href='/second?user_id=" + user_id
                    + "&user_pw=" + user_pw
                    + "&user_address=" + user_address
                    + "'>두 번째 서블릿으로 보내기</a>");
            data = "</body></html>";
        }
        else {
            out.println("로그인 하지 않았습니다. <br><br>");
            out.println("다시 로그인 하세요. <br><br>");
            out.println("<a href='login-rewrite.html'>로그인 창으로 이동</a>");
        }
    }
}

~~~

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form name="frmLogin" method="post" action="loginHidden" >
        아이디  :<input type="text" name="user_id"><br>
        비밀번호:<input type="password" name="user_pw" ><br>
        <input type="submit" value="로그인">  <input type="reset" value="다시입력">
        <!-- 히든 태그 삽입-->
        <input type="hidden" name="user_address" value="서울시 종로구">
        <input type="hidden" name="user_email" value="test@naver.com">
        <input type="hidden" name="user_hp" value="010-1111-1111">
    </form>
</body>
</html>
~~~

#### URL Rewriting 방식 예제 - LoginRewriteServlet.java, SecondServlet.java, login-rewrite.html

~~~java
package com.example.servlet4;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;
import java.net.URLEncoder;

@WebServlet("/loginrewrite")
public class LoginRewriteServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");
        PrintWriter out = response.getWriter();

        String user_id = request.getParameter("user_id");
        String user_pw = request.getParameter("user_pw");
        String user_address = request.getParameter("user_address");
        String user_email = request.getParameter("user_email");
        String user_hp = request.getParameter("user_hp");
        if (user_id != null && user_id.length() != 0) {
            String data = "<html><body>";
            data += "안녕하세요!<br> 로그인하셨습니다.<br><br>";
            data += "아이디 : " + user_id + "<br>";
            data += "비밀번호 : " + user_pw + "<br>";
            data += "주소 : " + user_address + "<br>";
            data += "이메일 : " + user_email + "<br>";
            data += "휴대전화 : " + user_hp;
            out.print(data);

            // URL Rewriting 방식 이용
            user_address = URLEncoder.encode(user_address, "utf-8");
           // 인코딩 하면 서울시+종로구 라고 나오고 하지 않으면 서울시%종로구 라고 나옴
            out.print("<br><br><a href='/second?user_id=" + user_id
                    + "&user_pw=" + user_pw
                    + "&user_address=" + user_address
                    + "'>두 번째 서블릿으로 보내기</a>");
            data = "</body></html>";
        }
        else {
            out.println("로그인 하지 않았습니다. <br><br>");
            out.println("다시 로그인 하세요. <br><br>");
            out.println("<a href='login-rewrite.html'>로그인 창으로 이동</a>");
        }
    }
}
~~~

~~~java
package com.example.servlet4;

import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.*;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet("/second")
public class SecondServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");
        PrintWriter out = response.getWriter();

        String user_id = request.getParameter("user_id");
        String user_pw = request.getParameter("user_pw");
        String user_address = request.getParameter("user_address");

        out.print("<html><body>");
        if(user_id != null && user_id.length() != 0) {
            out.println("이미 로그인 상태입니다. <br><br>");
            out.println("첫 번째 서블릿에서 넘겨준 아이디 : " + user_id + "<br>");
            out.println("첫 번째 서블릿에서 넘겨준 비밀번호 : " + user_pw + "<br>");
            out.println("첫 번째 서블릿에서 넘겨준 주소 : " + user_address + "<br>");
            out.print("</body></html>");
        }
        else {
            out.println("로그인 하지 않았습니다. <br><br>");
            out.println("다시 로그인 하세요. <br><br>");
            out.println("<a href='login-rewrite.html'>로그인 창으로 이동</a>");
        }
    }
}
~~~

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form name="frmLogin" method="post" action="loginrewrite" >
        아이디  :<input type="text" name="user_id"><br>
        비밀번호:<input type="password" name="user_pw" ><br>
        <input type="submit" value="로그인">  <input type="reset" value="다시입력">
        <!-- hidden 태그  -->
        <input type="hidden" name="user_address" value="서울시 종로구" >
        <input type="hidden" name="user_email" value="test@naver.com" >
        <input type="hidden" name="user_hp" value="010-1111-1111" >
    </form>
</body>
</html>
~~~

#### 쿠키 방식 예제 - popUp.html, popUpTest.html

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>팝업창</title>
</head>
<script>
    function setPopUpStart(obj) {
        if(obj.checked == true) {
            var expireDate = new Date();
            // alert(expireDate); // 오늘 날짜
            var days = 1;
            expireDate.setDate(expireDate.getDate() + days);
            // alert(expireDate); // 내일 날짜
            // 쿠키 값 설정 : 쿠키 이름, 패스, 유효 기간
            document.cookie = "notShowPop=" + "true" + ";path=/;expires=" + expireDate.toGMTString();
            // 팝업창 닫기
            window.close();
        }
    }
</script>
<body>
  알림 팝업창입니다.<br><br><br><br><br><br><br>
<form>
  <input type="checkbox" onclick="setPopUpStart(this)">오늘 더 이상 팝업창 띄우지 않기
</form>
</body>
</html>
~~~

~~~html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>popUpTest</title>
    <script type="text/javascript">
        // 시작 시 페이지 로드 함수 호출
        window.onload = pageLoad;

        /* 페이지 로드 함수 : 팝업창(popUp.html) 띄우는 함수 */
        function pageLoad(){
            //  쿠키 읽어 오는 함수  getCookieValue() 함수 호출해서 저장된 쿠키 읽어 오기
            var notShowPop = getCookieValue();

            // 읽어 온 쿠키 값이 "true"가 아니면 popUp.html 열기
            if(notShowPop != "true"){
                window.open("popUp.html", "pop", "width=400,height=500, " +
                    "history=no,resizable=no,status=no,scrollbars=yes,menubar=no");
            }
        }
        /* 쿠키 읽어 함수 */
        function getCookieValue(){
            var result = "false";

            // 쿠키 존재 여부 확인 : 쿠키가 존재하면
            if(document.cookie != ""){
                // 구분자를 세미콜론(;)으로 해서 각 값을 배열로 저장
                cookie = document.cookie.split(";");
                for(var i=0; i<cookie.length; i++){
                    //구분자를 =으로 해서 각 값을 배열로 저장
                    element = cookie[i].split("=");
                    value = element[0]; // 쿠키 이름 (배열 첫 번째 요소)
                    //value = value.replace(/^\s*/,'');// 앞 공백 제거 정규식

                    // 쿠키 이름이 notShowPop 이면
                    if(value == "notShowPop") {
                        result = element[1]; //쿠키 값 가져오기 ("true") (배열 두 번째 요소)
                    }
                }
            }
            return result;
        }
        // 쿠키 삭제하는 함수 : 유효 기간을 -1로 설정
        function deleteCookie(){
            document.cookie = "notShowPop=" + "false" + ";path=/;expires=-1";
        }

    </script>
</head>
<body>
<form>
    <input type="button" value="쿠키삭제" onClick="deleteCookie()">
</form>
</body>
</html>
~~~

#### 세션 방식 예제 1(세션 아이디, 최소 생성 시간, 접근 시간, 유효 시간, isNet() 확인) - SessionTest.java

~~~java
@WebServlet("/sess")
public class SessionTest extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		HttpSession session = request.getSession();

		out.println("세션 아이디 : " + session.getId() + "<br>");
		out.println("최초 세션 생성 시각 : " + new Date(session.getCreationTime()) + "<br>");
		out.println("최근 세션 접근 시각 : " + new Date(session.getLastAccessedTime()) + "<br>");
		out.println("세션 유효 시간 : " + session.getMaxInactiveInterval() + "<br>");

		if(session.isNew()) {
			out.print("새 세션이 만들어졌습니다");
		}
	}
}
~~~

#### 세션 방식 예제 2(세션 유효 시간 5초로 설정) - SessionTest2.java

~~~java
@WebServlet("/sess2")
public class SessionTest2 extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		HttpSession session = request.getSession();

		out.println("세션 아이디 : " + session.getId() + "<br>");
		out.println("최초 세션 생성 시각 : " + new Date(session.getCreationTime()) + "<br>");
		out.println("최근 세션 접근 시각 : " + new Date(session.getLastAccessedTime()) + "<br>");

		out.println("기본 세션 유효 시간 : " + session.getMaxInactiveInterval() + "<br>");
		session.setMaxInactiveInterval(5);		// 세션 유효 시간을 5초로 설정
		out.println("세션 유효 시간 : " + session.getMaxInactiveInterval() + "<br>");

		if(session.isNew()) {
			out.print("새 세션이 만들어졌습니다");
		}
	}
}
~~~

#### 세션 방식 예제 3(invalidate() 호출해서 사용자가 세션을 강제로 삭제) - SessionTest3.java

~~~java
@WebServlet("/sess3")
public class SessionTest3 extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		HttpSession session = request.getSession();

		out.println("세션 아이디 : " + session.getId() + "<br>");
		out.println("최초 세션 생성 시각 : " + new Date(session.getCreationTime()) + "<br>");
		out.println("최근 세션 접근 시각 : " + new Date(session.getLastAccessedTime()) + "<br>");
		out.println("세션 유효 시간 : " + session.getMaxInactiveInterval() + "<br>");

		if(session.isNew()) {
			out.print("새 세션이 만들어졌습니다");
		}
		session.invalidate();// 생성된 세션 객체를 강제로 삭제
	}
}
~~~

#### 세션 이용해서 로그인/로그아웃 기능 - sessionLogin.html, LoginLogout.java, SessionLogout.java

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>로그인창</title>
	</head>
	<body>
	  <form name="frmLogin" method="post" action="logInOut" >
		   아이디  :<input type="text" name="user_id"><br>
	     비밀번호:<input type="password" name="user_pw" ><br>
	    <input type="submit" value="로그인">  <input type="reset" value="다시입력">	    
	  </form>
	</body>
</html>
~~~

~~~java
@WebServlet("/logInOut")
public class LoginLogout extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doProcess(request, response);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doProcess(request, response);
	}

	protected void doProcess(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		request.setCharacterEncoding("utf-8");
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		HttpSession session = request.getSession();

		String user_id = request.getParameter("user_id");
		String user_pw = request.getParameter("user_pw");

		// 처음 접속이면
		if(session.isNew()) {
			// user_id 입력 값이 있으면
			if(user_id != null) {
				// SID 이름, user_id 값으로 세션 변수 설정
				session.setAttribute("SID", user_id);
				// 다시 실행시켜서 SID 확인
				out.print("<a href='logInOut'>로그인 상태 확인</a>");
			}else { // user_id 입력 값이 없으면
				out.print("<a href='sessionLogin.html'>다시 로그인 하세요!</a>");
				session.invalidate();
			}

		} else {   //아니고 세션이 있으면
			user_id = (String) session.getAttribute("SID");
			if(user_id != null && user_id.length() != 0) {
				out.print("안녕하세요 " + user_id + "님!!");
				out.print("<br><a href='logout'>로그아웃</a>");
			} else {
				out.print("<a href='sessionLogin.html'>다시 로그인 하세요!</a>");
				session.invalidate();
			}
		}
	}
}
~~~

~~~java
@WebServlet("/logout")
public class SessionLogout extends HttpServlet {
	private static final long serialVersionUID = 1L;
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		HttpSession session = request.getSession();

		session.invalidate(); // 세션 무효화

		out.print("로그아웃 되었습니다. <br>");
		out.print("<a href='sessionLogin.html'>로그인</a>");
	}
}
~~~