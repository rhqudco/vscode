# SQLday_7 정리 (2021.11.26 금요일)
## 연습문제
- db4 패키지 생성
- product  테이블 사용
- ProductDTO
- ProductDAO
- 생성자에서 DB 연결
- insertProduct() : 데이터 저장 (insert)
- selectProduct() : 데이터 출력 (select)
- ProductEx
- 데이터 입력하고
- insertProduct() 호출해서 데이터 저장
- selectProduct() 호출해서 데이터 출력

##### ProductDTO

~~~java
package productDB5;

public class ProductDTO {
    String prdNo;
    String prdName;
    int prdPrice;
    String prdMaker;
    String prdColor;
    String ctgNo;

    public ProductDTO(String prdNo, String prdName, int prdPrice, String prdMaker, String prdColor, String ctgNo) {
        this.prdNo = prdNo;
        this.prdName = prdName;
        this.prdPrice = prdPrice;
        this.prdMaker = prdMaker;
        this.prdColor = prdColor;
        this.ctgNo = ctgNo;
    }

    public String getPrdNo() {
        return prdNo;
    }

    public void setPrdNo(String prdNo) {
        this.prdNo = prdNo;
    }

    public String getPrdName() {
        return prdName;
    }

    public void setPrdName(String prdName) {
        this.prdName = prdName;
    }

    public int getPrdPrice() {
        return prdPrice;
    }

    public void setPrdPrice(int prdPrice) {
        this.prdPrice = prdPrice;
    }

    public String getPrdMaker() {
        return prdMaker;
    }

    public void setPrdMaker(String prdMaker) {
        this.prdMaker = prdMaker;
    }

    public String getPrdColor() {
        return prdColor;
    }

    public void setPrdColor(String prdColor) {
        this.prdColor = prdColor;
    }

    public String getCtgNo() {
        return ctgNo;
    }

    public void setCtgNo(String ctgNo) {
        this.ctgNo = ctgNo;
    }
}
~~~

##### ProductDAO

~~~java
package productDB5;

import db5.StudentDTO;

import java.sql.*;

public class ProductDAO {
    Connection connection;
    PreparedStatement preparedStatement;
    ResultSet resultset;


    // DB연결 생성자
    public ProductDAO() {
        try {
            String url = "jdbc:mysql://localhost:3306/sqldb6?serverTimezone=UTC";
            String user = "root";
            String pwd = "";

            connection = DriverManager.getConnection(url, user, pwd);

            if(connection != null) {
                System.out.println("연결 성공");
            }
        } catch (Exception e) {
            System.out.println("연결 오류 발생!");
            e.printStackTrace();
        }
    }
    // select Method
    public void selectProduct()  {
        try {
            String sql = "select * from product order by prdNo";
            preparedStatement = connection.prepareStatement(sql);
            resultset = preparedStatement.executeQuery(sql);

            while (resultset.next()) {
                String prdNo = resultset.getString(1);
                String prdName = resultset.getString(2);
                int prdPrice = resultset.getInt(3);
                String prdMaker = resultset.getString(4);
                String prdColor = resultset.getString(5);
                String ctgNo = resultset.getString(6);
                System.out.format("%-10s \t %-10s\t %-4d\t %-20s\t %13s\t %s  \n",
                        prdNo, prdName, prdPrice, prdMaker, prdColor, ctgNo);
            }
        } catch(Exception e) {
            System.out.println("select 오류 발생!");
            e.printStackTrace();
        }
    }
    // insert Method
    public void insertProduct(ProductDTO productDTO) {
        try{
            String sql = "insert into product values(?, ?, ?, ?, ?, ?)";
            PreparedStatement preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setString(1, productDTO.getPrdNo());
            preparedStatement.setString(2, productDTO.getPrdName());
            preparedStatement.setInt(3, productDTO.getPrdPrice());
            preparedStatement.setString(4, productDTO.getPrdMaker());
            preparedStatement.setString(5, productDTO.getPrdColor());
            preparedStatement.setString(6, productDTO.getCtgNo());
            int result = preparedStatement.executeUpdate();
            if(result > 0) {
                System.out.println("성공");
            }
        }catch (Exception e) {
            System.out.println("insert 오류 발생!");
            e.printStackTrace();
        }
    }
}
~~~

