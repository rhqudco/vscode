# day_7 정리 (2021.11.09 화요일)

## 타입에 따른 입력값 전달
- 자바에서의 변수 종류
  - 기본형(boolean, byte, char, short, int, float, double)
    - 메인 메모리와는 별개의 공간을 갖기 때문에 서로 영향이 없다.
  - 참조형(String, Array, ...)
    - 메인 메모리에 영향을 끼친다.
- Call By Value
  - 변수의 값을 전달한다.
- Call By Reference
  - 변수의 위치를 전달

~~~java
import java.lang.reflect.Array;
import java.util.Arrays;

public class Method_2 {
    static void primitive_method(int a, int b) { // 기본형 전달
        System.out.printf("before a : [%d], b:[%d]\n", a,b);
        int temp = b;
        b = a;
        a = temp;
        System.out.printf("after a : [%d], b:[%d]\n", a,b);
    }
    static void reference_method(int [] arr) { // 참조형
        // 전달받은 배열에 전환
        Arrays.sort(arr);
        System.out.print("reference_method");
        System.out.println(Arrays.toString(arr));
    }
    // 참조형 반환이 있는 메소드 정의
    static int[] sub(int n) {
        // 전달받은 n크기의 배열을 생성 전달
        int[] arr = new int[n];
        // 확인하기 위해 정수 배열에 값 할당
        for(int i = 0; i < arr.length; i++)  {
            arr[i] = i+1;
        }
        return arr;
    }
    public static void main(String[] args) {
        int a = 10;
        int b = 20;
        primitive_method(10, 20);
        System.out.printf("main a : [%d], b:[%d]\n\n", a,b);

        int[] arr = {5,4,3,2,1};
        System.out.println("main method 함수 호출 전 " + Arrays.toString(arr));
        // main 메소드의 arr가 영향을 받는다.
        reference_method(arr);
        System.out.println("main method 함수 호출 후 " + Arrays.toString(arr));

        // sub 메소드 호출
        System.out.println("호출 " + Arrays.toString(sub(5)));
        int[] ret = sub(5);
        System.out.println("재사용 " + Arrays.toString(ret));
    }
}
~~~

## 참조형 변수의 반환
- 참조형 타입의 변수를 반환할 때 주소(시작주소)가 반환된다.

## 재귀호출
- Recursive Call
- 자기 자신을 호출하는 메소드
  - 반복의 또 다른 형태
- 종료 조건을 넣어주지 않으면 Stack 메모리에 계속 쌓이게 된다.
  - 접근하면 안되는 메모리에 접근하거나 메모리가 꽉 차게된다면 시스템이 다운될 수 있음.
  - 종료될 수 있는 조건을 명확하게 명시해야 한다.

~~~java
public class Recursive_Call { // 종료 조건이 명시된 재귀호출
    static void recursive(int n) {
        if(n > 10) {
            return;
        }
        System.out.println(n);
        recursive(n+1);
    }
    public static void main(String[] args) {
        recursive(1);
    }
}
~~~

~~~java
public class Recursive_Call { // 종료 조건이 명시되지 않은 재귀호출
    static void recursive() {
        recursive();
    }
    public static void main(String[] args) {
        recursive();
    }
}
~~~

## 객체지향 프로그래밍
- Object Oriented Programing
- 객체지향 프로그래밍이 나온 이유
  - 커지는 소스코드의 양을 감당하지 못했다.
    - 발달하는 하드웨어에 따라 처리양이 늘어남
    - 복잡해지는 프로그램
    - 소스코드가 너무 방대하여 유지보수가 어렵다.
  - 대규모 소프트웨어의 개발의 어려움을 해소하기 위해 나온 개념
- 소프트웨어를 관리하고 개발하는 전체적인 '방법론'
  - 계획 - 요구사항 분석 - 설계 - 구현(개발) - 테스트 - 배포 - 유지보수
  - 소프트웨어 공학
- 클래스나 객체는 객체지향에서 아주 일부분

