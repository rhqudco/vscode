# Artineer Spring 6주차 강의노트

# Loagging

- 실제 운영되는 시스템은 무조건 이슈가 발생한다.
- 로그를 통해 과거 발생한 이슈를 알 수 있고 해결하기 위해 로그는 매우 중요하고 무조건 필요하다.
- 로그가 쌓이게 되면 엄청난 정보이기 때문에 꼭 필요한 로그만을 사용해야 하는데 필요한 로그만을 추출하기는 너무 어렵다.
  - 다양한 모니터링 툴이 있지만 셀프로 공부하자.
- 우리는 실제로 로그를 사용하기 위해 정확한 로깅을 하는 방법을 배운다.
- @Slf4j
  - Lombok에 라이브러리
  - log.info를 통해 로그를 볼 수 있다.
- Api 서버에서 효과적으로 로그를 남기는 방법은 맨 처음 요청이 들어온 값과 응답 값을 남겨주는 것
  - 이상이 발생했을 때 입력값과 반환값을 확인하면 문제를 큰 틀안에서 발견할 수 있다.

## 1. 가장 심플한 로깅

- 조회를 통한 로깅하는 방법
- 로그 내역이 따로 나오기 때문에 여러 개의 요청이 들어오면 햇갈릴 수 있다.
    - 합쳐서 로깅을 해도 된다.
- article을 조회하는 기능과 로깅을 하는 기능이 같이 있기 때문에 한 기능(article을 조회하는)에 집중을 하지 못하는 코드가 됐다는 단점이 있다.

#### ArticleService.java

~~~java
@Slf4j
@RequiredArgsConstructor
@Service
public class ArticleService {
    
    // ...

  public Article findById(Long id) {
    log.info("Request : id - {}", id); // 요청값

    Article article = articleRepository.findById(id)
            .orElseThrow(() -> new ApiException(ApiCode.DATA_IS_NOT_FOUND, "article is not found"));

    log.info("Response : article.title - {}, article.content - {}", article.getTitle(), article.getContent()); // 응답 값

    return article;
  }
  
  // ...
}
~~~

#### 로그 내역

~~~java
2021-11-21 19:34:09.272  INFO 25824 --- [nio-8080-exec-3] c.a.s.service.ArticleService : Request : id - 1
2021-11-21 19:34:09.290  INFO 25824 --- [nio-8080-exec-3] c.a.s.service.ArticleService : Response : article.title - 아티니어 스프링 강좌, article.content - 아티니어 스프링 많관부
~~~

## 2. proxxy Pattern을 활요한 로깅
- 스프링에서는 대부분 프록시 패턴으로 구현된 AOP를 사용한다.
- 로그를 하는 코드와 비즈니스를 하는 코드를 분할 하는 것이 목표.
  -  응집도를 높이고 결합도를 낮출 수 있다.
  -  분리가능한 기능을 한 곳에 두는 것은 두 기능의 의존성을 높이고 결합도를 낮추는 행위
- ArticleService를 ArticleServiceImpl로 이름을 변경.
- ArticleService Interface 생성
  - 인터페이스에는 보통 함수를 구현하지 않고 선언만 한다.
    - 함수 시그니처라고 하며 인터페이스에는 함수의 시그니처를 작성한다.
    - 함수 시그니처 : __함수가 반환하는 리턴 타입__ __함수의 이름(함수가 받는 파라미터 타입);__
    - 객체지향에서는 함수라기보단 규격, 규약에 대한 목적이 더 크기 때문에 메세지라고 한다.

#### ArticleService.java

~~~java
public interface ArticleService {
    // CRUD에 해당하는 시그니처
    Long save(Article request);

    Article findById(Long id);

    Article update(Article request);

    void delete(Long id);
}
~~~

#### ArticleService 인터페이스를 구현 
- 실제 실무에서는 인터페이스 먼저 만들어지고 구현체가 만들어진다.

#### ArticleServiceImpe.java

~~~java
@Slf4j
@RequiredArgsConstructor
@Service
public class ArticleServiceImpl implements ArticleService {
  private final ArticleRepository articleRepository;

