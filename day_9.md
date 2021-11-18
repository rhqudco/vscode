# day_9 정리 (2021.11.11 목요일)

## 다형성
- 객체의 다형성
  - 하나의 객체가 여러 개의 타입을 가질수 있는 것을 뜻한다.

~~~java
class Tv {
    boolean power;
    int channel;

    void power() {power = !power;}
    void channelUp() {channel++;}
    void channelDown() {channel--;}

}

class CaptionTv extends Tv {
    String text;
    void caption() {}
}

class Other {

}

public class Poly {
    public static void main(String[] args) {
        // is-a 관계
        // CaptionTv는 Tv다
        // CaptionTv is Tv
        Tv t0 = new Tv();
        CaptionTv t2 = new CaptionTv();

        // Tv에 CaptionTv가 포함되어 있기 때문에 가능
        Tv t1 = new CaptionTv();

        t1.channelUp();
        t1.power();

        //t2.text; Tv타입의 참조형 변수는 자식 타입의 속성까지는 알 수 없다.

        t2.channelDown();
        t2.power();
        t2.text = "Unknown";

        // CaptionTv에 Tv는 포함되어 있지 않기 때문에 불가능
        // CaptionTv t4 = new Tv();

        // 참조변수와 객체 타입이 다르면 안된다.
        // Tv t3  = new Other();

        Tv[] arrT = new Tv[10]; // Tv 타입만을 원소로 가질 수 있다.
    }
}
~~~

## 추상 클래스
- 추상 메소드를 포함하는 클래스를 추상 클래스라 한다.
  - 추상 메소드란 선언만 되어있고 내부는 정의되어 있지 않은 메소드
- 완성되지 않은 클래스
  - 인스턴스화 할 수 없다.
    - 객체로 생성될 수 없다는 의미
    - 반드시 상속을 통해서 추상 메소드를 재정의 해야(오버라이딩) 인스턴스화 할 수 있다.
  
~~~java
abstract class Abstract   { // 추상 메소드가 하나라도 있으면 추상메소드라고 함
    //선언만 되어 있고 내부가 정의되어 있지 않은 메소드
    abstract void abstractMethod();

    void generalMethod() {
        System.out.println("일반 메소드");
    }
}

class General extends Abstract {
    // 메소드 재정의(오버라이딩)을 통해 완성시킨다.
    void abstractMethod() {
        System.out.println("추상 메소드 완성");
    }
    
}

public class Absmethod {
    public static void main(String[] args) {
        Abstract obj = new Abstract(); // 오류 만들 수 없다!
        General robj = new General(); // 만들 수 있다.
    }
}
~~~

## 인터페이스
- 추상 클래스의 한 종류
- 추상 메소드만을 가지는 추상 클래스를 '인터페이스'라고 한다.
- 인터페이스의 상속은 extends가 아닌, implements로 상속이 된다.
- 다중 상속은 허용하지 않지만 한 개의 클래스(일반, 추상)와 여러 개의 인터페이스는 상속 가능

~~~java
interface Interface{
    abstract void abstractMethod1();
    abstract void abstractMethod2();
    abstract void abstractMethod3();
}

// 인터페이스의 상속은 extends가 아닌, implements로 상속이 된다.
// 여러 개의 인터페이스를 상속 받아서 구현
// 다중 상속은 허용하지 않지만 한 개의 클래스(일반, 추상)와 여러 개의 인터페이스는 상속 가능
class Sample implements Interface {
    @Override
    public void abstractMethod1() {
        System.out.println("1");
    }

    @Override
    public void abstractMethod2() {
        System.out.println("2");
    }

    @Override
    public void abstractMethod3() {
        System.out.println("3");
    }
}
public class Inter {
    public static void main(String[] args) {
        Sample s = new Sample();
    }
}
~~~

~~~java
// 동물 클래스
class Animal {
    String name;

    public void setName(String name) {
        this.name = name;
    }
}

interface Ground {

}

/*interface Bird {
    public String getAction();
}*/
abstract class Bird extends Animal {
    // 추상 메소드와 일반 메소드가 같이 구현
    public abstract String getAction();
    public String getName() {
        System.out.println("너의 이름은 : " + this.name);
        return this.name;
    }
}
interface Foodable {
    public void food();
}

// 인터페이스끼리는 extends를 통해서 여러 개의 인터페이스를 상속받을 수 있다.
interface GroundFoodable extends Ground, Foodable {

}

class Tiger extends Animal implements GroundFoodable {

    public void food() {
        System.out.println("닭");
    }
}

