## REST
- 브라우저에서 페이지 요청 시
  - PC에서는 페이지 전체를 다시 전송해서 표시해도 문제 없지만 스마트폰 등의 모바일 기기에서는 기존 화면은 그대로 유지하면서 필요한 내용만 추가해서 화면에 표시
- 모바일 기기가 유선 기기보다 네트워크 전송량이 떨어지므로 현재 화면은 그대로 유지하면서 필요한 데이터만 전송 받아 빠르게 표시할 필요가 있다.
  - 대표적인 예 : Ajax 이용
  - 데이터만 전송하는 기능의 표준화 필요성이 대두
  - REST 방식이 대안으로 사용됨

### REST (Representational State Transfer)
- URI가 고유한 리소스를 처리하는 공통 방식
  - 예: /board/112로 요청할 경우
    - 게시글 112번째 글만 응답 처리
- REST 방식으로 제공되는 API를 REST API(또는 RESTful API)라고 함
- 트위터와 같은 Open API에서 많이 사용됨
- 전송방식을 나타내는 메소드 속성의 값에 따라 리소스에 대한 추가 작업 요청
- REST 방식의 데이터 처리
  - 스프링 3버전
    - @ResponseBody 어노테이션 지원
  - 스프링 4버전
    - @RestController 어노테이션 이용(권장)

## Ajax (Asynchronous JavaScript and XML)
- 클라이언트에서 비동기 방식으로 자바스크립트를 이용하여
- 화면 전환 없이 서버 측에 데이터를 요청하고 응답 받을 때 사용
- HTML, XML, JSON, 텍스트 등의 데이터 처리 가능
- 웹서버 환경에서 실행

### Synchronous(동기식) / Asynchronous(비동기식) 통신
- Synchronous(동기식) 통신
  - Request 보낸 후 Request에 대한 Response를 받아서 두 두 통신 간의 트랜잭션을 맞추는 통신 방식
  - Request를 보낸 Thread는 Response가 도착하기 전까지는 다른 일 처리하지 못하고 Block 상태로  Response
  - 요청과 응답 값의 순서를 보장하고, 보낸 Request에 대한 처리 결과 값을 보장 받을 수 있기 때문에 Response에 대한 처리 결과를 보장받고 처리해야 되는 서비스에 적합
  - 신뢰성 보장
- Asynchronous(비동기식) 통신
  - Request를 보내고 Request에 대한 Response를 받지 않고도 다른 일 처리가 가능한 통신 방식
  - 처리 속도가 빠름
  - Response에 대한 처리 결과를 보장받고 처리해야 되는 서비스에는 적합하지 않음
  - 신뢰성 보장 되지 않음

### 비동기 통신
- 클라이언트에서 서버로 요청 메시지를 보낼 때, 서버에서 클라이언트로 응답을 보낼 때 본문(body)에 데이터를 포함시켜서 보냄
- 요청 본문 : RequestBody
  - @RequestBody 어노테이션 사용
    - HTTP 요청 바디를 자바 객체로 변환
    - 일반적인 GET/POST 방식의 요청 파라미터인 경우 필요 사용 안 함
- 응답 본문 : ResponseBody
  - @ResponseBody 어노테이션 사용
    - 자바 객체를 HTTP 응답 바디로 변환
    - HTTP 요청의 본문 body 부분이 그대로 전달

### Ajax 주요 메소드
- $.ajax()
  - 데이터를 서버에 HTTP POST, GET 방식으로 전송 가능
  - HTML, XML, JSON, 텍스트 유형의 데이터를 요청할 수 있는 통합적인 메소드
  - $.get(), $.post(), $.getJSON() 메소드의 기능을 하나로 합쳐 놓은 기능
  - 지정한 url 경로에 있는 파일(url 매핑 이름)의 데이터를 전송하고, 입력한 url 경로의 파일로부터 요청한 데이터를 불러 오는데 사용
- serialize()
  - 폼에 입력된 값을 쿼리 스트링 방식의 데이터로 변환하여 액션 페이지에 전송
  - 예: ‘id=abcd&pass=1234…’

~~~js
$.ajax({
	url:"전송되는 요청 url 매핑 이름",
	type:"데이터 전송 방식 (get/post)",
	data:"전송할 데이터",
	dataType:"요청하는 데이터의 타입 (html/xml/json)",
	success:function(result) {   
// 서버로부터 응답(return 값)을 result로 받음
		전송 및 요청 성공 시 실행 부분
	},
	error:function(){
		오류 발생 시 실행 부분
	},
	complete:function(){
		전송 및 요청 완료 시 실행 부분
	}
});
~~~

### 추가
- https://5bong2-develop.tistory.com/156
  - 이전 내용

