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

### name 속성

### jQuery 사용