## 클래스
- 사용자가 정의하는 새로운 타입으로 해석할 수 있다
  - 이는 아주 작은 부분으로 해석하는 것에 불과.
  - 기본 타입을 제외한 String, Array는 자바에서 미리 정의된 클래스라볼 수 있다.
  - 이러한 클래스르 새로운 타입으로 정의
- 미리 정의된 클래스 뿐 아니라 직접 클래스를 정의해서 사용할 수 있다
- 클래스의 이름은 대문자로 하는 것이 좋다.
  - 클래스를 제외한 변수의 이름이나 메소드의 이름은 소문자로 정의

~~~java
class 클래스이름 { // 클래스의 이름은 대문자로 시작하는 것이 좋다.
  //클래스 블록
}
~~~

## 객체
- object(객체), instence(인스턴스)
- 클래스는 정의이다.
  - 정의된 클래스를 사용하기 위해서는 메모리에 공간을 만들어줘야 한다.
  - 정의된 클래스를 메모리에 생성하면 객체라고 한다.
    - '인스턴스'화 한다고 표현
- 객체란 메소드 호출과 같다.
  - 메소도를 호출하면 메모리에 만들어진다(콜스택)
  - 클래스를 호출하면 클래스가 메모리에 만들어진다.
  - 메소드는 실행이 끝나면 사라지지만 객체는 사라지지 않는다.
    - 클래스는 종료라는 개념이 없다.
      - 직접 삭제하지 않으면 메모리에 계속 존재
        - 이것을 '객체'라고 한다.
- 같은 클래스의 객체를 여러 개 생성
  - 동일한 타입의 변수가 여러 개인 것으로 볼 수 있다.
  - 타입만 같을 뿐 메모리의 위치는 다르기 때문에 생성되는 변수는 다르다.
- 모든 것은 주소를 기준으로 구분한다.
  - 변수, 메소드, 클래스, 객체를 구분하는 기준은 메모리
  - 같아 보이는 객체도 주소가 다르면 다른 객체
  - 달라 보이는 객체도 주소가 같으면 같은 객체
  
~~~java
class Person { // 간단한 클래스 정의

}
public class Practice {
    public static void main(String[] args) {
        // 클래스를 통해 객체 생성
        // new를 통해 class호출
        new Person();
        // 이렇게 생성하면 이후에 객체에 접근할 방법이 없다.
        // 그렇기 때문에 참조 변수를둔다.
        System.out.println(new Person()); // Person@3f0ee7cb
        System.out.println(new Person()); // Person@75bd9247
        Person person = new Person();
        System.out.println(person); // Person@7dc36524
        System.out.println(person); // Person@7dc36524
        Person person1 = new Person();
        System.out.println(person1); // Person@35bbe5e8
        System.out.println(person1); // Person@35bbe5e8
        // 같은 클래스를 통해 생성된 모두 다른 객체
        
        // 형태에 따라 주소가 다르다.
        // 변수(참조변수)를 통해서 객체에 접근
        // 일반적으로, 객체지향 프로그래밍에서 변수를 하나의 객체로 취급
        // 정확하게 변수와 객체는 다르다.
        // 변수를 객체와 동일시 해서 코드를 작성해도 무방하다.

        Person person2 = person;
        System.out.println(person); // Person@7d417077
        System.out.println(person2); // Person@7d417077
        // 얕은 복사
        // 두 객체는 같은 객체가 된다.
    }
}
~~~

## 클래스의 구조
- 속성(변수)과 기능(메소드)로 정의될 수 있다.
  - 클래스 내의 변수를 멤버변수 라고 표현
  - 하나의 클래스 내에는 여러 개의 변수와 여러 개의 메소드

~~~java
class Persons {
    String name;
    int age;
}
public class Prectice_2 {
    public static void main(String[] args) {
        Persons p1 = new Persons();
        Persons p2 = new Persons();
        // .을 통해서 접근(객체의 속성에 접근)
        // 객체.속성
        // 객체.기능()
        p1.age = 24;
        p1.name = "rhqudco";
        // 서로 다른 객체
        // 객체변수는 공유되지 않는다.
        System.out.println("이름 : " + p1.name + " 나이 : " + p1.age); // 이름 : rhqudco 나이 : 24
        System.out.println("이름 : " + p2.name + " 나이 : " + p2.age); // 이름 : null 나이 : 0

    }
}
~~~