#### Ajax 이용한 로그인 예제 1 - loginForm.jsp, login.js

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>로그인폼</title>
		<script src="js/jquery-3.6.0.min.js"></script>
		<script src="js/login.js"></script>
	</head>
	<body>
		  <!-- <form id="frmLogin" method="post" action="login" > -->
		  <form id="frmLogin"> <!-- Ajax 사용하는 경우  -->
			   아이디  :<input type="text" id="user_id" name="user_id"><br>
		     비밀번호:<input type="password" id="user_pw" name="user_pw" ><br>
		    <input type="submit" value="로그인">  <input type="reset" value="다시입력">
		  </form>
	</body>
</html>
~~~

~~~js
/**
 * login.js
 */
$(document).ready(function(){
    $('#frmLogin').on('submit', function(){
        event.preventDefault();

        var userId = $('#user_id').val();
        var userPw = $('#user_pw').val();

        $.ajax({
            type:"post",
            url:"login",
            data:{"id": userId,
                "pw": userPw},  /* 컨트롤러에서 받을 때 : id, pw로 받음*/
            dataType:'text',
            success:function(result){
                //alert(result);
                if(result == "success")
                    message = "로그인 성공";
                else
                    message = "로그인 실패";

                alert(message);
            },
            error:function(data, textStatus){
                alert("전송 실패");
            },
            complete:function(data, textStatus){
                alert("작업을 완료했습니다");
            }
        });
    });
});
~~~

#### Ajax 이용한 로그인 예제 2 - loginForm2.jsp, login2.js

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<html>
	<head>
		<meta charset="UTF-8">
		<title>로그인폼</title>
		<script src="js/jquery-3.6.0.min.js"></script>
		<script src="js/login2.js"></script>
	</head>
	<body>
		  <!-- <form id="frmLogin" method="post" action="login" > -->
		  <form id="frmLogin2"> <!-- Ajax 사용하는 경우  -->
			   아이디  :<input type="text" id="user_id" name="user_id"><br>
		     비밀번호:<input type="password" id="user_pw" name="user_pw" ><br>
		    <input type="submit" value="로그인">  <input type="reset" value="다시입력">
		  </form>
	</body>
</html>
~~~

~~~js
/**
 * login2.js
 */
$(document).ready(function(){
    $('#frmLogin2').on('submit', function(){
        event.preventDefault();

        var userId = $('#user_id').val();
        var userPw = $('#user_pw').val();

        $.ajax({
            type:"post",
            url:"login",
            data:{"id": userId,
                "pw": userPw},  /* 컨트롤러에서 받을 때 : id, pw로 받음*/
            dataType:'text',
            success:function(result){
                if(result == "success"){
                    alert("로그인 성공!\n상품 조회 화면으로 이동합니다.");
                    location.href="/product/listAllProduct";
                }else{
                    alert("로그인 실패");
                }
            },
            error:function(data, textStatus){
                alert("전송 실패");
            }
        });
    });
});
~~~

## 중복 체크 예제
### 추가
- https://5bong2-develop.tistory.com/156
  - 이전 내용

### IProductDAO.java

~~~java
String prdNoCheck(String prdNo); // 입력 상품번호 중복 조회
~~~

### IProductService.java

~~~java
String prdNoCheck(String prdNo); // 입력 상품번호 중복 조회
~~~

### ProductService.java

~~~java
    @Override
    public String prdNoCheck(String prdNo) {
        return dao.prdNoCheck(prdNo);
    }
~~~

### newProductForm.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<html>
  <head>
      <title>상품 등록</title>
    <script src="<c:url value='/js/jquery-3.6.0.min.js/' />"></script>
    <script src="<c:url value='/js/prdNoCheck.js/' />"></script>
  </head>
  <body>
    <h3>상풍 등록</h3>
    <form method="post" action="/product/insertProduct">
      <table>
        <tr><td>상품 번호</td><td><input type="text" name="prdNo" id="prdNo"><button id="prdNoCheckBtn">중복확인</button></td></tr>
        <tr><td>상품명</td><td><input type="text" name="prdName"></td></tr>
        <tr><td>가격 </td><td> <input type="text" name="prdPrice"></td></tr>
        <tr><td>제조회사</td><td><input type="text" name="prdCompany"></td></tr>
        <tr><td>재고 </td> <td><input type="text" name="prdStock"></td></tr>
        <tr><td colspan="2"><input type="submit" value="등록"> <input type="reset" value="취소"></td></tr>
      </table>
    </form>
  </body>
</html>
~~~

### prdNoCheck.js

