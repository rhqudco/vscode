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
- Artifact : boot002
- name : boot002
- Package Name : com.multi.boot002
- Packaging : War
- Dependency
  - JDBC API
  - MySQL Driver
  - Spring Web
  - MyBatis Framework

### 프로젝트 구조


#### application.properties

~~~
server.port=8080
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/springDB
spring.datasource.username=root
spring.datasource.password=1234

spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp

# xml-location
mybatis.mapper-locations=classpath:mappers/**/*.xml
~~~

#### pom.xml
- 아래의 내용 추가

~~~xml
<!--	JSP 사용 위해 의존성 추가	-->
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
		</dependency>
		<dependency>
			<groupId>org.apache.tomcat.embed</groupId>
			<artifactId>tomcat-embed-jasper</artifactId>
			<scope>provided</scope>
		</dependency>
<!--	lombok	 -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>
    </dependencies>
~~~

#### mapper 수정
- mapper namespace 경로를 바꿔야 한다.
  
~~~xml
<mapper namespace="com.multi.product.IProductDAO">
<!-- 이하 경로 모두 변경 -->
~~~

#### 패키지명Application.java

~~~java
// 컨트롤러 빈 추가
@ComponentScan(basePackageClasses = ProductController.class)
// mapper 빈 추가
@MapperScan(basePackageClasses = IProductDAO.class)
~~~

### 스프링 부트 프로젝트 생성 시 자동 생성되는 파일
- Myboot01Application.java
  - @SpringBootApplication
    - 스프링 부트 애플리케이션으로 설정하는 어노테이션
  - main() 메소드 : 스프링 부트 생성 시 자동으로 생성
    - 스프링 부트 프로젝트는 반드시 main()이 있어야 함
    - main()을 포함하는 java 파일이 있어야 함
      - 스프링 부트 애플리케이션을 일반 자바 애플리케이션처럼 개발하려는 의도 때문
- ServletInitializer.java
  - SpringBootServletInitializer 클래스로부터 상속 받음
  - SpringBootServletInitializer의 역할
    - 스프링 부트 애플리케이션을 web.xml 없이 톰캣에서 실행하게 해줌
      - 스프링 부트에는 web.xml, context.xml 설정 파일이 없음

### Spring Boot가 Spring Legacy(MVC 등)와 다른점
- pom.xml에서 스프링 프레임워크 버전 자동 설정
- 프로젝트 생성 시 dependencies 선택해서 pom.xml에 자동 삽입
- src/main/java에 패키지이름Application.java 메인 메소가 있다.
  - 이 클래스 실행 시 스프링 부트 시작
- tomcat 서버 자동 시작
  - 포트 충돌 시 오류 가능성 있음
- .jsp 파일을 기본 view로 하지 않으므로 추가 설정 필요
- src/main/resources 폴더 하위의 static 폴더에 리소스 파일 등 저장
  - image, js, css 등
- src/main/resources 폴더 하위의 templates 폴더에 템플릿 파일(jsp 파일 외) 저장
  - html
- src/main/resources 폴더 하위에 자동 생성되는 application.properties
  - web.xml 등을 대신하는 설정 파일

### 스프링 부트에서 프로젝트 외부 경로 지정
- 패키지에 WebConfig.java 클래스 생성
- @Configration
  - WebMvcConfigurer 인터페이스 구현
  - 외부 경로 지정

~~~java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        // "/prdImages/**" prdImages로 들어오면 file:////Users/gobyeongchae/Desktop/productImages/해당 경로에 들어가서 image 인식
        registry.addResourceHandler("/prdImages/**")
                .addResourceLocations("file:////Users/gobyeongchae/Desktop/productImages/");
    }
}
~~~

## 스프링 부트 파일 업로드 / 파일 다운로드
- MultipartFile 클래스 사용
  - 의존성 필요 없음
  - application.properties 파일에서 파일 최대 크기만 설정
- 자동으로 MultipartConfigElement 클래스를 빈으로 등록
- 파일명 중복되지 않도록 UUID 사용
  - 소프트웨어 구축에 사용되는 식별자 표준
  - 16 옥텟(128바이트)의 수
  - 표준 형식에서 UUID는 32개의 16진수로 표현되며 총36개 문자(32개 문자와 4개의 하이픈)로 된 8-4-4-4-12라는 5개의 그룹을 하이픈으로 구분
  - 자바 UUID 클래스의 randomUUID() 메소드를 사용해서 유일한 식별자 생성

