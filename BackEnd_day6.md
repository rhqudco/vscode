## 스프링 프레임워크
- 엔터프라이즈 애플리케이션 구축을 위한 솔루션
- 자바 애플리케이션 개발을 포괄적인 인프라 지원을 제공하는 자바 플랫폼
  - 스프링에서 인프라를 처리하므로 개발자는 애플리케이션 개발에만 집중
- 모듈화되어 있어 필요한 부분만 사용 가능
- 완전한 기능을 갖춘 MVC 프레임워크 제공

### 장점
- 생산성 우수
  - 엔터프라이즈 애플리케이션 구축을 위한 솔루션이지만, 가볍고 모듈화 되어 있어 필요한 부분만 사용하면 된다.
  - POJO 클래스와 약간의 설정만으로도 개발이 가능하므로 개발 생산성을 높일 수 있음
  - 실제 스프링을 적용하면 적용하지 않은 코드의 1/3 정도의 코드만으로도 개발 가능
- 품질 보증
  - 스프링 프레임워크는 이미 검증된 많은 아키텍처 및 디자인 패턴을 적용하여 만들어졌기 때문에 코드에 아키텍처를 구현하기 위한 코드나 디자인 패턴을 사용하기 위한 코드를 개발자가 만들 필요가 없음
  - 이는 개발에 일관성을 제공해 주고 소프트웨어의 품질을 보증해 줌
- 유지 보수 용이
  - 스프링 프레임워크를 사용하여 작성된 애플리에케이션들을 유지보수하는데 소요되는 인력과 시간을 줄일 수 있기 때문에 여러 프레임워크 중 스프링 프레임워크가 업계 표준으로 자리잡음

### EJB(Enterprise JavaBean)
- 규모가 커지고 복잡한 애플리케이션 제작위해 만들어진 기술
- extends, implements를 많이 사용해서 클래스 의존도가 높고, 복잡하고 제한이 많은 문제 발생
- 별도로 종속되지 않고 간단한 자바 객체를 사용하자는 의도에서 나온 것이 POJO
- Java EE 등의 중량 프레임워크들을 사용하게 되면서 해당 프레임워크에 종속된 '무거운'객체를 만들게 된 것에 반발해서 사용하게 된 용어가 POJO

### POJO (Plain Old Java Object)
- 자바 언어 사양 외에 어떠한 제한에도 묶이지 않은 자바 객체
- 특정 환경과 규약에 종속되지 않아 필요에 따라 재사용될 수 있는 방식으로 설계된 객체
- 즉, 다른 클래스를 상속 받거나 인터페이스를 구현해야 하는 규칙이 없는 자바 클래스
- 미리 정의된 클래스 확장의 예
  - public class @@@ extends javax.servlet.http.HttpServlet{ ... }
- 대표적인 POJO
  - JavaBean
    - 생성자와 Getters/Setters만 지닌 단순 자바 객체
  - 프레임워크
    - 스프링 프레임워크
      - POJO를 사용하는 장점과 EJB에서 제공하는 엔터프라이즈 서비스와 기술을 그대로 사용할 수 있도록 도와주는 프레임워크

### 특징
- POJO 기반 프레임워크
  - 자바 객체의 라이프사이클을 스프링 컨테이너가 직접 관리하고 스프링 컨테이너로부터 필요한 객체를 얻어옴
- DI(Dependency Injection) 지원
  - 의존성 주입
  - 의존 관계에 있는 객체를 생성 조립해주는 기능
  - 각 계층이나 서비스들 사이 또는 객체들 사이의 의존성이 존재할 경우 스프링 프레임워크가 서로 연결시켜, 클래스 간 약한 결합 가능
- AOP(Aspect Oriented Programming) 지원
  - 관점 지향 프로그래밍
  - 트랜잭션 로깅, 보안 등 여러 모듈에서 공통적으로 지원하는 기능을 분리하여 사용 가능
  - 반복적인 코드를 줄이고 개발자가 비즈니스 로직에만 집중할 수 있도록 지원
- 뛰어난 확장성
  - 스프링 프레임워크의 소스는 모두 라이브러리로 분리되어 있어서 필요한 라이브러리만 가져다 사용하면 됨
- Model2 방식의 MVC 프레임워크 지원
  - Model / View / Controller 패턴