  @Override
  public Long save(Article request) {
    return articleRepository.save(request).getId();
  }

  @Override
  public Article findById(Long id) {
    return articleRepository.findById(id)
            .orElseThrow(() -> new ApiException(ApiCode.DATA_IS_NOT_FOUND, "article is not found"));
  }

  @Transactional
  @Override
  public Article update(Article request) {
    Article article = this.findById(request.getId());
    article.update(request.getTitle(), request.getContent());

    return article;
  }

  @Override
  public void delete(Long id) {
    articleRepository.deleteById(id);
  }
}
~~~

- ArticleService의 규정을 준수하는 또 다른 구현체를 만든다.
- ArticleServiceImpl이 원본이고 원본과 Proxy가 같은 규정을 지키는 객체가 인터페이스이다.
- 프록시 객체는 원본 구현체를 가지고 있는 형태(감싸고 있는)이며 구현체를 그냥 호출하여 실행시키는 구조.
- 프록시와 원본을 따로 구현하기 때문에 로깅을 프록시에서 처리할 수 있다.
  - 로깅 외에 다른 부가적인 기능 모두 프록시에서 처리할 수 있다.

#### ArticleServiceProxy.java

~~~java
@RequiredArgsConstructor // 의존성 주입을 위해 생성자 만듦(생성자 주입)
@Service // 빈에 등록
public class ArticleServiceProxy implements ArticleService {
    private final ArticleServiceImpl articleServiceimpl;

    @Override
    public Long save(Article request) {
        return articleServiceimpl.save(request);
    }

    @Override
    public Article findById(Long id) {
        return articleServiceimpl.findById(id);
    }

    @Override
    public Article update(Article request) {
        return articleServiceimpl.update(request);
    }

    @Override
    public void delete(Long id) {
        articleServiceimpl.delete(id);
    }
}
~~~

#### ArticleServiceProxy.java

~~~java
@Slf4j
@RequiredArgsConstructor
@Service
public class ArticleServiceProxy implements ArticleService {
  private final ArticleService articleService;

  @Override
  public Long save(Article request) {
    return articleService.save(request);
  }

  @Override
  public Article findById(Long id) {
    // Pre-Process
    log.info("Request : id - {}", id);

    Article article = articleService.findById(id);

    // Post-Process
    log.info("Response : article.title - {}, article.content - {}", article.getTitle(), article.getContent());

    return article;
  }

  @Override
  public Article update(Article request) {
    return articleService.update(request);
  }

  @Override
  public void delete(Long id) {
    articleService.delete(id);
  }
}
~~~

- 하나의 인터페이스를 통해 같은 규정에 넣어놨다.
- 객체지향에서의 느슨한 결합을 위해서는 구현체에 직접 접근해서 바로 사용하는 것 보다 사이에 인터페이스를 두고 인터페이스를 통해 통신할 수 있도록 하는 것이 중요하다.
- ArticleController는 ArticleService를 사용하는 클라이언트 입장에서 ArticleSerivceImpl이나 ArticleServiceProxy에 대한 정보가 필요 없다.
  - ArticleService라는 인터페이스와 소통을 하기 때문
  - 정보의 은닉이 된다.
    - 서버의 입장에서는 프록시 객체를 만들어도 클라이언트는 알지 않아도 된다.
    - 반대로 서버는 클라이언트에세 프록시의 존재를 알리지 않아도 된다.
- 즉 클라는 서버의 상세 구현 내용을 알 필요가 없고, 반대로 서버는 인터페이스 규격만 맞추어준다면 원하는 대로 개발을 진행할 수 있다.

~~~java
Parameter 0 of constructor in com.artineer.spring_lecture_week_2.conroller.ArticleController required a single bean, but 2 were found:
	- articleServiceImpl: defined in file [/Users/gobyeongchae/Desktop/Artineer_Spring/spring_lecture_week_6/build/classes/java/main/com/artineer/spring_lecture_week_2/service/ArticleServiceImpl.class]
	- articleServiceProxy: defined in file [/Users/gobyeongchae/Desktop/Artineer_Spring/spring_lecture_week_6/build/classes/java/main/com/artineer/spring_lecture_week_2/service/ArticleServiceProxy.class]