##### ProductInsert

~~~java
package productDB5;

import student.StudentDAO;
import student.StudentDTO;

import java.util.Scanner;

public class ProductInsert {
    public void productInsert() {

    Scanner scan = new Scanner(System.in);
    ProductDAO productDAO = new ProductDAO();

    System.out.print("제품 번호 입력 ");
    String prdNo = scan.nextLine();

    System.out.print("제품명 입력 ");
    String prdName = scan.nextLine();

    System.out.print("가격 입력 ");
    int prdPrice = scan.nextInt();
        scan.nextLine();

    System.out.print("제조사 입력 ");
    String prdMaker = scan.nextLine();

    System.out.print("색상 입력 ");
    String prdColor = scan.nextLine();

    System.out.print("카테고리 입력 ");
    String ctgNo = scan.nextLine();

    ProductDTO productDTO =
            new ProductDTO(prdNo, prdName, prdPrice, prdMaker, prdColor, ctgNo);
    productDAO.insertProduct(productDTO);
    }
}
~~~

##### ProductSelect

~~~java
package productDB5;

public class ProductSelect {
    public void productSelect() {
        ProductDAO productDAO = new ProductDAO();
        productDAO.selectProduct();
    }
}
~~~

##### ProductEx

~~~java
package productDB5;

import java.util.Scanner;

public class ProductEx {
    public static void main(String[] args) {
        System.out.println("************************************");
        System.out.println("\t 제품 관리 프로그램");
        System.out.println("************************************");
        System.out.println("\t 메뉴에서 선택");
        System.out.println("************************************");
        System.out.println("1. 제품 등록");
        System.out.println("2. 제품 정보 조회");
        System.out.println("3. 제품 정보 수정");
        System.out.println("4. 제품 정보 삭제");
        System.out.println("5. 종료");
        System.out.println("************************************");
        Scanner scan = new Scanner(System.in);
        int choice = scan.nextInt();
        switch (choice) {
            case 1:
                ProductInsert productInsert = new ProductInsert();
                productInsert.productInsert();
                break;
            case 2:
                ProductSelect productSelect = new ProductSelect();
                productSelect.productSelect();
                break;
            case 3:
                break;
            case 4:
                break;
            case 5:
                break;
            default:
                System.out.println("잘못된 입력");
                break;
        }
    }
}
~~~

# Algorithmday_1 정리 (2021.11.26 금요일)

## 알고리즘
- 문제 해결을 위해 논리 정연한 절차에 의해 계획한 해결 방은을 정형적이고 체계적으로 기술한 것
- 주어진 문제를 해역하기 위해 구체적인 작업을 하기 전 어떤 구조와 방법으로 구성할 것인지 생각하는 기본적인 설계
- 문제를 해결하기 위해 단계별로 명확하게 기술하여 나열한 일련의 명령어(혹은 다른 것이 될 수도 있음)들의 모임
- 문제 -> 문제 분석 -> 설계 -> 검증 -> 구현 -> 결과
- 어떤 문제를 해결하기 위해 나열한 계산적인 절차
- 절차 실행 후 주어진 문제에서 요구하는 결과 출력
- 수행 절차
  - 입력 -> 수행 -> 출력
    - 입력 : 문제의 각 사례에서 포함하고 있는 숫자 또는 문자들
    - 출력 : 알고리즘이 수행된 후에 얻을 수 있는 문제에 대한 해답.