~~~js
$(document).ready(function () {
    $('#prdNoCheckBtn').on('click', function () {
        event.preventDefault();
        $.ajax({
            type:"post",
            url:"prdNoCheck",
            data:{"prdNo" : $('#prdNo').val() },  /* 컨트롤러에서 받을 때 : id, pw로 받음*/
            dataType:'text',
            success:function(result){
                if(result == "no_use"){
                    alert("사용할 수 없는 번호입니다.");
                }else{
                    alert("사용 가능한 번호입니다.");
                }
            },
            error:function(data, textStatus){
                alert("전송 실패");
            }
        });
    });
});
~~~

## 상품 검색 예제

### 추가
- https://5bong2-develop.tistory.com/156
- https://5bong2-develop.tistory.com/157
- https://5bong2-develop.tistory.com/158
  - 이전 내용들

## 방법 1. Ajax / @ResponseBody 사용

### ProductService

~~~java
@Override
    public ArrayList<ProductVo> productSearch(HashMap<String, Object> map) {
        return dao.productSearch(map);
    }
~~~

### IProductService

~~~java
ArrayList<ProductVo> productSearch(HashMap<String, Object> map); // 상품 검색
~~~

### IProductDAO

~~~java
ArrayList<ProductVo> productSearch(HashMap<String, Object> map); // 상품 검색
~~~

### ProductController

~~~java
// 상품 검색 폼 이동
    @RequestMapping("/product/productSearchForm")
    public String productSearchForm() {
        return "product/productSearchForm";
    }

    // 상품 검색 폼 검색
    @ResponseBody
    @RequestMapping("/product/productSearch")
//	public ArrayList<ProductVO> productSearch(@RequestParam("type") String type,
//											  @RequestParam("keyword") String keyword) {
    public ArrayList<ProductVo> productSearch(@RequestParam HashMap<String, Object> param,
                                              Model model){
        System.out.println("a");
        ArrayList<ProductVo> prdList = service.productSearch(param);
        model.addAttribute("prdList", prdList);
        // prdList로 제대로 반화되었는지 확인하기 위한 코드
		for(int i =0; i < prdList.size(); i++) {
			ProductVo prd = (ProductVo) prdList.get(i);
			System.out.println(prd.getPrdNo());
		}
        return prdList;
    }
~~~

### ProductMapper