~~~

- ArticleController는 ArticleService하나의 빈을 요구하는데 두 개가 발견되어 오류가 발생
  - ArticleService를 구현하는 구현체가 Impl과 Proxy가 있기 때문
  - 우리는 Proxy를 거쳐가는 것을 원하기 때문에 Proxy에 @Primary 작성
    - 원본보다 우선순위가 높아져 최우선순위를 갖게하는 어노테이션

#### 결론
- 인터페이스를 설계하여 느슨한 결합을 가져왔다
- 클라이언트는 서버가 어떻게 구현됐는지 모르고, 서버는 클라이언트에게 알려줄 필요가 없다.
- 프록시 객체에서 비즈니스 로직을 제외한 부가적 기능을 처리하면 효과적으로 코드 분리 가능, 원하는 기능을 구현할 수 있다.

## 3. AOP를 활용한 로깅
- OOP(객체지향 프로그래밍)을 보완하기 위한 패러다임.
- 객체지향을 중심으로 프로그래밍을 하다보니 기능이 흩어져 있는 코드를 한 클래스에 모아 구현하는 것
- AOP 용어
  - Aspect : AOP (Aspect Oriented Programming) 객체로서 사용하겠다고 명시
  - Advice : 실제 모듈로서 동작되는 그 일 자체. 여기서는 로깅하는 업무 그 자체를 개념적으로 의미.
  - Weaving : 프록시 객체에 원본 객체를 끼워 넣는 것.
  - Around : 언제 Asepct 를 Weaving 시킬 것인지 그 조건을 명시
  - JoinPoint : Advice가 적용된 위치
- AOP를 통한 로깅 구현
  - Around에 조건을 넣어 사용하는데 특정 어노테이션을 넣어서 어노테이션이 선언 됐을 때 Aspect가 실행되도록 구현한다.
  - aspect 패키지 생성
    - aspect 패키지에 ExecuteLog.java(어노테이션) 생성

#### ExecuteLog.java

~~~java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface ExecuteLog {
}
~~~
- @Target 어노테이션이 적용되는 위치를 설정할 수 있다.  __.METHOD__ 라고 되어 있기 때문에 METHOD 레벨에서만 설정 가능
- @Retention 어노테이션은 해당 어노테이션이 어느 시점까지 메모리에 존재하게 하는지를 지정한다.
- 실제 Weaving Point의 일을 받아 Advice는(로깅)를 객체를 만든다

#### ExecuteLogAspect.java

~~~java
@Slf4j // 로깅을 하기 위해 로깅 라이브러리
@Component // 빈으로 등록
@Aspect // 흩어진 기능을 뭉쳐서 쓴다. AOP로 동작
public class ExecuteLogAspect {
  @Around(value = "@annotation(ExecuteLog)") // 언제 실행되는지(위빙되는 시점) @annotation(ExecuteLog)가 선언된 함수에서만 위빙이 일어난다.
  public Object log(ProceedingJoinPoint joinPoint) throws Throwable {
    // jointpoint는 위빙된 위치에 대한 정보를 갖고 있다.

    // 작업 시작 시간을 구합니다.
    long start = System.currentTimeMillis();

    // 위빙된 객체의 작업을 진행합니다.
    final Object result = joinPoint.proceed(); // joinPoint.proceed()는 원본 객체를 실행하라는 의미

    MethodSignature signature = (MethodSignature) joinPoint.getSignature(); // 원본함수의 시그니처를 joinpoint를 통해 가지고 온다.

    String methodName = signature.getName(); // 어떤 함수가 실행된지 모르기 때문에 이름을 가져온다.
        String input = Arrays.toString(signature.getParameterNames()); // 입력에 해당하는 값

    String output = result.toString();

    log.info("Method Name : {}, Input : {}, Output : {}, Execute Time : {}", methodName, input, output, (System.currentTimeMillis() - start) + " ms");

    return result;
  }
}
~~~

#### ArticleServiceImpl.java

~~~java
@Slf4j
@RequiredArgsConstructor
@Primary
@Service
public class ArticleServiceImpl implements ArticleService {
    
