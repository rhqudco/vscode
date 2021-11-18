# day_2 정리 (2021.11.02 화요일)
## 메모리
- 스토리지에 자료가 있다면, 프로그램
- 메모리에 자료가 있다면, 프로세스가 된다
  - 프로세서는 CPU

## 문자(문자열)
- 문자는 (' '), 문자열은 (" ")
  - 문자열은 여러 개의 단일 문자의 집합이다.
- 문자열의 비교는 "=="를 통해 비교하지 않고 equals 클래스를 사용해서 비교한다.

## CR, LF
- CR = 0x0d
- LF = 0x0a
- 공백 = 0x20
- 탭 = 0x09

## ASCII
- 아스키코드 값이 같으면 두 문자는 다르게 보여도 같은 문자이다
  - font에 따라 달라지기 때문.

## 문자열 이스케이프
1. 문자를 사용할 때 충돌이 발생하는 경우
 - 다른 용도로 사용하고 싶은 경우 충돌이 발생한다.
   - 용도가 정해진 문자들이 있다
   - 대표적으로 작은따옴표('), 큰따옴표(") 등이 있다.
     - 이럴 경우 따옴표를 사용하기 위하여 탈출 시킨다. 탈출은 탈출 할 문자 앞에 역슬래쉬(\)를 삽입. "\"Hello World\""
     - 역슬래쉬도 역슬래쉬로 탈출한다. (\\) -> (\)만 출력
2. 반대인 경우
  - 특별한 의미가 없는 문자인데, 특별한 의미를 부여해서 사용
    - 엔터(CR + LF)가 대표적이다.
    - 엔터는 입력할 수 없기 때문에 엔터를 대신하여 사용 할 New Line(\n)을 만들었다.

## 변수와 상수
- 상수(Constant)
  - 변하지 않는 수
  - 변수의 상수화
    - final을 붙여주면 변수는 상수가 된다.
      - 반드시 선언과 정의를 동시에 해야한다.
      - 일반적으로 대문자를 사용해서 표기한다.(꼭 지킬 필요는 없지만 사회적으로 합의)
- 변수
  - 변하는 수

## 타입 변환
- 타입이 가지는 가장 중요한 의미는 "크기" 이다.
  - 크기에 따른 문제
  - 작은 자료형을 큰 자료형에서 표현할 수는 있지만, 큰 자료형에서 작은 자료형을 표현할 수 없다.
    - 강제 형변환을 사용하면 오류는 나지 않음
      - (작은 자료형)큰 자료형 변수 이름 -> (short)num(num은 int형);
- 실수에서 정수로 바꾸는 경우
  - 가수부가 떨어져 나가면서 지수부만 남게 된다.(올림, 반올림, 버림)
    - 반올림 -> Math.round : Math클래스의 round함수
    - 올림 -> Math.ceil : Math클래스의 ceil함수
    - 내림 -> Math.floor : Math클래스의 floor함수 

## 형변환
### 문자 -> 숫자
  #### - String to Int
  ~~~java
  //Integer.paseInt(String값)
  //Integer.valueOf(String값)

  String s_num = "10";
  int i_num = Integer.parseInt(s_num); //String -> Int 1번방식
  int i_num2 = Integer.valueOf(s_num); //String -> Int 2번방식
  ~~~

  #### - String to Double, Float
  ~~~java
    //Double.valueOf(String값)
    //Float.valueOf(String값)

    String s_num = "10";
    double d_num = Double.valueOf(s_num); //String -> Double
    float f_num = Float.valueOf(s_num); //String -> Float
  ~~~

  #### - String to Long, Short 
  ~~~java
  //Long.parseLong(String값)
  //Short.parseShort(String값)

  String s_num = "10";
  long l_num = Long.parseLong(s_num); //String -> Long
  short sh_num = Short.parseShort(s_num); //String -> Short
  ~~~

### 숫자 -> 문자
  #### - Int to String
~~~java
//String.valueOf(Int값)
//Integer.toString(Int값)

int i_num = 10;
String s_num;
		
s_num = String.valueOf(i_num); //문자 -> 숫자 1번방식
s_num = Integer.toString(i_num); //문자 -> 숫자 2번방식
s_num = ""+i_num; //문자 -> 숫자 3번방식
   ~~~

  #### - Double, float to String
  ~~~java
  //String.valueOf(Float값,Double값)
  //Float.toString(Float값,Double값)

  float f_num = 10.10;
  double d_num = 10.10;
		
  String s_num;

  s_num = String.valueOf(f_num); //Float -> String 1번방식
  s_num = Float.toString(f_num); //Float -> String 2번방식
		
  s_num = String.valueOf(d_num); //Double -> String 1번방식
  s_num = Double.toString(d_num); //Double -> String 2번방식
  ~~~

### 정수 <-> 실수
  #### - Double,Float to Int
~~~java
//(int)실수값
double d_num = 10.101010;
float f_num = 10.1010

int i_num;
i_num = (int)d_num; //Double-> Int
i_num = (int)f_num; //Float -> Int
~~~

  #### - Int to Double, Float
~~~java
//(int)실수값
int i_num = 10;
	
double d_num = (double)i_num; //Int -> Double
float f_num = (float)i_num; //Int -> Float
~~~

## 표준 출력
- 표준을 통한 출력
  - 표준이라는 이름을 사용(출력이 이미 정해져 있음을 의미)
  - 표준 출력의 기본 형태는 문자열
  - println
    - 한 줄을 출력
  - printf
    - f는 format string
    - 출력할 때 출력 형태를 직접 지정할 수 있다.
    - 출력할 문자열을 미리 구성하고 출력한다.
      - 출력하려는 문자열 내에 %가 붙은 문자를 형식지정자 라고 한다.
        - 불리언 : %b
        - 정수 : %d
        - 문자열 : %s
        - 실수 : %f(부동소수점 형태로 출력)
        - 8진수 : %o
        - 16진수 : %x
  
## 표준 입/출력
- 자바에서 스트림은 닫히기 전까지 스트림을 계속 유지한다.

## 표준 입력
- 표준 입력은 문자(문자열)만 입력 가능
- Scanner 클래스를 이용하면 가장 쉽게 처리할 수 있다
  - 사용은 쉽지만 속도가 느리고, 메모리를 많이 사용한다는 단점이 존재
  - next()는 단어별로 입력.
    - 단어별 구분은 공백, 탭, 뉴라인으로 한다.
  ~~~java
  public class Hello {
    public static void main(String[] args){

        Scanner scan = new Scanner(System.in);
        int ab = scan.nextInt(); // 정수
        String abav = scan.next(); // 단어(문자열)
        String add = scan.nextLine(); // 라인 입력
        System.out.println(ab);
    }
}
~~~

- InputStream
  - 문자 한개 입력(정수형으로 입력 받음, 여러 문자를 작성해도 첫 글자만 입력 받을 수 있다.)
  ~~~java
  public class Hello {
    public static void main(String[] args) throws IOException {

        InputStream in  = System.in;
        int a = in.read();
        System.out.println(a);
        in.close();
        // 무조건 아스키 코드값으로 입력된다. 숫자 1 입력 -> 49 출력
        // A 입력 -> 65, a 입력 -> 97
    }
}
~~~
- InputStreamReader
  - 배열에 저장하는 모든 문자
  ~~~java
  public class Hello {
    public static void main(String[] args) throws IOException {

        InputStream in  = System.in;
        InputStreamReader reader = new InputStreamReader(in);
        char[] a = new char[1024];
        reader.read(a);
    }
}
  ~~~
- BufferdReader
  - 엔터를 누르기 전에 입력한 모든 값을 저장.
  ~~~java
  public class Hello {
    public static void main(String[] args) throws IOException {
        
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str = br.readLine();
        System.out.println(str);
    }
}
  ~~~
  - BufferWriter
  - 저장된 값을 빠르게 출력할 때 사용
  ~~~java
  public class Hello {
    public static void main(String[] args) throws IOException {
        
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        bw.write("출력");
        bw.flush();
    }
}
  ~~~

## 객체
- 변수는 곧 객체이다.
  - 변수를 하나의 물체라고 해석한다.