- 문제를 제대로 해결하기 위해서는 입/출력, 정확성, 유한성, 명확성, 유효성이 충족되어야 한다.
  - 입/출력(Input/Output) : 외부로부터 0개 이상의 입력을 받아 1개 이상의 출력, 외부에서 입력 받지 않는 경우 내부에서 자체적으로 생성
  - 정확성(Corerectness) : 문제가 허용하는 범위 내에서는 모든 경우의 가능한 입력에 대하여 정확한 출력을 생성해야 하지만 문제가 복잡한 경우 증명 과정이 난해하고 방대하며 모든 입력에 대한 테스트는 불가능하다. 따라서 오류를 완전히 배제할 수 없는 문제점이 있다.
  - 유한성(Finiteness) : 유한한 단계가 실행된 후 반드시 종료 되어야 함. 예기치 못한 데이터나 상황에 의해 무한하게 반복해서는 안된다.
  - 명확성(Definiteness) : 모든 명령어와 절차는 컴퓨터의 작동 원리에 기반하여 정확하고 명료하게 나타나야 한다.
  - 유효성(Effectiveness) : 알고리즘에서 요구하는 연산은 컴퓨터에서 처리될 수 있어야 한다.
- 알고리즘을 표현할 수 있는 방법은 많지만, 처리할 내용을 전달할 수 있는 방법이면 어떠한 형태든 가능하다. 하지만 절차와 명령을 명확하게 기술해야 한다.
- 알고리즘 표현법
  - 기호로 표현
  - 프로그래밍 언어로 표현
  - 수학적 수식으로 표현

## 알고리즘의 성능
- 공간적 자원과 시간적 자원
- 자원을 적게 요구하는 알고리즘의 성능이 더 좋다고 표현
- 공간적 자원
  - 컴파일된 프로그램을 이루는 명령어 저장공간(프로그램의 스토리지에 저장되는 크기)
  - 프로그램이 실행되는 공간 필요한 데이터 저장 공간(프로그램이 사용하는 메모리)
- 시간적 자원
  - 알고리즘이 구현된 프로그램의 실행이 시작되어 종료될 때 까지 걸리는 시간
- 시간 복잡도
  - 알고리즘의 시간적 성능을 분석하기 위해 입력 크기 n에 대한 기본 연산의 실행 횟수를 함수 형태로 나타낸 것
  - T(n) = n
  - T(n) = n - 1
  - T(n) = n^2
  - T(n) = n(n-1)/2
  - ....
- 알고리즘의 시간 복잡도 계산 예
  - 정수형 배열의 각 원소를 더해서 그 합을 출력
    - A = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}, sum = 0
    - 배열의 크기가 10이기 때문이 상위 조건에서는 총 10회로 배열의 크기가 n일 경우 총 실행 횟수은 n이 된다.
    - 시간 복잡도 : T(n) = n이다.
    - A = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}, sum = 1
    - 배열의 크기가 10이지만 A[0]이 1이고, sum이 1이기 때문에 A[1]부터 계산하면 된다
    - 시간 복잡도 T(n) = n-1이다.

## 알고리즘 순서도(Flowchart)
- 처리하고자 하는 문제의 순서와 상호간의 관계를 일정한 기호로 표현한 그림
- 순서도의 역할
  - 코딩의 기초 자료로 활용
  - 문제의 이해성 증대
  - 디버깅 용이
  - 보관, 유지보수 등 문서로 역할
- 순서도의 종류
  - 개략 순서도
    - 전체 내용을 쉽게 파악할 수 있도록 중요한 부분만 블록으로 간략하게 표현
    - 시작 -> 초기값 저장 -> 1부터 n까지 1씩 증가하며 변수에 누적 -> 누적된 변수값 출력 -> 끝
  - 상세 순서도
    - 컴퓨터가 수행할 수 있는 명령문 단위로 세부화 하여 상세하게 표현
    - 상세 순서도를 코딩하면 원시 프로그램이 된다.
    - (시작) -> [n = 0, s = 0] -> [n = n + 1, s = s + n] -> <n < 10(맞으면 [n = n + 1, s = s + n]으로) 아니면 다음 블록으로> -> 합계 = s 출력 -> 끝
