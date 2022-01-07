## 컨트롤러와 요청 처리
### View의 요청 경로(Path) 설정
- Controller에서

~~~java
   @RequestMapping("접속할 URL")
   public String index(Model model) {
      return "jsp 파일 이름";
   }
~~~

### 스프링 컨트롤러
- 스프링 컨트롤러는 빈으로 등록되어야 한다.
- 비즈니스 로직이 실행되기 위해 비즈니스 객체를 의존성 주입(DI) 해야 함
- 클래스 생성하고 @Controller 어노테이션 붙임
- @RequestMapping 어노테이션을 사용하여 url 맵핑
  - 요청 처리 메소드 구현
- 뷰 페이지 이름 반환 : jsp 파일명

#### 간단한 Controller 예제 - HelloController.java

~~~java
@Controller
public class HelloController {
//    @RequestMapping("/")
//    public String index(Model model) {
//        return "index";
//    }
    @RequestMapping("/home")
    public String home(Model model) {
        return "home";
    }
}
~~~

## 데이터 전송
- Controller -> View 페이지
- View 페이지 -> Controller

### Controller -> View 페이지로 데이터 전송
- Model
  - Model에 Attribute를 추가하기 위해 고안
  - key / value 형태로 값을 임시 저장
  - Controller에서 Model에 데이터를 저장하고 View 이름을 return 하면 View 페이지로 Model 이 전달되고 View 페이지에서 key를 사용해서 Model에 저장된 data 사용
  - 컨트롤러에서 Model 인터페이스 객체 사용
    - Model 객체를 메소드의 파라미터로 받아서 데이터를 뷰로 전달
  - public String index(Model model) 
    - model.addAttribute(“name”, “홍길동”);
  - 컨트롤러에서 뷰로 데이터 전달되면 뷰에서
    - ${name}
- ModelAndView

#### Controller -> View 페이지로 데이터 전송 예제 : Model 사용 - BookController.java, bookInforView.jsp

~~~java
@RequestMapping("/bookInfoView1")
	public String showBookInfo(Model model) {
		model.addAttribute("title","스프링 프레임 워크");
		model.addAttribute("price", 20000);
		
		return "book/bookInfoView";
	}
~~~

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>bookInforView</title>
	</head>
	<body>
		도서 제목: ${title }	<br>
		도서 가격: ${price }
	</body>
</html>
~~~

### @RequestMapping 다중 매핑
- 한 개의 메소드로 여러 요청 경로 처리 가능
- @RequestMapping(value={“요청경로1”, “요청경로2”})

#### @RequestMapping 다중 매핑 예제 - BookController.java, bookInforView.jsp

~~~java
// 다중 매핑
	@RequestMapping(value= {"/bookInfoView3", "/bookInfoView4"})
	public String showBookInfo34(HttpServletRequest request, Model model) {
		
		if(request.getServletPath().equals("/bookInfoView3")) {
			model.addAttribute("title", "영어 회화");
			model.addAttribute("price", 30000);
		}else if(request.getServletPath().equals("/bookInfoView4")) {
			model.addAttribute("title", "수학 정석");
			model.addAttribute("price", 40000);
		}
		return "book/bookInfoView";
	}
~~~

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>bookInforView</title>
	</head>
	<body>
		도서 제목: ${title }	<br>
		도서 가격: ${price }
	</body>
</html>
~~~

### View 페이지에서 컨트롤러로 데이터 전송
- Form을 통한 데이터 전송
  - (1) getParameter() 메소드 사용
  - (2) @RequestParam 어노테이션 사용
  - (3) Command 객체 이용
- url을 통한 데이터 전송
  - @PathVariable 어노테이션 사용

#### Form을 통한 데이터 전송 : getParameter() 메소드 사용 연습문제 - ProductController.java, productForm.jsp