class Lion extends Animal implements GroundFoodable {
    public void food() {
        System.out.println("바나나");
    }
}

class Monkey extends Animal implements GroundFoodable {
    public void food() {
        System.out.println("소고기");
    }
}

class Eagle extends Bird implements Foodable {
    Eagle() { this.name = "독수리"; }
    public String getAction() {return "fly";}
    public void food() {
        System.out.println("지렁이");
    }
}
class Duck extends Bird implements Foodable {
    Duck() { this.name = "오리"; }
    public String getAction() {return "fly";}
    public void food() {
        System.out.println("물고기");
    }
}
class Tazo extends Bird implements Foodable {
    Tazo() { this.name = "타조"; }
    public String getAction() {return "Walk";}
    public void food() {
        System.out.println("사료");
    }
}

class Zoo {

    // 메소드 오버로딩(메소드 이름, 접근제어자는 같고 매개변수(타입, 갯수)가 다르다.)
    // 호랑이가 입력되면 닭을 출력
    // 원숭이가 입력되면 바나나를 출력
    /*public void food(Tiger tiger) {
        System.out.println("닭");
    }
    public void food(Monkey monkey) {
        System.out.println("바나나");
    }*/

    // 메소드 오버로딩(메소드 이름, 접근제어자는 같고 매개변수(타입, 갯수)가 다르다.)
    public void action(Ground ground) {
        System.out.println("Walk");
    }
    public void action(Bird bird) {
        System.out.println(bird.getAction());
    }
    //	public void food( Animal animal ) {
//		// 동물에 따라서 음식을 다르게 표현
//		// 객체지향은 아래와 같이 코드가 늘어나는 것을 좋아하지 않습니다.
//		if ( animal instanceof Tiger ) System.out.println("닭");
//		else if ( animal instanceof Monkey ) System.out.println("바나나");
//		else if ( animal instanceof Lion ) System.out.println("소고기");
//		else if ( animal instanceof Eagle) System.out.println("지렁이");
//
//	}
    public void food(Foodable animal) {
        animal.food();
    }
}

public class All {
    public static void main(String[] args) {
        Zoo zoo = new Zoo();
        Tiger tiger = new Tiger();
        Monkey monkey = new Monkey();
        Lion lion = new Lion();
        Eagle eagle = new Eagle();
        Duck duck = new Duck();
        Tazo tazo = new Tazo();
        zoo.action(tiger);
        zoo.action(monkey);
        zoo.action(lion);
        zoo.action(eagle);
        zoo.action(duck);
        zoo.action(tazo);

        zoo.food(tiger);
        zoo.food(monkey);

        eagle.getName();
    }
}
~~~

## 오버로딩 vs 오버라이딩
- 오버로딩은 상속을 필요로 하지 않는다
  - 해당 클래스 내에서 같은 이름의 여러 메소드
- 오버라이딩은 반드시 상속이 되어야 한다.
  - 상속된 메소드에 대해서 재정의

## 패키지와 예외처리
### 패키지
- 자바의 클래스들을 모아놓은 폴더
  - 폴더의 경로를 표현할 때 사용하는 구분자
    - Windows : \
    - 맥, 리눅스 : /
    - 자바에서는 패키지 경로 표기할 때 .을 사용
- 모든 클래스는 반드시 하나의 패키지에 포함
- 동일한 특징을 갖는 여러 개의 클래스를 하나의 폴더로 관리하는 방법
- 하나의 소스파일(.java)에는 첫 번째 문장으로 단 한 번의 패키지를 선언할 수 있다.

## 예외처리
- 코드를 작성하며 발생하는 예외에 대한 처리 방법 2가지
1. 고전적인 예외처리(LBYL)
   - Look Before Tou Leap(도약하기 전에 확인 해라)
   - 코드를 실행하기 전에 예외가 발생하지 않도록 미리 검증하고 실행을 하자
   - 즉, 발생할 수 있는 모든 예외적인 상황들에 대해서 미리 예측하고, 미연에 하겠다는 뜻
   - 현실적으로 불가능.
     - 완벽하게 예외를 제어할 수 없다.
     - 완전한 소프트웨어는 불가능 하
2. EAFP
   - It's Easier Ask Forgiveness Than Permission
   - 허락보다 용서가 쉽다.
   - 일단 실행하고 예외가 발생하면 그때 처리
   - 고전적인 방법보다 예외 관리가 더 쉬워진다.