### 스프링 프레임워크 핵심 기능
- 의존 관계에 있는 객체를 생성 조립해주는 기능
- DI(Dependency Injection : 의존성 주입)
  - 객체 간의 의존성을 개발자가 설정하는 것이 아니라 스프링 컨테이너가 주입 시켜주는 기능
  - 장점 : 객체를 쉽게 확장하고 재사용할 수 있음
- IoC(Inversion of Control : 제어의 역전)
  - 객체에 대한 제어권 문제
  - 기존에는 개발자에게 제어권이 있었음
    - new 연산자를 사용해서 원하는 곳에서 객체 생성
  - 스프링 프레임워크에서는 개게의 제어권이 스프링에게 있고 인스턴스 라이프 사이클(생성~소멸)을 개발자가 아닌 스프링 프레임워크에서 담당

### 스프링 프로젝트 종류
- Spring Legacy Project
  - 스프링 템플릿 프로젝트 이용하는 프로젝트
  - 모델2 방식 (MVC) 프로젝트 생성 시 사용
  - 서버 및 여러 설정 필요
  - 실제 개발 업무에서 많이 사용 했었음
- Spring Starter Project
  - Spring Boot을 이용하는 프로젝트
  - 최대한 간단하게 실행하고, 배포가 가능한 수준의 웹 애플리케이션을 제작하기 위한 목적
  - 개발에 필요한 모든 환경 설정을 갖추면서 최소한의 개발을 해야 하는 경우 사용
  - 개발자가 복잡한 설정 없이 모든 개발 환경이 준비되기 때문에 초보 개발자도 쉽게 웹 프로젝트 생성 가능
  - 실제 개발 업무에서는 Legacy Project 사용했지만 현재는 Spring Boot를 주로 사용
  - 기존에 진행했던 프로젝트들은 Legacy Project가 많다.
- Simple Spring Maven (Maven)
  - Spring 라이브러리의 기본 세트를 포함하는 Maven을 사용하여 간단한 Spring 프로젝트 생성
    - Maven (메이븐)
      - Java용 프로젝트 관리도구
      - XML 기반의 정적인 빌드 제공
    - Gradle (그레이들)
      - 그루비(groovy) 스크립트 기반의 동적인 빌드 기능 제공
      - 안드로이드 앱을 만들 때 필요한 공식 빌드시스템
      - 메이븐보다 빌드 작업이 간단하며 프로그래밍만으로 기능 추가 가능
      - 별도의 빌드 스크립트를 통하여 사용할 애플리케이션 버전, 라이브러리 등 설정

## 의존성(Dependency)
- 객체 간 의존성
- 한 클래스가 다른 클래스의 객체를 통해 그 클래스의 메소드를 실행할 때 이를 '의존'한다고 표현

~~~java
class A {
  private B b;
  public A() {
    b = new B();
  }
}
// A 클래스에서 직접 생성
// (A 클래스 객체 생성될 때 B 클래스 객체 b 생성)
// (일체형으로 묶여 있음)
~~~

~~~java
class A {
  private B b;
  public void setB(B b) {
    this.b = b;
  }
}
// 외부에서 만든 객체를 받아서 사용
// (부품을 조립하여 사용하는 개념)
// DI
~~~

- DI (Dependency Injection : 의존성 주입)
  - 외부에서 빈(객체)을 만들어 필요로 하는 곳에 전달해 주도록 하는 것
  - 즉, 개발자가 new 연산자를 사용하여 직접 객체를 생성하지 않고 외부에서 생성된  Bean(객체)을 IoC 컨테이너가 넣어 주는 방식 (주입 : injection)
  - 일반적으로 부품(Bean)을 조립(의존성 주입)해서 사용한다고 함
- DI(의존성 주입) 방법을 사용하는 이유
  - 의존하는 객체의 클래스가 변경되거나 다른 클래스의 객체를 사용하게 될 경우 의존 관계(결합 상태)에 있는 다른 모든 클래스들의 소스 코드도 변경해야 함
  - 의존성 주입 방법을 사용하면, 클래스 결합 상태를 변경하거나 객체를 주입하는 부분만 수정하면 되므로 수정할 코드의 양을 줄일 수 있다는 장점이 있다.
  - 예
    - A1 클래스를 사용하다가 A2 클래스로 변경할 경우 설정 파일에서 클래스 이름만 변경해 주면 됨
    - \<bean id=”a” class=”com.package.A1” />  // A1을 A2로 변경하기만 하면 됨