~~~java
@RequestMapping("product/newProduct")
	public String insertProduct(HttpServletRequest request, Model model) {
		String prdNo = request.getParameter("prdNo");
		String prdName = request.getParameter("prdName");
		String prdPrice = request.getParameter("prdPrice");
		String prdMaker = request.getParameter("prdMaker");
		String prdDate = request.getParameter("prdDate");
		String prdQty = request.getParameter("prdQty");
		
		model.addAttribute("prdNo",prdNo);
		model.addAttribute("prdName",prdName);
		model.addAttribute("prdPrice",prdPrice);
		model.addAttribute("prdMaker",prdMaker);
		model.addAttribute("prdDate",prdDate);
		model.addAttribute("prdQty",prdQty);
		
		return "product/productResult";
	}
~~~

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>상품 등록</title>
	</head>
	<body>
		<h3>상풍 등록</h3>
		
		<form method="post" action="/product/newProduct">
			상품 번호 : <input type="text" name="prdNo"><br>
			상품명 : <input type="text" name="prdName"><br>
			가격 : <input type="text" name="prdPrice"><br>
			제조회사 : <input type="text" name="prdMaker"><br>
			제조일 : <input type="date" name="prdDate"><br>
			재고 : <input type="text" name="prdQty">
			<input type="submit" value="등록"><input type="reset" value="취소">
		</form>
	</body>
</html>
~~~

#### Form을 통한 데이터 전송 : @RequestParam 어노테이션 사용 예제 - StudentController.java, studentForm.jsp

~~~java
@RequestMapping("/student/newStudent2")
	public String insertStrudent2(@RequestParam("no") String no,
								  @RequestParam("name") String name,
								  @RequestParam("year") String year,
								  Model model) {

		model.addAttribute("no", no);
		model.addAttribute("name", name);
		model.addAttribute("year", year);

		return "student/studentResult";
	}
~~~

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>학생 정보 등록</title>
	</head>
	<body>
			<h3>학생 정보 등록</h3>
			
			<form method="post" action="/student/newStudent2">
				학번 : <input type="text" name="no"><br>
				성명 : <input type="text" name="name"><br>
				학년 : <input type="text" name="year"><br>			
				<input type="submit" value="등록"> <input type="reset" value="취소">
			</form>
	</body>
</html>
~~~

#### Command 객체 이용 - StudentController.java, Student.java, studentCmdResult.jsp

~~~java
	@RequestMapping("/student/newStudent3")
	public String insertStudent3(Student student) {
		// command 객체는 자동으로 View Model에 등록됨 : Model 등록 필요 없음.
		return "student/studentCmdResult";
	}
~~~

~~~java
package controller;

public class Student {
    private String no;
    private String name;
    private String year;

    public String getNo() {
        return no;
    }
    public void setNo(String no) {
        this.no = no;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String getYear() {
        return year;
    }
    public void setYear(String year) {
        this.year = year;
    }
}
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
  학번 : ${student.no} <br>
  성명 : ${student.name} <br>
  학년 : ${student.year} <br>
</body>
</html>
~~~

#### Command 객체 이용(이름 변경) - StudentController.java, Student.java, studentCmdRenameResult.jsp

~~~java
// Command 객체 이름 변경 : @ModelAttribute 어노테이션 사용
	@RequestMapping("/student/newStudent4")
	public String insertStudent4(@ModelAttribute("stdInfo") Student student) {
		// command 객체는 자동으로 View Model에 등록됨 : Model 등록 필요 없음.
		return "student/studentCmdRenameResult";
	}
~~~

~~~java
package controller;

public class Student {
    private String no;
    private String name;
    private String year;

    public String getNo() {
        return no;
    }
    public void setNo(String no) {
        this.no = no;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String getYear() {
        return year;
    }
    public void setYear(String year) {
        this.year = year;
    }
}
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
학번 : ${stdInfo.no} <br>
성명 : ${stdInfo.name} <br>
학년 : ${stdInfo.year} <br>
</body>
</html>
~~~

#### url을 통한 데이터 전송 @PathVariable 어노테이션 사용 - studentForm.jsp, studentResult.jsp, StudentController.java

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>학생 정보 등록</title>
	</head>
	<body>
			<h3>학생 정보 등록</h3>
			