## 자바의 변수 종류
- 클래스 변수
  - 정적(static)변수
  - 공유변수
  - 동일한 타입의 클래스의 객체가 모두 같은 변수를공유
  - 메모리에 한 번만 생성
- 인스턴스(객체) 변수
  - 클래스 내에서 정의된 변수
  - 메소드 외부, 클래스 내부
  - 객체.속성명
  - 객체변수는 각 객체에 속한 고유 메모리에 만들어진다.
    - 메소드의 지역변수와 마찬가지
    - 객체간 속성은 공유되지 않는다.
- 지역 변수
  - 메소드 내에서 선언(정의)된 변수
  - Parameter도 지역변수
  - 지역 변수는 메소드의 범위를 벗어날 수 없다.

~~~java
// 간단한 클래스를 정의
class Persons {
  // 변수를 정의(사람에 대한 속성)
    //객체 변수(인스턴스 변수)
    String name;
    int age;
    // 클래스 변수(정적 변수)
    static int share = 10;
    
    void method() {
        System.out.println();
        int a = 10;
        a++;
        System.out.println(a);
    }
}
public class Prectice_2 {
    public static void main(String[] args) {
        Persons p1 = new Persons();
        Persons p2 = new Persons();
        // .을 통해서 접근(객체의 속성에 접근)
        // 객체.속성
        // 객체.기능()
        p1.age = 24;
        p1.name = "rhqudco";
        // 서로 다른 객체
        // 객체변수는 공유되지 않는다.
        System.out.println("이름 : " + p1.name + " 나이 : " + p1.age); // 이름 : rhqudco 나이 : 24
        System.out.println("이름 : " + p2.name + " 나이 : " + p2.age); // 이름 : null 나이 : 0

        System.out.println(++p1.share);
        System.out.println(p2.share);
        
        // 객체내의 메소드를 호출하는 경우에도 동일하게 .을 통해 접근
        // 클래스내의 메소드는 서로 다른 변수.
        p1.method();
        p2.method();
        
        // 메소드안에 정의된 변수 a는 접근 불가능
        // p1.a;
    }
}
~~~

## this
- 객체 자기 자신을 나타낸다

~~~java
class Persons {
    String name;
    int age;
    static int share = 10;
    //객체의 속성을 출력해주는 메소드 정의
    void info() {
        System.out.println("이름: " + this.name + " 나이: " + this.age);
    }
    // 속성을 정의하는 메소드 추가
    // Setter라고 표현
    // 메소드 이름 앞에 set을 붙여서 표현
    void setName(String name) {
        // 전달받은 매개변수로 객체변수 초기화
        // 둘 다 지역변수의 name
        // 지역변수와 객체변수가 이름이 동일하면 지역변수가 우선
        System.out.print("this : ");
        System.out.println(this);
        // this를 이용해서 객체변수를 구분
        this.name = name;
        //지역변수    객체변수
    }
}
public class Prectice_2 {
    public static void main(String[] args) {
        Persons p1 = new Persons();
        Persons p2 = new Persons();

        p1.setName("장동건");
        System.out.print("p1 : ");
        System.out.println(p1);
        p1.info();
    }
}
~~~

## 생성자
- Constructor
- 생성 메소드 정도로 이해하자.
  - 약간 특별한 메소드
  - 초기화 할 때 사용
- 객체를 생성할 때 자동으로 호출되기 때문에 직접 호출하지 않는다

~~~java
class Persons {
    String name;
    int age;
    static int share = 10;

    // 생성자
    // 객체가 생성될 때 값이 할당 되길 바라면 사용
    // 반환 타입이 없다.
    // 클래스의 이름과 메소드의 이름이 동일해야 한다.
    Persons(String name, int age) {
        System.out.println("생성자 실행");
        this.name = name;
        this.age = age;
    }