    // ...
  
    @ExecuteLog
    @Override
    public Article findById(Long id) {
        return articleRepository.findById(id)
                .orElseThrow(() -> new ApiException(ApiCode.DATA_IS_NOT_FOUND, "article is not found"));
    }
    
    // ...
}
~~~

- ArticleServiceImpl의 findById에 로깅을 하고 싶었기 때문에 @ExecuteLog 작성
- Proxy를 쓰지 않기 위해 @Primary를 Impl로 옮긴다.
  - ArticleController는 ArticleServiceProxy가 아니라 ArticleServiceImpl을 주입 받는다.
    - Controller의 코드는 수정하지 않고 의존성이 바뀌게 된다
      - 객체지향 프로그램의 장점으로
        - 다형성을 갖고 필요할 때 마다 빈들을 주입하며 스프링 부트의 자동 설정도 이런 기능을 활용한다.

~~~java
@Slf4j
@RequiredArgsConstructor
@Primary
@Service
public class ArticleServiceImpl implements ArticleService {
    
    // ...
  
    @ExecuteLog
    @Override
    public Article findById(Long id) {
        return articleRepository.findById(id)
                .orElseThrow(() -> new ApiException(ApiCode.DATA_IS_NOT_FOUND, "article is not found"));
    }
    
    // ...
}
~~~

~~~java
2021-11-21 21:08:47.761  INFO 26194 --- [nio-8080-exec-2] c.a.s.aspect.ExecuteLogAspect            : Method Name : findById, Input : [id], Output : com.artineer.spring_lecture_week_2.domain.Article@3ead4540, Execute Time : 18 ms
~~~

- 실행 결과를 확인해 보면 Output 부분이 세부적으로 나오지 않고 클래스 명과 헤쉬코드 값이 나온다.
- toString() 을 오버라이딩 하지 않았기 때문에 자바에서 기본으로 제공되는 toString() 함수가 호출되는 것.
- Article.java(도메인)에 @ToString 어노테이션을 넣어서 해결 가능하다.

#### Article.java

~~~java
@Getter
@Builder
@NoArgsConstructor
@AllArgsConstructor
@ToString
@Entity
public class Article {
    // ...
}
~~~

##### 로그 결과

~~~java
2021-11-21 21:31:07.459  INFO 26285 --- [nio-8080-exec-2] c.a.s.aspect.ExecuteLogAspect            : Method Name : findById, Input : [id][1], Output : Article(id=1, title=아티니어 스프링 강좌, content=아티니어 스프링 많관부), Execute Time : 24 ms
~~~

- AOP를 활용하여 범용적으로 사용할 수 있도록 했다.
  - 어노테이션을 넣어주는 것으로 Weaving이 되어 우리가 원했던 작업(여기서는 로깅)들을 비즈니스 로직이 침해되지 않고 이루어냈다.
  - 하지만 @ToString을 활용하는 것은 지양된다.
    - 만약 어떤 객체가 같은 클래스를 참조하고 있다면 무한 재귀 호출이 발생하여 StackOverFlow가 발생한다.
    - @ToString은 조심헤서 사용할 것.

## Optional) 4. Reflection 활용하여 어노테이션으로 정보를 가져와 보자.

- Reflection을 사용하여 @ToString을 사용하지 않고 어노테이션에 type정보도 같이 전달하는 방법으로 AOP에서 type을 찾아 type에 맞는 렌더링을 할 수 있다.
- 기존 자바와는 다르다.
  - 일반적인 코딩의 순서는 코드를 짜고 클래스 파일을 만들고 결국 클래스 파일이 실행되고 런타임 상에서 동작을 한다.
  - 중간 언어가 있는 언어들은 Reflection이라는 테크닉을 사용할 수 있다
    - Reflection은 소스코드를 짤 때 소스코드가 클래스 코드로 가는 것이 원래 방향이지만, 소스코드를 짤 때 이미 만들어진 클래스 파일의 형식을 가져와서 사용한다.
      - 여기서는 ExecuteLog에서 Article이라는 클래스 타입을 넘겨주고 ExecuteLogAspect에서 받아 렌더링을 하는 기능을 자체적으로 구현하기 위해 Article이라는 클래스 타입을 가지고 왔는데, Article 클래스 타입을 가지고 Article 클래스 파일을 액세스 하여 파일이 가진 필드 정보 메소드 정보를 스캔해서 런타임상으로 주입할 수 있다.