## 스프링 부트 프로젝트에서 파일 업로드 / 다운로드 예제
### 파일 업로드
- 파일명 중복되지 않도록 파일 이름 변경해서 업로드
- 한 번에 여러 개의 파일 업로드
- 원본 파일명 그대로 업로드
### 파일 다운로드
- 폴더 내 파일 목록에서 선택해서 다운로드

#### 파일 업로드 예제 1
- 파일명 중복되지 않도록 파일 이름 변경해서 업로드

~~~java
// FileUploadController.java
// 파일 업로드 처리 (파일명 중복되지 않도록 파일 이름 변경해서 업로드)
    @RequestMapping("/upload/fileUpload")
    public String fileUpload(@RequestParam("uploadFile") MultipartFile file, Model model) throws IOException {
        String savedFileName = "";
        // 1. 파일 저장 경로 설정 : 실제 서비스되는 위치(프로젝트 외부에 저장)
        String uploadPath = "/Users/gobyeongchae/Desktop/UploadServerFile/";
        // 2. 원본 파일 이름 알아오기
        String originalFileName = file.getOriginalFilename();
        // 3. 파일 이름 중복되지 않게 이름 변경(서버에 저장할 이름) UUID 사용
        UUID uuid = UUID.randomUUID();
        savedFileName = uuid.toString() + "_" + originalFileName;
        // 4. 파일 생성
        File file1 = new File(uploadPath + savedFileName);
        // 5. 서버로 전송
        file.transferTo(file1);
        // model로 저장
        model.addAttribute("originalFileName", originalFileName);
        return"upload/fileUploadResult";
    }
~~~

~~~xml
<!-- fileUploadForm.jsp -->
<body>
    <h3>파일 업로드</h3>
    <form id="fileUploadForm" method="post" action="/upload/fileUpload" enctype="multipart/form-data">
      파일 : <input type="file" id="uploadFile" name="uploadFile"><br><br>
      <input type="submit" value="업로드">
    </form>
  </body>
~~~

~~~xml
<!-- fileUploadResult.jsp -->
    <body>
        ${originalFileName} 파일을 업로드 하였습니다.<br>
        (서버에만 출력) Users/gobyeongchae/Desktop/UploadServerFile 확인
    </body>
~~~

#### 파일 업로드 예제 2
- 여러 개 파일 업로드

~~~java
// FileUploadController.java
// 여러 개의 파일 업로드
    @RequestMapping("/upload/fileUploadMultiple")
    public String fileUploadMultiple(@RequestParam("uploadFileMulti") ArrayList<MultipartFile> files, Model model) throws IOException {
        String savedFileName = "";
        // 1. 파일 저장 경로 설정 : 실제 서비스되는 위치(프로젝트 외부에 저장)
        String uploadPath = "/Users/gobyeongchae/Desktop/UploadServerFile/";
        // 여러 개의 원본 파일을 저장할 리스트 생성
        ArrayList<String> originalFileNameList = new ArrayList<String>();
        for(MultipartFile file : files) {
            // 2. 원본 파일 이름 알아오기
            String originalFileName = file.getOriginalFilename();
            // 3. 파일 이름을 리스트에 추가
            originalFileNameList.add(originalFileName);
            // 4. 파일 이름 중복되지 않게 이름 변경(서버에 저장할 이름) UUID 사용
            UUID uuid = UUID.randomUUID();
            savedFileName = uuid.toString() + "_" + originalFileName;
            // 5. 파일 생성
            File file1 = new File(uploadPath + savedFileName);
            // 6. 서버로 전송
            file.transferTo(file1);
        }
        // model로 저장
        model.addAttribute("originalFileNameList", originalFileNameList);
        return"upload/fileUploadMultipleResult";
    }
~~~

~~~xml
<!-- fileUploadForm.jsp -->
<body>
    <h3>파일 업로드 (여러 개 파일 업로드)</h3>
        <form id="fileUploadFormMulti" method="post" action="/upload/fileUploadMultiple" enctype="multipart/form-data">
        파일 : <input type="file" id="uploadFileMulti" name="uploadFileMulti" multiple="multiple"><br><br>
        <input type="submit" value="업로드">
        </form>
  </body>