- 순서도의 기본 유형
  - 직선형
    - 한 명령이 처리되면 다음 명령이 순서적으로 처리되는 형태로 가장 기본적
  - 분기형
    - 조건을 비교하여 결과에 따라 서로 다른 처리를 수행할 때 사용
    - 조건의 결과가 참, 거짓으로 나뉜다.
  - 반복형
    - 조건이 만족되는 동안 반복 구간의 처리 내용을 반복적으로 실행하는 구조
    - 수행 여부는 반복 전 또는 후에 결정
    - 반복 전 판단 방법
      - 조건을 비교한 후 조건을 만족했을 경우에만 반복 구간의 명령 수행
      - 조건에 따라 한번도 반복되지 않는 경우 발생 가능
- 양음의 덧셈
  - 1부터 100까지 정수
  - 1-2+3-4+5…. +97-98+99-100의 총합을 구하여 출력

~~~java
package AlgoPractice;

public class Ex1 {
    public static void main(String[] args) {
        int sum = 0;
        for(int i  = 1; i <= 100; i++) {
            if(i % 2 == 0) sum -= i;
            else sum += i;
        }
        System.out.println(sum);
    }
}
~~~

## 알고리즘 설계 기법
- 문제를 해결해 나가는 기법
- 알고리즘이 채택한 전략이나 관점
- 대표적인 알고리즘 설계 기법
  - 분할 정복 기법(Divide and Conquer)
  - 욕심쟁이 기법(Greedy Method)
  - 동적 프로그래밍 기법(Dynamic Programming)

### 분할 정복 기법(Divide and Conquer)
- 하향식 설계 기법
- 문제의 크기를 작게 나누어서 좀 더 쉽게 해결할 수 있는 상태로 변환하여 문제를 해결하는 방법
  - 하나의 문제를 어러 개의 작은 문제로 나누어 동일한 해결 기법을 계속적으로 적용한 후 결과들을 연합하여 원래의 문제를 해결
- 분할된 문제들의 크기가 여전히 클 경우 다시 분할을 하여 분할 정복 기법을 적용
  - 각 부분 문제들이 간단히 해결될 수 있는 상태에 이를 때까지 반복(순환 : Recursion)
- 재귀함수는 분할 정복 기법을 위한 구현 기술
- 분할된 작은 문제들이 서로 동일한 경우가 많이 발생되면서 재귀적으로 처리하는 알고리즘에 중복된 계산이 계속 발생
- 이를 방지하기 위해 동적 프로그래밍 기법 사용
- 분할 정복 기법으로 최대 / 최소 값 구하는 예의 알고리즘 처리 과정
  - 분할
    - [45, 7, 2, 36, 61, 25, 22, 15]
    - [45, 7, 2, 36], [61, 25, 22, 15]
    - [45, 7], [2, 36], [61, 25], [22, 15]
      - [max = 45, min = 7], [max = 36, min = 2], [max = 61, min = 25], [max = 22, min = 15]
  - 결합
    - [45, 7, 2, 36], [61, 25, 22, 15]
      - [max = 45, min = 2], [max = 61, min = 15]
    - [45, 7, 2, 36, 61, 25, 22, 15]
      - [max = 61, min = 2]