    void info() {
        System.out.println("이름: " + this.name + " 나이: " + this.age);
    }

    void setName(String name) {
        this.name = name;
    }
}
public class Prectice_2 {
    public static void main(String[] args) {
        // 생성자는 직접 호출하지 않는다
        // 객체를 생성할 때 자동으로 호출
        // 콜백 메소드
        // 생성자를 만들 때 작성했던 파라미터 값에 맞춰서 작성
        Persons p1 = new Persons("장돈건", 10);
        Persons p2 = new Persons("웡빈", 20);
        p1.info();
        p2.info();

    }
}
~~~

## Static method & Instance method
- (Instance)인스턴스 메소드
  - 생성자를 제외한 정의된 메소드는 전부 '인스턴스 메소드'
  - 객체를 통해서 호출할 수 있다
- 클래스 메소드(Static method)
  - 클래스 변수와 객체 변수는 메모리에 생성되는 시점이 다르다
    - 클래스 변수는 객체보다 먼저 메모리에 생성
    - 객체변수는 객체가 생성될 때 메모리에 생성
    - 객체가 생성되기 전 메모리에 만들어진 클래스 변수를 객체를 통해서 접근해야 한다?
    - 객체가 없어도 호출 가능한 메소드 정의
      - 클래스 이름으로 호출 가능.
  
~~~java
class Other {
    int adad = 1130;
}

class Persons {
    String name; // 객체변수
    int age; // 객체변수
    static int share = 10; // 클래스 변수

    // 생성자
    // 객체가 생성될 때 값이 할당 되길 바라면 사용
    // 반환 타입이 없다.
    // 클래스의 이름과 메소드의 이름이 동일해야 한다.
    Persons(String name, int age) {
        System.out.println("생성자 실행");
        this.name = name;
        this.age = age;
    }

    // 클래스 메소드(static method)
    static void getshare() {
        System.out.println(share);
        // 객체변수에 대한 접근 불가능
        // static으로 선언된 변수만 사용 가능

        // 다른 클래스의 객체 변수는 접근 가능
        Other other = new Other();
        int a = other.adad;
        System.out.println(a);
    }

    void info() {
        System.out.println("이름: " + this.name + " 나이: " + this.age);
    }

    void setName(String name) {
        this.name = name;
    }
}
public class Prectice_2 {
    public static void main(String[] args) {

        //객체를 생성하지 않아도 클래스를 통해서 호출
        Persons.getshare();


        Persons p1 = new Persons("장돈건", 10);
        Persons p2 = new Persons("웡빈", 20);
        p1.info();
        p2.info();

    }
}
~~~

## 클래스의 특징
- 메소드와 변수를 하나의 타입으로 묶어놓은 것이 클래스
  - 비슷한 특징을 가지고 있는 여러 메소드와 변수를 특징별로 클래스화 했다
    - 관리가 쉬워진다
- 은닉성(Capsulation) : 클래스를 보호하기 위한 장치
- 상속(Inherit) : 재사용성을 더 확대한 개념
- 다형성(Pholymophism) : 오버로딩(Overloading), 오버라이딩(Overriding)

### 은닉성
- 클래스 내에서 정의된 변수나 메소드에 대해 외부에서 함부로 접근하지 못하도록 비공개로 하는 것
  - 객체지향에서 클래스는 제공되는 기능이 어떻게 동작하는지 알 필요 없다.
    - String클래스나 Array클래스 등 클래스 외부에서 클래스의 속성이나 기능을 알 수 없게하고 사용법만 알게 함.
- 일반적으로 객체지향 프로그래밍에서 모든 속성을 비공개로 하는 것이 원칙.
  - 외부 접근이 필요하다면 메소드를 통해 접근할 수 있도록 제공하는 것이 좋다.
- 접근제어자(Access Modifier)
1. private : 동일 클래스 안에서만 접근 가능(외부 접근 불가)
2. default : 접근제어자가 명시되지 않은 것(기본값) 동일 패키지 안에서만 접근 가능
3. protected : 해당 클래스를 상속 받은 외부 패키지의 클래스까지 가능
4. public : 제한 없다
- private -> default -> protected -> public  ->순서로 접근이 쉽다.