- 스프링에서 의존성 주입 방법
  - XML을 이용한 방법
    - xml 설정 파일에 \<bean> 설정
  - Annotation을 이용한 방법
    - 자바 코드에서 '@어노테이션'으로 설정
- 스프링을 사용하지 않는 DI
  - DI를 사용하지 않는 코드
    - DI를 사용하지 않는 코드 특징
      - 의존성 관계가 있는 객체를 개발자가 new 연산자를 이용해서 직접 생성
  - DI를 사용한 코드
    - 생성자 기반 DI
    - Setter 기반 DI
- 스프링 DI
  - XML을 이용한 DI
  - Annotation을 이용한 DI

#### 스프링을 사용하지 않는 DI - DI를 사용하지 않는 코드 예제 - NameService.java, NameController.java, NameMain.java

- NameService
- NameController
  - new 연산자를 사용해서 NameService 클래스 객체 생성
  - 의존성 존재
  - DI는 아님
- NameMain

~~~java
package com.di.no_spring_no_di;

public class NameService {
    // 이름 전달 받아서  "내 이름은 ~ 입니다" 반환하는 메소드
    public String showName(String name) {
        System.out.println("NameService showName() 메소드");
        String myName = "내 이름은 " + name + " 입니다.";
        return myName;
    }
}
~~~

~~~java
package com.di.no_spring_no_di;

public class NameController {
    // 원하는 곳에서 new 연산자를 사용해서 객체 직접 생성
    // 의존성은 존재하나 DI는 아님
    NameService nameService = new NameService();

    // 이름을 전달 받아서 NameService 클래스의 showName() 메소드에게 전달하고
    // "내 이름은 ~ 입니다" 전달 받아서 출력하는 메소드.
    public void show(String name) {
        System.out.println("NameController : " + nameService.showName(name));
    }
}
~~~

~~~java
package com.di.no_spring_no_di;

public class NameMain {
    public static void main(String[] args) {
        NameController nameController = new NameController();
        nameController.show("홍길동");
    }
}
~~~

#### 스프링을 사용하지 않는 DI - 생성자 기반 DI 코드 예제 - NameService.java, NameController.java, NameMain.java
- 의존성 관계에 있는 객체를 new를 통해 직접 생성하지 않고
- 생성자를 통해 외부에서 전달 (주입 : injection)

~~~java
package com.di.no_spring_di_constructor;

public class NameService {
    // 이름 전달 받아서  "내 이름은 ~ 입니다" 반환하는 메소드
    public String showName(String name) {
        System.out.println("NameService showName() 메소드");
        String myName = "내 이름은 " + name + " 입니다.";
        return myName;
    }
}
~~~

~~~java
package com.di.no_spring_di_constructor;

public class NameController {
    // 멤버 변수 선언
    NameService nameService;
    // NameService 객체를 new 연산자를 통해 직접 만들지 않고 생성자를 통해 객체를 전달 받음.
    // 생성자를 통해 외부에서 주입
    // 의존성 주입
    public NameController(NameService nameService) {
        this.nameService = nameService;
    }
    public void show(String name) {
        System.out.println("NameController : " + nameService.showName(name));
    }
}
~~~

~~~java
package com.di.no_spring_di_constructor;

public class NameMain {
    public static void main(String[] args) {
        // NameController에 전달할 NameService 클래스 객체 생성
        NameService nameService = new NameService();

        NameController controller = new NameController(nameService);
        controller.show("이몽룡");
    }
}
~~~

#### 스프링을 사용하지 않는 DI - Setter 기반 DI - NameService.java, NameController.java, NameMain.java
- 생성자를 구현할 때 전달해야 할 객체가 많은 경우 일일이 생성자를 구현하는 것이 번거로울 수가 있음 이 때 Setter 메소드를 사용하여 의존성 주입 수행

~~~java
package com.di.no_spring_di_setter;

public class NameService {
    // 이름 전달 받아서  "내 이름은 ~ 입니다" 반환하는 메소드
    public String showName(String name) {
        System.out.println("NameService showName() 메소드");
        String myName = "내 이름은 " + name + " 입니다.";
        return myName;
    }
}
~~~

~~~java
package com.di.no_spring_di_setter;

public class NameController {
    NameService nameService;

