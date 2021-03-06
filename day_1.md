# day_1 정리 (2021.11.01 월요일)
## 세대별 언어
- 세대별
  - 1세대
    - 절차지향 언어(C, Potran 등)
      - 함수를 통한 코드의 재사용성 증가
      - 소스코드의 관리와 유지보수
  - 2세대
    - 객체지향 언어(Java, C++, Go 등)
      - 자바는 객체지향 다운언어
      - 클래스를 통한 코드의 재사용성 증가
  - 3세대
    - 함수형 언어
## Java?
- 자바란?
  - 자바의 특징
    - JVM(Java Virtual Machine)에서 동작하기 때문에 운영체제에 의존하지 않고 동작할 수 있다.
    - 동작 순서 (Java -> Byte Code -> JVM -> OS -> CPU)
  
    - 자바는 무조건 Class안에 들어가 있어야 작동한다.
    - 반드시 한 개의 main을 가지고 있어야 한다.(Java로 동작하는 모든 프로그램의 시작은 main)
  - Java의 장점
    - 객체지향 언어
      - Class를 통한 코드의 재사용성 증가
    - 객체지향이지만 함수형 문법을 지원한다.
      - lamda 식으로 사용 가능
## 코드 작성 시 주의 사항
  1. main이 있는 클래스와 없는 클래스로 나뉘며 main이 있는 클래스의 이름은 파일의 이름과 반드시 같아야 한다.
  2. 명령의 끝에는 세미콜론(;)을 붙여줘여 한다.
  3. 코드를 작성할 때 공백과 대/소문자는 구분한다.

## 메모리(Memory)
- 자료를 저장할 수 있는 공간
  - 명령어를 실행한 결과, 파일에서 읽은 내용 등을 메모리 어딘가에 저장하고, 필요할 때 꺼내서 사용한다.
  - 자료를 처리하고 싶은 경우, 그 자료는 반드시 메모리에 있어야 한다.
  - 이런 개념을 프로그래밍 언어에서 변수(Variable)라고 한다.
  - 자료가 메모리 어디에 위치한지는 알 필요가 없다. -> JVM이 알아서 해주기 때문!

## 바이트(Byte)?
-  정보를 표현하는 최소 단위 : bit
   -  1bit = 0 또는 1을 표현
- bit가 8개 즉, 8bit가 된다면 1byte라고 한다.
  - 1byte(8bit)는 2^8개의 정보를 표현할 수 있다.
- byte단위
  - 1024byte가 되면 1kb로 표현한다.
  - 1024kb = 1mb
  - 1024mb = 1gb
  - 1024gb = 1tb
  - 등...

## 주소(address)
- 메모리 어딘가에 변수가 저장된 위치.
- 자료는 비트의 형태로 저장되며, 1byte마다 번호가 부여된다.
  - 메모리의 첫 번째 바이트의 주소는 0
  - 그 이후부터 1씩 증가하며 차례대로 번호 부여
- 값이 저장된 위치(주소)를 알고 있어야 한다.
  - 모르면 값을 다시 사용할 수 없기 때문
  - 주소는 숫자로 되어 있고, 값이 저장된 위치를 전부 기억할 수 없다.
  - 자바는 메모리의 주소를 이용한 접근을 허용하지 않는다.

## 변수(Variable)
- 변수란 주소 대신 사용할 수 있는 이름
- 변수의 3대 요소
  1. 주소
  2. 값
  3. 크기
- 변수 선언
  - 자료형 (int, float, string, char, double 등)
  - 이름 
    - 첫글자는 숫자로 하면 안되고 중복된 이름과 예약어는 허용하지 않으며, 영어(대/소문자 구분), 언더바(_), 스트링($), 숫자만 사용 가능하지만 스트링은 거의 사용하지 않는다.
  - 값 (자료형에 맞는 값을 저장해야 한다.)
  - int(자료형) a_1(이름) = 5(값);
- 변수의 종류
  - 정수
    - byte, short, int, long(각 1, 2, 4, 8byte)
  - 실수(부동소수점, 고정소수점)
    - float, double(각 4, 8byte)
    - 유리수만 표현 가능
  - 논리형
    - 참, 거짓으로 나뉘는 변수(true, false)
    - 1byte
  - 문자
    - 2byte
    - char
    - char a = 'a'; 이런 식으로 단일 문자는 작은따옴표에 감싸서 사용한다.
  - 문자열
    - String
    - String str = "This is String"; 이런 식으로 큰따옴표에 감싸서 사용한다.

## 컴퓨터가 문자를 처리하는 방법
- 컴퓨터는 숫자만 처리할 수 있다.
  - 정확하게는 2진수(0,1)로만 처리 가능
    - 때문에 문자는 처리할 수 없다.
- 하지만 문자를 처리하는 방법이 있다
  - 문자에 대응되는 숫자를 만들었기 때문.
    - ASCII코드라고 한다.
      - 0~127까지 128개의 문자에 대한 숫자 테이플(표준)
      - 모든 시스템이 동일한 값을 사용
    - 1byte가 8bit인 이유
      - 8개의 bit면 모든 문자를 전부 포현할 수 있음
        - 2^8 = 256(0~255)
      - 맨 앞에 있는 bit는 MSB
        - MSB(Most Signature Bit / 최상위 부호 비트) -> 음수 = 1, 양수 = 0
        - MSB를 제외한 나머지 7bit(2^7 = 128(0~127))로 표현
  - 한글은 어떻게 처리?
    - 새로운 문자 인코딩을 만듬(표준이 아니다.)
      - 표준이 아니기 때문에 깨지는 이슈가 발생
    - 한글을 표현할 수 있는 인코딩 셋
      - UTF-8
      - CP949
      - EUC-KR(CP949의 하위호환)
- 눈으로 보이는 것이 전부가 아니고 공백, 줄 바꿈, 탭도 표현한다.ㄴ
  - 키보드를 통해 입력할 수 있는 모든 값을 처리할 수 있다.
    - 엔터키도 문자이다.
      - CR(Carriage Return/해당 라인의 가장 앞으로 이동), LF(Line Feed/다음 라인)이 합쳐진 문자.

## 주석
 -  //를 먼저 쓰고 뒤에 내용을 작성하면 //를 쓴 곳 한 줄은 주석처리 되어 컴파일할 때 무시한다.
    -  // 이곳은 주석을 작성 했습니다.
  
 - /* ... */ 아래와 같이 작성하면 여러 줄 주석처리 할 수 있다.
     - /* 이곳은 주석을 작성 했습니다. */