#### ExecuteLog.java

~~~java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface ExecuteLog {
    Class<?> type(); // 클래스의 와일드카드 타입을 가진다.
}
~~~

#### ArticleServiceImpl.java

~~~java
// ...
public class ArticleServiceImpl implements ArticleService {

    // ...
    
    @ExecuteLog(type = Article.class) // 리턴 타입에 맞춰 작성
    @Override
    public Article findById(Long id) {
        return articleRepository.findById(id)
                .orElseThrow(() -> new ApiException(ApiCode.DATA_IS_NOT_FOUND, "article is not found"));
    }
    
    // ...
}
~~~

#### ExecuteLogAspect.java

~~~java
@Slf4j
@Component
@Aspect
public class ExecuteLogAspect {
    @SuppressWarnings("unchecked")
    @Around(value = "@annotation(ExecuteLog)")
    public <T> Object log(ProceedingJoinPoint joinPoint) throws Throwable {
        // 작업 시작 시간을 구합니다.
        long start = System.currentTimeMillis();

        // 위빙된 객체의 작업을 진행합니다.
        final T result = (T) joinPoint.proceed();

        MethodSignature signature = (MethodSignature) joinPoint.getSignature();

        // ExecuteLog 어노테이션에 type 값에 들어간 타입을 추론합니다.
        Class<T> clazzType = this.classType(signature.getMethod().getAnnotations());

        String methodName = signature.getName();
        String input = Arrays.toString(signature.getParameterNames());

        String output = this.toString(result);

        log.info("Method Name : {}, Input : {}, Output : {}, Execute Time : {}", methodName, input, output, (System.currentTimeMillis() - start) + " ms");

        return result;
    }

    private <T> String toString(T result) throws Throwable {
        StringBuilder sb = new StringBuilder();
        sb.append("[");
        for(Field field : result.getClass().getDeclaredFields()) {
            if(Strings.isBlank(field.getName())) {
                continue;
            }

            field.setAccessible(true);
            sb.append(field.getName()).append("=").append(field.get(result)).append(", ");
        }
        sb.append("]");

        return sb.toString();
    }

    @SuppressWarnings("unchecked")
    private <T> Class<T> classType(Annotation[] annotations) throws Throwable {
        Annotation executeLogAnnotation = Arrays.stream(annotations)
                .filter(a -> a.annotationType().getCanonicalName().equals(ExecuteLog.class.getCanonicalName()))
                .findFirst().orElseThrow(() -> new RuntimeException("ExecuteLog Annotation is not existed..."));

        String typeMethodName = "type";
        Method typeMethod = Arrays.stream(executeLogAnnotation.annotationType().getDeclaredMethods())
                .filter(m -> m.getName().equals(typeMethodName))
                .findFirst().orElseThrow(() -> new RuntimeException("type() of ExecuteLog is not existed..."));

        return (Class<T>) typeMethod.invoke(executeLogAnnotation);
    }
}
~~~

#### 로그 결과

~~~java
2021-11-22 00:08:55.796  INFO 27117 --- [nio-8080-exec-2] c.a.s.aspect.ExecuteLogAspect            : Method Name : findById, Input : [id][1], Output : [id=1, title=아티니어 스프링 강좌, content=아티니어 스프링 많관부, ], Execute Time : 20 ms
~~~

- 접근하는 방법들이 이미 다 만들어진 클래스 파일의 구조로 액세스를 하는데 이것이 Reflection 테크닉이다.
  - 클래스의 구조로 접근해서 어떤 필드인지, 어떤 메소드인지 이름을 통해 값들을 가져오는 형태.
  - 라이브러리나 오픈소스를 사용자의 관점뿐만 아니라 직접 만드는 수준의 레벨이 되기 위해서는 알고 있으면 좋다.