    // 생성자 없고 Setter 메소드를 통해서 외부에서 주입 받음
    public void setNameService(NameService nameService) {
        this.nameService = nameService;
    }
    public void show(String name) {
        System.out.println("NameController : " + nameService.showName(name));
    }
}
~~~

~~~java
package com.di.no_spring_di_setter;

public class NameMain {
    public static void main(String[] args) {
        NameService nameService = new NameService();
        NameController controller = new NameController();
        // Setter메소드를 통해 nameService 객체 전달
        controller.setNameService(nameService);
        controller.show("성춘향");
    }
}
~~~

## Spring DI
- 스프링의 의존성 주입 (스프링의 핵심 기능)
  - 스프링 프레임워크는 컨테이너 역할을 하기 때문에 스프링 컨테이너 또는 IoC 컨테이너라고도 함
  - 스프링은 필요한 빈을 생성하여 컨테이너에 넣어 관리
  - 따라서 빈을 생성하기 위한 설정과 의존 객체를 주입시키기 위한 설정 필요

### IoC 컨테이너
- Inversion of Control : 제어의 역전
  - 객체를 생성/관리하는 제어권이 개발자에게 있는 것이 아니라
  - 객체를 생성해서 주입시키고 관리하는 제어권이 스프링에게 있기 때문에 제어가 역전되었다고 하는 것
- 객체를 개발자가 생성/관리하는 것이 아니라 IoC 컨테이너가 빈으로 설정/주입 관리
- 스프링은 프레임워크이면서 동시에 컨테이너 역할
- 빈을 생성하고 소멸하기까지 생명주기를 관리하기 위해 빈을 컨테이너에 로드하여 관리

### XML을 이용한 DI (생성자 기반)
- XML 파일에 빈(bean : 부품)을 정의(생성)하고
  - \<bean id=”이름” class=”패키지명.클래스명”>
- 의존성 설정 (부품 조립)
  - \<ref bean=”의존하는 빈”>
- XML을 이용해서 의존성을 주입하기 위해서는 클래스에 생성자 또는 Setter 메소드가 반드시 있어야 함
- 스프링은 Pre-loading 방식 사용
  - ApplicationContext를 이용해서 컨테이너를 구동하면 컨테이너가 구동되는 시점에 스프링 설정 파일에 등록된 빈을 생성하고 컨테이너에 로드

#### XML을 이용한 DI - 생성자 기반 DI (스프링 DI) 예제 - applicationContext.xml, NameService.java, NameController.java, NameMain.java
- 클래스에 생성자 있어야 하고
- 스프링 설정 파일(xml)에서 빈을 정의할 때
  - \<constructor-arg ref=”의존하는 빈”> 태그를 이용하여 의존성 주입
- NameService 객체를 NameMain에서 생성하지 않고
  - XML 설정 파일에서 생성
- Main 클래스 역할
  - 컨테이너 객체 생성
  - 컨테이너에서 컴포넌트(빈) 가져옴

~~~xml
    <bean id="nameService" class="com.di.spring_di_xml_constructor.NameService"/>
    <bean id="nameController" class="com.di.spring_di_xml_constructor.NameController">
        <!-- 생성자 기반 의존성 주입 : nameService 참조-->
        <constructor-arg ref="nameService"/>
    </bean>
~~~

~~~java
package com.di.spring_di_xml_constructor;

public class NameService {
    // 이름 전달 받아서  "내 이름은 ~ 입니다" 반환하는 메소드
    public String showName(String name) {
        System.out.println("NameService showName() 메소드");
        String myName = "내 이름은 " + name + " 입니다.";
        return myName;
    }
}
~~~

~~~java
package com.di.spring_di_xml_constructor;

public class NameController {
    // 멤버 변수 선언
    NameService nameService;
    // NameService 객체를 new 연산자를 통해 직접 만들지 않고 생성자를 통해 객체를 전달 받음.
    // 생성자를 통해 외부에서 주입
    // 의존성 주입
    public NameController(NameService nameService) {
        this.nameService = nameService;
    }
    public void show(String name) {
        System.out.println("NameController : " + nameService.showName(name));
    }
}
~~~

~~~java
package com.di.spring_di_xml_constructor;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