			<form method="post" action="/student/newStudent">
				학번 : <input type="text" name="no"><br>
				성명 : <input type="text" name="name"><br>
				학년 : <input type="text" name="year"><br>			
				<input type="submit" value="등록"> <input type="reset" value="취소">
			</form>
	</body>
</html>
~~~

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Student Result</title>
	</head>
	<body>
			<h3>학생 정보 등록 결과</h3>
			학번 : ${no } <br>
			성명 : ${name } <br>
			학년 : ${year }

	<br><br>
	url을 통한 데이터 전송 <br>
	<a href="/student/studentModify/${no}" > ${no}</a>
	</body>
</html>
~~~

~~~java
	// 4. url을 통한 데이터 전송 @PathVariable 사용
	@RequestMapping("/student/studentModify/{stdNo}")
	public String studentModify(@PathVariable String stdNo) {
		// 수정 처리헸다 가정하고 home 페이지로 이동
		System.out.println(stdNo);
//		return "jsp/home"; // URL에 입력 값이 뜨는 이슈 발생.
		return "redirect:/";
//		"redirect:다시 이동할 URL"
//		다시 이동할 URL로 가서 Controller가 작동하는 알고리즘 수행 후 return에 있는 페이지로 이동함.
	}
}
~~~

=================================================================================================

## 스프링에서 데이터베이스 연동 : MyBatis 사용해서 DB 연동

### MyBatis (마이바티스)
- ORM(Object Relational Mapping : 객체 관계 매핑) 프레임워크
- 자바에서 JDBC를 이용할 경우 Java 언어와 SQL언어가 한 파일에 존재해서 재사용성이 좋지 않음
  - MyBatis는 JDBC의 이런 단점을 개선하여 SQL 명령어를 별도의 XML 파일에 분리하여 SQL 명령어와 자바 객체를 매핑해주는 기능을 제공
  - SQL 명령어를 재사용
- MyBatis 특징
  - SQL 명령어를 자바 코드에서 분리하여 별도의 XML 파일에서 관리
  - XML을 매퍼(Mapper)로 부름

## 사진

### IntelliJ Mybatis, JDBC 연결

- pom.xml 의존성 설정
- 데이터베이스
  - Spring JDBC 의존성 : spring-jdbc
  - Connection Pool 의존성 : commons-dbcp
  - MySQL 의존성 : mysql-connector-java
- MyBatis
  - mabatis
  - mybatis-spring

#### pom.xml
~~~xml
<!-- pom.xml -->
<dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.2.19.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>commons-dbcp</groupId>
            <artifactId>commons-dbcp</artifactId>
            <version>1.4</version>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.27</version>
        </dependency>

        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.9</version>
        </dependency>

        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>2.0.6</version>
        </dependency>

    </dependencies>
~~~

- cmd + ; -> Libraries에서 + 클릭 후 Java -> jdbc커넥터.jar 파일 찾아서 등록 -> Artifacts에서 모두 더블클릭해서 등록

- 프로퍼티 파일 작성 (DB 연결 정보)
  - src/main/resources 폴더에 database 폴더 생성
  - jdbc.properties 파일 생성
  - driverClassName, url, username, password 등록

#### jdbc.properties
~~~
// jdbc.properties
jdbc.driverClassName=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://ip주소(local에서 사용할 경우 localhost):포트번호/스키마 이름?serverTimezone=UTC
jdbc.username=아이디
jdbc.password=패스워드
~~~

#### root-context.xml
~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd
http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <context:property-placeholder location="classpath:database/jdbc.properties" />
    <context:component-scan base-package="com.spring_mvc.mybatis" />
    <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource">
        <property name="driverClassName" value="${jdbc.driverClassName}" />
        <property name="url" value="${jdbc.url}" />
        <property name="username" value="${jdbc.username}" />
        <property name="password" value="${jdbc.password}" />
    </bean>

    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource" />
        <property name="mapperLocations" value="classpath:com/spring_mvc/mybatis/**/*.xml" />
    </bean>

</beans>
~~~

#### servlet-context.xml
- 내용 추가
~~~xml
<context:component-scan base-package="com.spring_mvc.mybatis" />
~~~