#### 분할 정복 기법 응용 예
- 이진 탐색
  - Binary Search
  - 전체 데이터 집합을 두 부분으로 나누어 검색하는 방법
  - 값이 어느 부분에 속하는지 결정하여 그 부분에 대하여 순환적으로 탐색을 수행
  - 정렬된 리스트에서 중간에 위치한 키 값과 찾고자 하는 값이 같으면 탐색 성공
  - 서로 다르면, 중간 항목을 기준으로 두 부분 중 한쪽 리스트를 선택하여 키를 정한 후 다시 이진 탐색하여 찾으면 성공
  - 없으면, 나머지 다른 한 쪽 이진 탐색
  1. {1,3,5,6,7,9,11,20,30} 중간 값 7로 키 설정
  2. 5가 7보다 작으니까 7을 기준으로 왼쪽 부분이 탐색 영역
  3. 중간 값 3을 키로 설정하여 5와 비교하니 3이 더 작기 때문에 오른쪽으로 이동
  4. 5를 찾음.
  - 리스트가 정렬되어 있는 경우에 적합한 탐색 방법
  - 데이터의 삽입, 삭제가 빈번하게 발생되는 경우 리스트 재구성에 의해 항목들의 이동이 요구되기 때문에 적합하지 않고 삽입, 삭제가 거의 없는 경우 적합
- 이(2)원합병 정렬
  - Two-way merge sort
  - 정렬된 두 개의 리스트를 혼합하여 완전히 정렬된 하나의 리스트로 합하는 방식
  1. 6, 9, 2, 12, 8, 34, 23, 33, 56, 17, 56, 32
  2. (6, 9), (2, 12), (8, 34), (23, 33), (17, 56), (32, 56)
  3. (2, 6, 9, 12), (8, 23, 33, 34), (17, 36, 56, 56)
  4. (2, 6, 9, 9, 12, 23, 33, 34), (17, 36, 56, 56)
  5. {2, 6, 8, 9, 12, 17, 23, 32, 33, 34, 56, 56}
- 퀵 정렬
  - Quick-Sort
  - 전체 리스트를 2개의 부분 리스트로 분할하고
  - 각각의 서브 리스트를 다시 퀵정렬로 정렬
  - 기준 값 보다 큰 값들을 오른쪽으로, 작은 값들을 왼쪽으로 재 배열
  - __정렬 방법__
    - 전체 리스트에서 한 원소를 기준 값(pivot)으로 선정
    - 피벗을 기존으로 두 개의 서브 리스트로 분할
      - 왼쪽 서브 리스트
        - 피벗 보다 작은 값의 원소들로 구성
      - 오른쪽 서브 리스트
        - 피벗 보다 큰 값의 원소들로 구성
    - 각각의 파티션에 대해 다시 퀵 정렬을 순환 적용
      - 피벗 선정 및 파티션 분할

#### 재귀적 알고리즘
- 재귀(Recursion 순환)
- 알고리즘이나 함수가 수행 도중에 자기 자신을 다시 호출하여 문제를 해결하는 기법
- 분할 및 정복에 사용
- 고려사항
  - 호출할 때 마다 처리할 문제의 크기는 계속 작아져야 한다.
  - 무한히 계속되지 않도록 종료 조건이 있어야 한다.
- 장점
  - 함수에서 실행해야 하는 작업의 특성에 따라 일반적인 호출방식보다 프로그램의 크기를 줄이고 간단하게 작성 가능

- 재귀 호출 예(Factorial)

~~~java
package AlgoPractice;

import java.util.Scanner;

public class Ex3 {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        System.out.print("정수 입력 : ");
        int f = scan.nextInt();
        System.out.print(f + "! = ");
        System.out.println("1 = " + factorial(f));
    }
    static int factorial(int num) {
        if(num == 0 || num == 1) {
            return 1;
        }
        else {
            System.out.print(num + " * ");
            return num * factorial(num - 1);
        }
    }
}
~~~

- 재귀 호출 예(Fibonacci numbers)

~~~java
package AlgoPractice;

import java.util.Scanner;

public class Fibonacci {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        System.out.print("항의 개수 입력 : ");
        int fib = scan.nextInt();
        for (int i = 1; i <= fib; i++) {
            System.out.print(fibonacci(i) + " ");
        }
    }
    static int fibonacci(int num) {
        if(num == 1 || num == 2) {
            return 1;
        }
        else {
            return fibonacci(num - 2) + fibonacci(num - 1);
        }
    }
}
~~~