public class NameMain {
    public static void main(String[] args) {
        AbstractApplicationContext context = new GenericXmlApplicationContext("applicationContext.xml");
        NameController controller = context.getBean("nameController", NameController.class);
        controller.show("변학도");
        context.close();
    }
}
~~~


#### XML을 이용한 DI - 생성자 기반 DI (스프링 DI) 예제 - applicationContext.xml, Speaker.java, Tv.java, TvMain.java

~~~xml
    <bean id="speaker" class="com.di.spring_di_xml_constructor_ex1.Speaker"/>
    <bean id="tv" class="com.di.spring_di_xml_constructor_ex1.Tv">
        <!-- 생성자 기반 의존성 주입 : nameService 참조-->
        <constructor-arg ref="speaker"/>
    </bean>
~~~

~~~java
package com.di.spring_di_xml_constructor_ex1;

public class Speaker {
    public void volumeUp() {
        System.out.println("볼륨을 키웁니다.");
    }
    public void volumeDown() {
        System.out.println("볼륨을 낮춥니다.");
    }
}
~~~

~~~java
package com.di.spring_di_xml_constructor_ex1;

public class Tv {
    Speaker speaker;

    public Tv (Speaker speaker) {
        this.speaker = speaker;
    }
    public void Up() {
        speaker.volumeUp();
    }
    public void Down() {
        speaker.volumeDown();
    }
}
~~~

~~~java
package com.di.spring_di_xml_constructor_ex1;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

public class TvMain {
    public static void main(String[] args) {
        AbstractApplicationContext context = new GenericXmlApplicationContext("applicationContext.xml");
        Tv tv = context.getBean("tv", Tv.class);
        tv.Up();
        tv.Down();
        context.close();
    }
}
~~~

### XML을 이용한 DI (Setter 기반)
- 클래스에 반드시 Setter 메소드가 있어야 함
- 스프링 설정 파일(xml)에서 \<property> 태그 이용하여 의존 객체 주입
  - \<bean id=”nameService” class=”...” />
  - \<property name=”nameService” ref=”nameService” />
    - name : setter 메소드 이름 
      - setNameService()를 이용해서 객체를 주입하겠다는 의미
    - ref : 참조 객체(빈) 이름
- setter 메소드를 사용할 때는 기본 생성자 외에 다른 생성자(매개변수가 있는 생성자)를 정의해서는 안 됨

#### Spring DI - XML을 이용한 DI - Setter 기반 DI 예제 - applicationContext2.xml, NameService.java, NameController.java, NameMain.java

~~~xml
    <bean id="nameService" class="com.di.spring_di_xml_setter.NameService" />
    <bean id="nameController" class="com.di.spring_di_xml_setter.NameController">
        <!-- Setter 기반 의존성 주입 : name(setter 메소드 이름 : setNameService()), ref(의존성있는 빈) -->
        <property name="nameService" ref="nameService" />
    </bean>
~~~

~~~java
package com.di.spring_di_xml_setter;

public class NameService {
    // 이름 전달 받아서  "내 이름은 ~ 입니다" 반환하는 메소드
    public String showName(String name) {
        System.out.println("NameService showName() 메소드");
        String myName = "내 이름은 " + name + " 입니다.";
        return myName;
    }
}
~~~

~~~java
package com.di.spring_di_xml_setter;

public class NameController {
    NameService nameService;

    // 생성자 없고 Setter 메소드를 통해서 외부에서 주입 받음
    public void setNameService(NameService nameService) {
        this.nameService = nameService;
    }
    public void show(String name) {
        System.out.println("NameController : " + nameService.showName(name));
    }
}
~~~

~~~java
package com.di.spring_di_xml_setter;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

public class NameMain {
    public static void main(String[] args) {
        AbstractApplicationContext context = new GenericXmlApplicationContext("applicationContext2.xml");
        NameController controller = context.getBean("nameController", NameController.class);
        controller.show("강길동");
        context.close();
    }
}
~~~

#### Spring DI - XML을 이용한 DI - Setter 기반 DI - 연습문제 - applicationContext2.xml, Speaker.java, Tv.java, TvMain.java

~~~xml
    <bean id="speaker" class="com.di.spring_di_xml_setter_ex1.Speaker" />
    <bean id="tv" class="com.di.spring_di_xml_setter_ex1.Tv">
        <!-- Setter 기반 의존성 주입 : name(setter 메소드 이름 : setNameService()), ref(의존성있는 빈) -->
        <property name="speaker" ref="speaker" />
    </bean>