## 예외의 종류
- 에러는 예외의 한 종류
- 예외에도 여러가지가 있다(경고, 에러 등)
- 에러는 여러가지 예외들 중에서도 프로그램 실행에 영향을 줄만큼 심각한 오류
- 에러 또한 여러가지 종류
  - 컴파일 에러
    - 컴파일 할 때 발생하는 에러(javac)
      - *.java -> *.class
    - 대부분은 문법적인 오류
      - 처리가 쉽다
  - 런타임 에러
    - 문법 오류는 체크 끝(실행에는 문제가 없다)
    - 실행했을 때 문제가 나오는 경우
    - 해결이 어렵다.

## 예외의 기본 구조
- 예외가 발생할 것 같은 코드를 'try' 구문으로 감싼다.
  - 자바는 'try'로 감싸진 블록에 있는 명령으에 대하여 모니터링 수행
- 예외가 발생하면 'catch'블록으로 예외를 넘기게 됩니다.
  - 'catch'구문에서 해당 예외를 처리
  - if-else if와 방식이 동일.
- 예외가 발생하는 곳과 예외가 처리되는 곳이 다를 수 있다.
- 예외는 발생하면 어디에서든 반드시 처리를 해줘야 한다.
~~~java
...
try {
    ....
}
catch(예외1) {
    ....
}
catch(예외2) {
    ....
}
...
~~~

### 처리방법 1
~~~java
public class Prac {
    public static void main(String[] args) {
        int num = 100;
        int re = 0;
        for(int i = 0; i < 10; i++) {
            try {
                re = num / (int) (Math.random() * 10);
            } catch (ArithmeticException e) {
                System.out.println("Arithmetic Error");
            } catch (Exception e) {
                System.out.println("Another Error");
            } finally {
                System.out.println("예외가 발생 하든 안하든 무조건 실행");
            }
            System.out.println(re);
        }
    }
}
~~~

### 처리방법 2
~~~java
import java.util.Objects;
class Sub {
    public int convToInt(String strs) {
        return Integer.parseInt(strs); // 예외가 발생하는 곳
    }
}
class Other extends Object {
    public int middleMethod(String strs) {
        Sub s =new Sub();
        try {
            return s.convToInt(strs);
        }catch (Exception e) {
            System.out.println("middleMethod에서 예외 처리");
        }
        return 0;
    }
}


public class Excep {
    public static void main(String[] args) {
        Other exam = new Other();
        int num = 0;
        try {
            num = exam.middleMethod("a");
        } catch (Exception e) {
            System.out.println("여기까지 왔네.");
        }

        System.out.println(num);
    }
}
~~~

### 처리방법 3

~~~java
import java.util.*;

// 모든 예외는 Exception 클래스를 상속 받아서 정의
// 직접 예외를 정의
class MyException extends Exception {
    MyException() {
        System.out.println("내가 만든 예외");
    }
}

// 예외의 흐름
class Sub {
    public int convToInt( String strs ) {
        try {
            return Integer.parseInt(strs); // 예외가 발생하는 곳
        } catch(Exception e) {
            System.out.println("예외가 발생한 곳에서 처리");
            // 예외도 객체
            throw new ArithmeticException();
        }
//		return 0;
    }
}

class Other extends Object {
    public int middleMethod( String strs ) throws MyException {
        Sub s = new Sub();
        try {
            return s.convToInt(strs);
        } catch (ArithmeticException e) {
            System.out.println("middleMethod에서 예외가 처리됨");
            throw new MyException();
        }
//		return 0;
    }
}

public class Excep {
    public static void main(String [] args) {
        Other exam = new Other();
        int num = 0;
        try {
            num = exam.middleMethod("a");
        } catch(Exception e) {
            System.out.println("결국 여기까지 오고야 말았구나");
        }
        System.out.println(num);
    }
}
~~~

## 프로세스
- 운영체제에서 작업을 실행하는 단위
  - 포그라운드
    - 눈에 보이는 프로세스
  - 백그라운드
    - 눈에 보이지 않는 프로세스 
- 스레드
  - 프로세스의 작업 단위
  - 프로세스는 자신이 해야 되는 작업을 여러 개의 스레드로 작게 쪼갤 수 있다.
  - 이렇게 쪼개진 여러 개의 스레드를 '동시'에 실행(병렬)

~~~java
//  간단한 쓰레드 실행
public class Threa extends Thread{
    int num;
    Threa(int num) {
        this.num = num;
    }
    public void run() {
        System.out.println(this.num + "번 thread 실행");
    }
    public static void main(String[] args) {
        for(int i = 0; i <= 10; i++) {
            Threa th = new Threa(i);
            th.start(); // start를 통해 run을 실행시킬 수 있다.
        }
        System.out.println("Main End");
    }
}
~~~