## @Controller vs @RestController
- @Controller : 결과를 뷰 페이지(.jsp) 이름 반환
- @RestController : 별도의 뷰를 제공하지 않은 채 데이터 반환
  - 클래스에 붙임
  - @ResponseBody와 기능 동일 (메소드에서 처리)

#### @RestController 예제

- productSearchForm3.jsp와 productSearchForm3.js는 1과 같다.(선택자 이름, js에서 url 이름만 바꿈)

~~~java
// ProductController3.java
    // 상품 검색 폼3 이동
    @RequestMapping("/product/productSearchForm3")
    public String productSearchForm3() {
        return "product/productSearchForm3";
    }
}
~~~

~~~java
// MVCRestController.java

@RestController
public class MVCRestController {
    @Autowired
    ProductService service;

    // 상품 검색3
    @RequestMapping("/product/productSearch3")
    public ArrayList<ProductVo> productSearch3 (@RequestParam HashMap<String, Object> param,
                                              Model model){
        System.out.println("RestController");
        ArrayList<ProductVo> prdList = service.productSearch(param);
        model.addAttribute("prdList", prdList);
        return prdList;
    }
}
~~~

## 스프링 부트(Spring Boot)
- 스프링 프레임워크를 사용하는 프로젝트를 아주 간편하게 설정할 수 있는 스프링 프레임워크의 서브 프로젝트
  - 톰캣 설치 등 여러가지 복잡한 설정하지 않아도 된다.
- 특징
  - XML 기반 설정 과정 없이 간단히 프로젝트를 시작할 수 있음
  - Maven의 pom.xml 파일에 의존성 라이브러리의 버전을 지정하지 않아도 된다.(스프링 부트가 권장 버전 관리)
  - 단독 실행되는 스프링 애플리케이션 구현 가능
  - 프로젝트 환경 구축에 필요한 서버 외적인 툴 내장되어 있어 별도 설치 필요 없음

### 사용할 스프링 부트 프로젝트
#### 정보
- Maven
- Java 11
- 2.6.2
- Group : com.multi
- Artifact : boot001
- name : boot001
- Package Name : com.multi.boot001
- Packaging : War
- Dependency
  - JDBC API
  - MySQL Driver
  - Spring Web

#### application.properties

~~~
server.port=8080(tomcat 포트 번호)
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=주소(mysql 주소)
spring.datasource.username=@@@
spring.datasource.password=@@@

spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp
~~~

#### pom.xml
- 아래의 내용 추가

~~~xml
<dependency>
	<groupId>javax.servlet</groupId>
	<artifactId>jstl</artifactId>
</dependency>
<dependency>
	<groupId>org.apache.tomcat.embed</groupId>
	<artifactId>tomcat-embed-jasper</artifactId>
	<scope>provided</scope>
</dependency>
~~~