### 상속
- 물려받는다는 의미
- 클래스의 재사용성을 더 극대화
- 예를 들면, 미리 정의된 사람 클래스를 상속 받아서 나머지 학생에 대한 속성이나 기능만 추가하면 되도록 하는 것을 상속이라 한다.
  - 잘 정의된 클래스가 있다면 다시 정의해서 사용하지 않고 재사용 할 수 있다.
  - 물려받은 클래스를 더 확장해서 사용
- 여러 개의 클래스가 서로 유기적으로 연결되어 동작
- 객체지향 프로그래밍에서 가장 중요한건 클래스의 설계
- 클래스와 클래스간 관계를 표현
  - is - a (상속)
  - has - a (다른 클래스의 객체를 속성으로 갖는 경우)
  - 클래스의 상속은 큰 개념에서 작은으로 상속

### 다형성

### 오버로딩
- 상속과는 무관한 개념
- 오버로딩의 조건
  1. 오버로딩 하는 메소드의 이름은 반드시 같아야 한다
  2. 오버로딩 하는 메소드의 매개변수는 반드시 달라야한다.

~~~java
class Persons {
    String name; // 객체변수
    int age; // 객체변수
    static int share = 10; // 클래스 변수

    // 생성자 오버로딩
    Persons() {

    }

    Persons(String name, int age) {
        this.name = name;
        this.age = age;
    }
    /*
    .........
    */
// Persons 상속 받아서 student클래스 정의
class Student extends Persons{
    // 정의된 내용이 없어도 물려받은 속성과 기능 사용 가능.

    // 입력되는 수가 없어도, 한 개여도, 세 개여도 동작하도록 하고 싶을 때 오버로딩 사용
    int add () {return 10 + 20;}
    int add(int a) {return a+20;}
    int add(int a, int b, int c) {return a+b+c;}
    int add(int a, int b) {
        return a+b;
    }
    String add(String c, String d) {return c+d;}
}
public class Prectice_2 {
    public static void main(String[] args) {

        Student s1 = new Student();

        System.out.println(s1.add(10,20));
        System.out.println(s1.add());
        System.out.println(s1.add(10));
        System.out.println(s1.add(10,20,30));
        System.out.println(s1.add("Hello", "java"));

        // 생성자 오버로딩
        Persons p1 = new Persons();
        p1.info();

        Persons p2 = new Persons("wkdehdrjs", 20);
        p2.info();
    }
}
    }
}
~~~

### 오버라이딩
- 메소드 재정의
- 부모 클래스로부터 물려받은 메소드를 자식 클래스가 재정의해서 사용
- 오버라이딩의 조건
  1. 재정의 하려는 메소드와 물려받은 메소드의 이름이 같아야 한다.
  2. 리턴 타입, 매개변수 개수, 타입이 모두 같아야 한다.
- 부모 클래스의 메소드를 사용하고 싶다면
  - super 사용


~~~java
class Persons {
    String name; // 객체변수
    int age; // 객체변수
    static int share = 10; // 클래스 변수
    /*
    .........
    */
    void info() {
        System.out.println("이름: " + this.name + " 나이: " + this.age);
    }
    /*
    .........
    */
}

// Persons 상속 받아서 student클래스 정의
class Student extends Persons{
    String school;
    // 정의된 내용이 없어도 물려받은 속성과 기능 사용 가능.
    // 생성자는 상속되지 않는다.
    // 생성자를 정의하지 않으면 기본 생성자가 존재하고 따로 정의 한다면 기본 생성자는 만들어지지 않는다.
    Student() {};
    Student(String name, int age, String school) {
        this.name = name;
        this.age = age;
        this.school = school;
}
public class Prectice_2 {
    public static void main(String[] args) {

        Student s1 = new Student("wkdehdrjs", 20, "dnjseo");
        s1.info();

    }
}
~~~