~~~

~~~xml
<!-- fileUploadMultipleResult.jsp -->
  <body>
  다음의 파일을 전송하였습니다.<br>
  <c:forEach items="${originalFileNameList}" var="file">
      ${file} <br>
  </c:forEach><br>
  (서버에만 출력) Users/gobyeongchae/Desktop/UploadServerFile 확인
  </body>
~~~

#### 파일 업로드 예제 3
- 원본 파일명 그대로 업로드
  - 예 : 상품 사진 등록하는 경우
    - 상품명과 동일한 이름으로 저장

~~~java
// FileUploadController.java
// 파일 업로드 처리 (원본 파일명 사용)
    @RequestMapping("/upload/fileOriginalNameUpload")
    public String fileUploadOriginal(@RequestParam("uploadFileOrigin") MultipartFile file, Model model) throws IOException {
        // 1. 파일 저장 경로 설정 : 실제 서비스되는 위치(프로젝트 외부에 저장)
        String uploadPath = "/Users/gobyeongchae/Desktop/UploadServerFile/";
        // 2. 원본 파일 이름 알아오기
        String originalFileName = file.getOriginalFilename();
        // 3. 파일 생성
        File file1 = new File(uploadPath + originalFileName);
        // 4. 서버로 전송
        file.transferTo(file1);
        // model로 저장
        model.addAttribute("originalFileName", originalFileName);
        return"upload/fileUploadResult";
    }
~~~

~~~xml
<!-- fileUploadForm.jsp -->
<body>
  <h3>파일 업로드 (원본 파일명 그대로 업로드)</h3>
      <form id="fileOriginalNameUpload" method="post" action="/upload/fileOriginalNameUpload" enctype="multipart/form-data">
        파일 : <input type="file" id="uploadFileOrigin" name="uploadFileOrigin" ><br><br>
        <input type="submit" value="업로드">
      </form> <br><h3>파일 업로드 (원본 파일명 그대로 업로드)</h3>
      <form id="fileOriginalNameUpload" method="post" action="/upload/fileOriginalNameUpload" enctype="multipart/form-data">
        파일 : <input type="file" id="uploadFileOrigin" name="uploadFileOrigin" ><br><br>
        <input type="submit" value="업로드">
      </form> <br>
  </body>
~~~

~~~xml
<!-- fileUploadResult.jsp -->
    <body>
        ${originalFileName} 파일을 업로드 하였습니다.<br>
        (서버에만 출력) Users/gobyeongchae/Desktop/UploadServerFile 확인
    </body>
~~~

#### 파일 다운로드 예제
- 폴더 내 파일 목록에서 선택해서 다운로드
- 다운로드 폴더로 파일 다운로드

~~~java
@Controller
public class FileDownloadController {
    // 파일 다운로드 폼으로 이동
    @RequestMapping("download/fileDownloadListView")
    public ModelAndView fileDownloadList() {
        ModelAndView mv = new ModelAndView();
        // 폴더에 있는 전체 파일 목록 가져오기
        File path = new File("/Users/gobyeongchae/Desktop/UploadServerFile/");
        String[] fileList = path.list();

        mv.addObject("fileList", fileList);
        mv.setViewName("download/fileDownloadListView");
        return mv;
    }
    // 파일 다운로드 처리
    @RequestMapping("/fileDownload/{file}")
    public void fileDownload(@PathVariable String file,
                             HttpServletResponse response) throws IOException {
        File f = new File("/Users/gobyeongchae/Desktop/UploadServerFile/", file);
        // file 다운로드 설정
        response.setContentType("application/download");
        response.setContentLength((int)f.length());
        response.setHeader("Content-disposition", "attachment;filename=\"" + file + "\"");
        // response 객체를 통해서 서버로부터 파일 다운로드
        OutputStream os = response.getOutputStream();
        // 파일 입력 객체 생성
        FileInputStream fis = new FileInputStream(f);
        FileCopyUtils.copy(fis, os);
        fis.close();
        os.close();
    }
}
~~~

~~~xml
 <body>
    <c:forEach items="${fileList}" var="file">
        <a href="<c:url value='/fileDownload/${file}'/> ">${file} 파일 다운로드</a><br>
    </c:forEach>
  </body>
~~~