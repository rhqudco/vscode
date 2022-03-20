## 리액트 스프링 연결
- 스프링 부트 프로젝트 생성
  - @RestController인 ReactController 생성
- 리액트 프로젝트 생성
  - axios로 http://localhost:8080 접속해서 메시지 와서 출력
  - 오류 발생
- 문제 해결 : WebConfig.java 설정
- 실행해서 오류 없이 잘 받아오는지 확인

### 리액트 프로젝트 생성
- react-spring-app
- npm install axios
- AxiosSpring.js 추가
- 실행 : 오류 발생
  - CORS 오류 : Cross-Origin Resource Sharing
  - 한 출처(origin)에서 실행 중인 웹 애플리케이션이 다른 origin 접근 권한이 없어서 나는 오류
    - WebConfig.java에서 설정

~~~java
@Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("http://localhost:8080", "http://localhost:3000");

    }
~~~