~~~

~~~java
package com.di.spring_di_xml_setter_ex1;

public class Speaker {
    public void volumeUp() {
        System.out.println("볼륨을 키웁니다.");
    }
    public void volumeDown() {
        System.out.println("볼륨을 낮춥니다.");
    }
}
~~~

~~~java
package com.di.spring_di_xml_setter_ex1;

public class Tv {
    Speaker speaker;

    public void setSpeaker(Speaker speaker) {
        this.speaker = speaker;
    }
    public void Up() {
        speaker.volumeUp();
    }
    public void Down() {
        speaker.volumeDown();
    }
}
~~~

~~~java
package com.di.spring_di_xml_setter_ex1;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

public class TvMain {
    public static void main(String[] args) {
        AbstractApplicationContext context = new GenericXmlApplicationContext("applicationContext2.xml");
        Tv tv = context.getBean("tv", Tv.class);
        tv.Up();
        tv.Down();
        context.close();
    }
}
~~~

### XML을 이용한 DI (생성자 기반 데이터 설정)
- \<constructor-arg value=”홍길동” /> // 값 설정
- 매개변수가 있는 생성자에게 값 전달

#### Spring DI - XML 기반 - 생성자 기반 - 데이터 설정 - applicationContext2.xml, BMI.java, Member.java, MemberMain.java

~~~xml
    <bean id="bmi" class="com.di.spring_di_xml_constructor_value.BMI"/>
    <bean id="member" class="com.di.spring_di_xml_constructor_value.Member">
        <!-- 생성자 기반 의존성 주입 -->
        <constructor-arg ref="bmi"/>
        <!-- 매개변수 있는 생성자 사용하므로 값 설정 -->
        <constructor-arg value="홍길동" />
        <constructor-arg value="24" />
        <constructor-arg value="177" />
        <constructor-arg value="59" />
        <constructor-arg><!-- ArrayList 값 설정-->
            <list>
                <value>수영</value>
                <value>헬스</value>
                <value>에어로빅</value>
            </list>
        </constructor-arg>
    </bean>
~~~

~~~java
package com.di.spring_di_xml_constructor_value;

public class BMI {
    public void showBMI(float height, float weight) {
        float bmi = weight/(height * height) * 10000;

        String result;
        if(bmi >= 25) {
            result = "비만입니다.";
        }
        else if(bmi < 25 && bmi >= 23) {
            result = "과체중입니다.";
        }
        else if(bmi < 23 && bmi >= 18.5) {
            result = "정상";
        }
        else {
            result = "저체중";
        }
        System.out.println("BMI 지수 : " + bmi + " - " + result);
    }
}
~~~

~~~java
package com.di.spring_di_xml_constructor_value;

import java.util.ArrayList;

public class Member {
    private BMI bmi;
    private String name;
    private int age;
    private float height;
    private float weight;
    private ArrayList<String> courses;

    // 생성자 기반 DI
    public Member(BMI bmi, String name, int age, float height, float weight, ArrayList<String> courses) {
        this.bmi = bmi;
        this.name = name;
        this.age = age;
        this.height = height;
        this.weight = weight;
        this.courses = courses;
    }

    public BMI getBmi() {
        return bmi;
    }
    public void setBmi(BMI bmi) {
        this.bmi = bmi;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
    public float getHeight() {
        return height;
    }
    public void setHeight(float height) {
        this.height = height;
    }
    public float getWeight() {
        return weight;
    }
    public void setWeight(float weight) {
        this.weight = weight;
    }
    public ArrayList<String> getCourses() {
        return courses;
    }
    public void setCourses(ArrayList<String> courses) {
        this.courses = courses;
    }
    public void showBMI() {
        bmi.showBMI(height, weight);
    }

    @Override
    public String toString() {
        return "Member{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", height=" + height +
                ", weight=" + weight +
                ", courses=" + courses +
                '}';
    }
}
~~~

~~~java
package com.di.spring_di_xml_constructor_value;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

public class MemberMain {
    public static void main(String[] args) {
        AbstractApplicationContext context = new GenericXmlApplicationContext("applicationContext2.xml");
        Member member = context.getBean("member", Member.class);
        System.out.println(member); // toString 자동 호출
        member.showBMI();
        context.close();
    }
}
~~~