- 재귀 호출 예(Tower of Hanoi)

~~~java
package AlgoPractice;

import java.util.Scanner;

public class Hanoi {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        System.out.print("원판 개수 입력 : ");
        int num = scan.nextInt();
        tower(1, 2, 3, num);
    }
    static void tower(int tower1, int tower2, int tower3, int n){ // tower1 -> tower3로 원판 이동
        //System.out.printf("[tower1 : %d] [tower2 : %d] [tower3 : %d] [n : %d]\n", tower1, tower2, tower3, n);
        if(n == 0) {
            return;
        }
        tower(tower1, tower3, tower2 ,n-1); // 원판  n-1을 tower1 -> tower3으로 이등
        System.out.printf("원판 [%d](를)을 기둥[%d]에서 기둥[%d](으)로 이동\n", n, tower1, tower3);
        tower(tower2, tower1, tower3, n-1); // 원판 n-1을 tower2 -> tower3으로 이동
    }
}
~~~

### 욕심쟁이 기법(Greedy Method)
- 최적 대합을 구성할 수 있는 집합을 만들기 위해 필요한 원소들 각 단계마다 하나씩 선택해 나가는 방법
- 선택을 하는 매 순간마다 현재 상태에서 가장 좋아보이는 원소를 선택하는 전략
- 최적의 해를 찾는 전형적인 방법
- 즉, 각 순간 지역적으로 가장 좋아 보이는 선택이 모여 최종적으로도 가장 좋을 것이라 생각하기 때문에 나온 기법
- 최적화 문제를 해결할 수는 없지만 많은 경우의 문제에 적용 가능

#### 욕심쟁이 기법 적용 예
- 배낭 채우기 문제
  - n개의 물건과 배낭이 있을 때 어떤 물건을 선택해서 배낭에 넣으면 배낭 안이 있는 물건들의 총 가격이 가장 크게 되는가?
  - 단, 배낭에 넣을 수 있는 최대 무게가 제한되어 있어 물건은 이 무게를 넘지 않아야 한다.
  - 연습문제
    - 배낭의 제한 무게 : 15kg
    - 물건의 가격 : (1번째 60원 - 4Kg) (2번째 45원 - 9Kg) (3번째 21원 - 7Kg) (4번째 12원 - 3Kg)
    - 1Kg당 가격 : (1번째 15원) (2번째 5원) (3번째 3원) (4번째 4원)
    - 각 물건은 분할 가능
    - 최대로 담을 수 있는 물건들과 총 가격은? -> (1번째 물건 4Kg), (2번째 물건 9Kg), (4번째 물건 2Kg) 총 113원
- 거스름돈 문제
  - 동전의 개수가 최소가 되도록 거스름 돈을 주는 문제
  - 거스름돈 : 890원
  - 가치가 가장 높은 동전부터 내림차순으로 총액이 정확히 거스름돈이 될 때까지 수행
  - 연습문제
  - 5,000원 지폐, 1,000원 지폐, 500원 동전, 100원 동전, 50원 동전, 10원 동전
  - 금액 입력 : 18,793

- 거스름돈 문제 코드

~~~java
package AlgoPractice;

public class ChangeMoney {
    public static void main(String[] args) {
        int money = 18793;
        int[] arr = {5000,1000,500,100,50,10};
        for(int i = 0; i < arr.length; i++) {
            System.out.println(arr[i] + "원 : " + money / arr[i]);
            money %= arr[i];
        }
        System.out.println("남은 돈  : " + money + "원");
    }
}
~~~

- 최단 경로 문제(Dijkstra의 최단 경로 알고리즘)
- 최소 비용 신장 트리(Prim 알고리즘, Kruscal 알고리즘)