~~~xml
<!-- 상품 검색  -->
    <select id="productSearch" resultMap="prdResult" parameterType="hashmap">
        SELECT * FROM product WHERE
        <choose>
            <when test="type != null and type.equals('prdName')">
                prdName LIKE CONCAT('%', #{keyword}, '%')
            </when>
            <when test="type != null and type.equals('prdCompany')">
                prdCompany LIKE CONCAT('%', #{keyword}, '%')
            </when>
        </choose>
    </select>
~~~

### productSearchForm.jsp

~~~jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>상품 검색</title>
      <script src="<c:url value='/js/jquery-3.6.0.min.js/' />"></script>
      <script src="<c:url value='/js/productSearchForm.js/' />"></script>
    </head>
    <body>
      <h3>상품 검색</h3>
        <form id="prdSearchFrm">
            <select id="type" name="type">
                <option value="">검색 조건 선택</option>
                <option value="prdName">상품명</option>
                <option value="prdCompany">제조회사</option>
            </select>
            <input type="text" name="keyword">
            <input type="submit" value="검색">
        </form>
      <div id="searchResultBox"></div>
    </body>
</html>
~~~

### productSearchForm.js

~~~js
/**
 * productSearch.js
 상품 검색
 */
$(document).ready(function(){
    $('#prdSearchFrm').on('submit', function(){
        event.preventDefault();

        var formData = $(this).serialize();
        // serialize() : 폼에 입력한 값을 쿼리 스트링 방식의 데이터로 변환
        //type=prdName&keyword=노트북

        $.ajax({
            type:"post",
            url:"productSearch",
            data:formData,
            success:function(result){   // 컨트롤러에서 반환한 prdList를 result가 받음
                //alert(result.length);
                // 반환된 결과(ArrayList<ProductVO>)를  searchResultBox에 테이블 형태로 출력
                $('#searchResultBox').empty();
                $('#searchResultBox').append('<table id="resultTable" border="1" width="600">' +
                    '<tr><th>상품번호</th><th>상품명</th><th>가격</th>' +
                    '<th>제조사</th><th>재고</th><th>사진</th></tr>');
                if(result == ""){
                    $('#resultTable').append('<tr align="center"><td colspan="6">찾는 상품이 없습니다 </td></tr>');
                }else{
                    for(var i=0; i <result.length; i++){
                        $('#resultTable').append('<tr><td>' + result[i].prdNo + '</td><td>' +
                            result[i].prdName + '</td><td>' +
                            result[i].prdPrice+ '</td><td>' +
                            result[i].prdCompany + '</td><td>' +
                            result[i].prdStock + '</td><td>' +
                            '<img src="/mybatis/images/' + result[i].prdNo + '.jpg" width="30" height="20"></td></tr>');
                    }
                }
                $('#searchResultBox').append('</table>');
            },
            error:function(data, textStatus){
                alert("전송 실패");
            }
        });
    });
});
~~~

## 방법 2. @ResponseBody 없이 뷰 페이지 리턴 후, Ajax에서 현재 페이지에 결과 뷰 페이지를 삽입

### ProductService

~~~java
@Override
    public ArrayList<ProductVo> productSearch(HashMap<String, Object> map) {
        return dao.productSearch(map);
    }
~~~

### IProductService

~~~java
ArrayList<ProductVo> productSearch(HashMap<String, Object> map); // 상품 검색
~~~

### IProductDAO

~~~java
ArrayList<ProductVo> productSearch(HashMap<String, Object> map); // 상품 검색
~~~

### ProductController

~~~java
// 상품 검색 폼2 이동
    @RequestMapping("/product/productSearchForm2")
    public String productSearchForm2() {
        return "product/productSearchForm2";
    }
    // 상품 검색 폼2 검색
    @RequestMapping("/product/productSearch2")
//	public ArrayList<ProductVO> productSearch(@RequestParam("type") String type,
//											  @RequestParam("keyword") String keyword) {
    public String productSearch2(@RequestParam HashMap<String, Object> param,
                                              Model model){
        ArrayList<ProductVo> prdList = service.productSearch(param);
        model.addAttribute("prdList", prdList);
        return "product/productSearchResultView";
    }
~~~

### ProductMapper

~~~xml
<!-- 상품 검색  -->
    <select id="productSearch" resultMap="prdResult" parameterType="hashmap">
        SELECT * FROM product WHERE
        <choose>
            <when test="type != null and type.equals('prdName')">
                prdName LIKE CONCAT('%', #{keyword}, '%')
            </when>
            <when test="type != null and type.equals('prdCompany')">
                prdCompany LIKE CONCAT('%', #{keyword}, '%')
            </when>
        </choose>
    </select>
~~~

### productSearchForm2.jsp

~~~jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>상품 검색2</title>
      <script src="<c:url value='/js/jquery-3.6.0.min.js/' />"></script>
      <script src="<c:url value='/js/productSearchForm2.js/' />"></script>
    </head>
    <body>
      <h3>상품 검색</h3>
        <form id="prdSearchFrm2">
            <select id="type" name="type">
                <option value="">검색 조건 선택</option>
                <option value="prdName">상품명</option>
                <option value="prdCompany">제조회사</option>
            </select>
            <input type="text" name="keyword">
            <input type="submit" value="검색">
        </form>
      <div id="searchResultBox"></div>
    </body>
</html>
~~~

### productSearchForm2.js

~~~js
/**
 * productSearch.js
 상품 검색
 */
$(document).ready(function(){
    $('#prdSearchFrm2').on('submit', function(){
        event.preventDefault();

        var formData = $(this).serialize();
        // serialize() : 폼에 입력한 값을 쿼리 스트링 방식의 데이터로 변환
        //type=prdName&keyword=노트북

        $.ajax({
            type:"post",
            url:"productSearch2",
            data:formData,
            success:function(result){
                $('#searchResultBox').html(result);
            },
            error:function(data, textStatus){
                alert("전송 실패");
            }
        });
    });
});
~~~

### productSearchResultView.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<html>
    <head>
        <meta charset="UTF-8">
        <title>상품 검색 결과</title>
    </head>
    <body>
        <h3>상품 검색 결과2</h3>
            <table border="1" width="600">
                <tr><th>상품번호</th><th>상품명</th><th>가격</th><th>제조사</th><th>재고</th><th>사진</th></tr>
                <c:choose>
                    <c:when test="${empty prdList}">
                        <tr align="center"><td colspan="6">찾는 상품이 없습니다.</td></tr>
                    </c:when>
                    <c:otherwise>
                        <c:forEach items="${prdList }" var="prd">
                            <tr><td><a href="<c:url value='/product/detailViewProduct/${prd.prdNo}'/>">${prd.prdNo }</a></td>
                                <td>${prd.prdName }</td>
                                <td>${prd.prdPrice }</td>
                                <td>${prd.prdCompany }</td>
                                <td>${prd.prdStock }</td>
                                <td><img src="c:url value='/images/${prd.prdNo}.jpg' />" width="30" height="20"/></td></tr>
                        </c:forEach>
                    </c:otherwise>
                </c:choose>
            </table>
        <br>
        <a href="<c:url value='/' />">메인 화면으로 이동</a>
    </body>
</html>
~~~