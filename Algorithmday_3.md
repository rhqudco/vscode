# Algorithmday_3 정리 (2021.11.30 화요일)

## 컬렉션 프레임워크(Collection Framework)
- 컬렉션
  - 사전적 의미로 요소(객체)를 수집해 저장한 것
- 프레임워크
  - 라이브러리 프로그래밍 방식
  - 표준화, 정형화된 체계적인 프로그래밍 방식
  - 미리 정해진 방식대로 개발
  - 누가 작성하든 프로그램이 표준화되기 때문에 프로그램 유지보수하기 쉬워진다.
- 컬렉션 프레임워크
  - 컬렉션(다수의 객체)를 다루기 위한 표준화된 프로그래밍 방식
    - 많은 양의 데이터를 저장, 삭제, 검색, 비교, 정렬 작업 등을 편리하게 쉽게 수행
  - 객체들을 효율적으로 추가, 삭제, 검색할 수 있도록 제공되는 컬렉션 라이브러리
  - 인터페이스를 통해서 정형화된 방법으로 다양한 컬렉션 클래스 이용
  - 인터페이스와 다형성을 이용한 객체지향적 설계를 통해 표준화 되어 있기 때문에 사용법 편하고 재사용성이 높은 코드 작성 가능
  - 프로그래머의 프로그래밍 부담을 많이 덜어 줌
  - java.util. * 패키지에 포함
- 자바 컬렉션 
  - 객체를 수집해서 저장하는 역할
- 프레임워크
  - 사용법을 미리 정해 놓은 라이브러리
- 컬렉션 클래스
  - 다수의 데이터를 저장할 수 있는 클래스
  - 예 : ArrayList, Linked List, Vector, HashSet, TreeSet
- 컬렉션 프레임워크의 주요 인터페이스
  - List
    - 순서가 있는 데이터의 집합, 데이터의 중복을 허용한다.
    - ArrayList, Linked List, Vector
  - Set
    - 순서를 유지하지 않는 데이터의 집합, 데이터의 중복을 허용하지 않는다.
    - HashSet
    - TreeSet
  - Map
    - Key-Value 쌍으로 이루어진 데이터의 집합, 순서는 유지되지 않으며 키는 중복을 허용하지 않고, 값은 중복을 허용한다.
    - HashMap
    - HashTable
    - TreeMap
    - Properties
  - List와 Set의 공통된 부분을 뽑아서 새로운 인터페이스 Collection이 추가로 정의되었음
  - Map은 List/Set과 전혀 다른 형태로 컬렉션을 다루기 때문에 같은 상속 계층에 포함되지 못했음
- 컬렉션 프레임워크 특징
  - List, Set, Map 인터페이스 이름이 클래스 이름에 포함되어 있음
  - 이름만으로도 클래스의 특징을 쉽게 알 수 있다.
  - Vector, Stack, HashTable, Properties와 같은 클래스들은 컬렉션 프레임워크가 만들어지기 전부터 존재했기 때문에 컬렉션 프레임워크 명명법을 따르지 않음
  - Vector나 HashTable 등 기존 컬렉션 클래스들은 이전에 작성된 프로그램들과 호환을 위해 설계를 변경해서 남겨둔 것임
  - 가능하면 ArrayList와 HashMap 사용 추천


## List 인터페이스의 특징 및 주요 메소드
- 특징
  - 순서가 있는 집합
  - 인덱스로 관리
  - 중복해서 객체 저장 가능
- 구현 클래스
  - ArrayList
  - LinkedList
  - Vector
- 주요 메소드
  - add(), get(), inEmpty(), size(), remove(), clear()


## ArrayList
- List 인터페이스의 구현 클래스
- 크기가 가변적으로 변하는 선형 리스트
- 배열과 유사(순차리스트, 인덱스 사용)
- 배열과 차이점
  - 배열 : 크기 고정
  - ArrayList : 객체 추가 가능, 저장 용량 초과 시 자동으로 저장 용량 증가
- 단점
  - 데이터를 읽어오고 저장하는데는 효율적이지만, 용량을 변경해야 할 때는 새로운 배열을 생성한 후 기존 배열로부터 새로운 배열로 복사해야 하기 때문에 상당히 비효율적
  - 따라서 처음에 생성할 때 저장할 데이터의 개수를 잘 고려하여 충분한 용량으로 생성하는 것이 좋다.
- 사용법
  - 객체 추가
    - 인덱스 0부터 차례로 저장
  - 객체 제거
    - 바로 뒤 인덱스부터 마지막 인덱스까지 모두 앞으로 1씩 이동
    - 따라서 빈번한 객체 삭제와 삽입이 일어나는 경우 ArrayList를 사용하는 것이 바람직하지 않음 -> Linked List


~~~java
// 제네릭을 사용하지 않을 경우 형변환 필요
List list = new ArrayList();
list.add("abc");
String str = (String)list.get(0);
~~~


~~~java
// 제네릭을 사용할 경우 형변환이 필요 없음.
List<String> list = new ArrayList<String>();
list.add("abc");
String str = list.get(0);
~~~

##### ArrayListEx1(제네릭 사용하지 않는 경우 예제)

~~~java
public class ArrayListEx1 {
    public static void main(String[] args) {
        List list = new ArrayList(5);

        list.add(100);
        list.add(2.55);
        list.add(300);
        list.add(9.9);
        list.add("자바 프로그래밍");
        list.add(1, "데이터베이스"); // 1번 index부터 뒤로 한 칸씩 밀고 1번에 삽입

        System.out.println("리스트 내용 출력");
        for(int i = 0; i <list.size(); i++) {
            System.out.println(i + " : " + list.get(i));
        }
        System.out.println();
        System.out.println("포함 여부 확인");
        System.out.println(list.contains(300)); // trye
        System.out.println(list.contains("자바")); // false

        System.out.println();
        System.out.println("리스트에서 데이터 삭제");
        System.out.println(list.remove(1)); // 1번 인덱스 삭제
        System.out.println(list.remove("자바 프로그래밍")); // 값이 들어있는 인덱스 삭제

        System.out.println();
        System.out.println("리스트 내용 출력");
        for(int i = 0; i <list.size(); i++) {
            System.out.println(i + " : " + list.get(i));
        }
    }
}
~~~

##### ArrayListEx1(제네릭 사용하는 경우 예제)

~~~java
public class ArrayListEx2 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<String>();

        list.add("Java");
        list.add("JDBC");
        list.add("Servlet/JSP");
        list.add("고병채 만세");

        System.out.println();
        System.out.println("전체 내용 출력");
        for(int i = 0; i < list.size(); i++) {
            System.out.println(i + " : " + list.get(i));
        }
        System.out.println();
        System.out.println("전체 내용 출력 2");
        for(String item : list) {
            System.out.println(item);
        }
        System.out.println();
        System.out.println("네 번째 요소 출력 : " + list.get(3));
        System.out.println("네 번째 요소 길이 : " + list.get(3).length()); // 한글도 한 글자당 1개 취급(공백도 1개 취급)

        // 2번 인덱스 위치(세 번째)에 삽입
        list.add(2,"Spring");
        // 총 객체 수 출력
        System.out.println();
        System.out.println("총 객체 수 : " + list.size());
        // 전체 내용 출력
        System.out.println();
        System.out.println("전체 내용 출력 3");
        for(String item : list) {
            System.out.println(item);
        }
        // JDBC 제거
        System.out.println();
        System.out.println("JDBC 제거");
        list.remove("JDBC");
        // Java포함 여부
        System.out.println();
        System.out.println("Java 포함 여부");
        System.out.println(list.contains("Java"));
    }
}
~~~

##### ArrayList 연습문제

- ArrayListEx3

~~~java
public class ArrayListEx3 {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<String>();
        Scanner scan = new Scanner(System.in);
        int temp = 0;
        String str = "";

        for(int i = 0; i < 4; i++) {
            System.out.print("단어 입력 : ");
            list.add(scan.nextLine());
        }
        System.out.println("---------------------------------------------");
        System.out.print("단어 리스트 : ");
        for (int i = 0; i < list.size(); i++) {
            System.out.print(list.get(i) + " ");
            if (temp < list.get(i).length()) {
                temp = list.get(i).length();
                str = list.get(i);
            }
        }
        System.out.println("\n가장 긴 단어 : " + str);
        System.out.println("가장 긴 단어 길이 : " + temp);
    }
}
~~~

- Employee.java

~~~java
public class Employee {
    int id;
    String name;
    double salary;

    public Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    @Override
    public String toString() {
        return  id + " - " + name + " - " + salary;
    }
}
~~~

- EmployeeMain.java

~~~java
public class EmployeeMain {
    public static void main(String[] args) {
        ArrayList<Employee> list = new ArrayList<Employee>(5);
        Employee employee1 = new Employee(100, "김사원", 3300.55);
        Employee employee2 = new Employee(101, "박대리", 4100.20);
        Employee employee3 = new Employee(102, "최과장", 5100.55);

        list.add(employee1);
        list.add(employee2);
        list.add(employee3);
        System.out.println("리스트 사이즈   : " + list.size());
        System.out.println();
        System.out.println("리스트 내부 목록 : " + list);

        System.out.println();
        System.out.println("출력 1");
        for(int i = 0; i < list.size(); i++) {
            Employee emp = list.get(i);
            System.out.println(emp);
        }
        System.out.println();
        System.out.println("출력 2");
        for(int i = 0; i < list.size(); i++) {
            System.out.println(list.get(i));
        }
    }
}
~~~

##### ArrayList에 ProductDTO 객체 저장

- productDB5 복사해서 다음과 같이 변경 -> productDB6ArrayListVer 패키지(ProductSelect, ProductDTO, ProductDAO.... etc)
  - 모든 행을 ArrayList에 담아, DAO 클래스의 selectProduct() 메서드에서 한 행씩 출력 
  - ProductSelect 클래스의 productSelect() 메서드에게 반환
  - productSelect() 메서드에서 출력
  - 모든 클래스 복사해서 수정
  - DAO 클래스의 selectProduct() 메서드의 반환형을 ArrayList\<ProductDTO> 변경
  - DTO를 담을 ArrayList\<ProductDTO> 객체 생성 : dataSet
  - resultSet에서 하나씩 가져와서 DTO 생성하고 DTO를 ArrayList에 add()
  - return dataSet;
  - ProductSelect 클래스의 productSelect()
  - 반환된 dataSet 출력
  - StudentDTO 클래스에 toString() 추가 : StringBuilder 사용

##### ProductDTO.java

~~~java
public class ProductDTO {

    // ...

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        sb.append(prdNo);
        sb.append("\t");
        sb.append(prdName);
        sb.append("\t");
        sb.append(prdPrice);
        sb.append("\t");
        sb.append(prdMaker);
        sb.append("\t");
        sb.append(prdColor);
        sb.append("\t");
        sb.append(ctgNo);
        return sb.toString();
    }
}
~~~

##### ProductDAO.java

~~~java
public class ProductDAO {
    
    // ...

    // select Method
    public ArrayList<ProductDTO> selectProduct() {
        ArrayList<ProductDTO> dataSet = null;
        try {
            String sql = "select * from product order by prdNo";
            preparedStatement = connection.prepareStatement(sql);
            resultset = preparedStatement.executeQuery(sql);

            dataSet = new ArrayList<ProductDTO>();

            while (resultset.next()) {
                dataSet.add(new ProductDTO(resultset.getString(1),
                        resultset.getString(2),
                        resultset.getInt(3),
                        resultset.getString(4),
                        resultset.getString(5),
                        resultset.getString(6))); // DTO 1개가 1행에 해당
            }
        } catch (Exception e) {
            System.out.println("select 오류 발생!");
            e.printStackTrace();
        }
        return dataSet; // ArrayList<ProductDTO> 타입
    }
 // ...
~~~

##### ProductSelect.java

~~~java
public class ProductSelect {
    public void productSelect() {
        ProductDAO productDAO = new ProductDAO();
        ArrayList<ProductDTO> dataSet = new ArrayList<ProductDTO>();
        dataSet = productDAO.selectProduct();
        for (ProductDTO dto : dataSet) {
            System.out.println(dto);
        }
    }
}
~~~

##### Interface를 통한 구현

- 기존의 StudentDAO 클래스를 인터페이스 IStudentDAO를 구현한 클래스 변경

##### IStudentDAO.java(interface)

~~~java
public interface IStudentDAO {
    // 추상 메소드(바디 없음)
    // IStudentDAO 인터페이스를 구현하는 클래스에서 반드시 구현해야 함.
    public ArrayList<StudentDTO> selectStudent();
    public void insertStudent(StudentDTO studentDTO);
}
~~~

##### StudentDAO.java(인터페이스 구현 부분)

~~~java
public class StudentDAO implements IStudentDAO {
    Connection connection;
    PreparedStatement preparedStatement;
    ResultSet resultset;

    // DB연결 생성자
    public StudentDAO() {
        try {
            String url = "jdbc:mysql://localhost:3306/sqldb6?serverTimezone=UTC";
            String user = "root";
            String pwd = "";

            connection = DriverManager.getConnection(url, user, pwd);

            if (connection != null) {
                System.out.println("연결 성공");
            }
        } catch (Exception e) {
            System.out.println("연결 오류 발생!");
            e.printStackTrace();
        }
    }

    @Override
    public ArrayList<StudentDTO> selectStudent() {
        ArrayList<StudentDTO> dataSet = null;
        try {
            String sql = "select * from student order by stdNo";
            preparedStatement = connection.prepareStatement(sql);
            resultset = preparedStatement.executeQuery(sql);

            dataSet = new ArrayList<StudentDTO>();

            while (resultset.next()) {
                dataSet.add(new StudentDTO(resultset.getString(1),
                        resultset.getString(2),
                        resultset.getInt(3),
                        resultset.getString(4),
                        resultset.getDate(5).toString(),
                        resultset.getString(6))); // DTO 1개가 1행에 해당
            }
        } catch (Exception e) {
            System.out.println("select 오류 발생!");
            e.printStackTrace();
        }
        return dataSet; // ArrayList<StudentDTOArr> 타입
    }

    @Override
    public void insertStudent(StudentDTO studentDTO) {
        try {
            String sql = "insert into student values(?, ?, ?, ?, ?, ?)";
            PreparedStatement preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setString(1, studentDTO.getStdNo());
            preparedStatement.setString(2, studentDTO.getStdName());
            preparedStatement.setInt(3, studentDTO.getStdYear());
            preparedStatement.setString(4, studentDTO.getStdAddress());
            preparedStatement.setString(5, studentDTO.getStdBirthday());
            preparedStatement.setString(6, studentDTO.getDptNo());
            int result = preparedStatement.executeUpdate();
            if (result > 0) {
                System.out.println("성공");
            }
        } catch (Exception e) {
            System.out.println("insert 오류 발생!");
            e.printStackTrace();
        }
    }
}
~~~

# Algorithmday_3 정리 (2021.11.30 화요일)

## LinkedList
- List 구현 클래스이므로 ArrayList와 사용 방법은 동일
- 내부 구조 다름
- ArrayList : 배열로 만들어져 있어서 인덱스 사용
- LinkedList : 인접 참조를 링크해서 체인처럼 관리 (이전/다음 객체의 주소 갖고 있음)
- 특정 인덱스에서 객체를 제거하거나 추가하게 되면 바로 앞뒤 링크만 변경
- 빈번한 객체 삭제와 삽입이 일어나는 곳에서는 ArrayList보다 성능 좋음
- 순차적으로 추가/삭제 시
  - ArrayList가 LinkedList 보다 빠름
  - ArrayList가 용량이 충분하면 더 빠르지만 충분하지 않으면 새로운 크기의 ArrayList를 생성하고 데이터를 복사는 일이 발생해서 순차적으로 데이터를 추가해도 ArrayList가 더 느릴 수 있음
    - 충분한 용량 확보 중요
  - 마지막 데이터부터 역순으로 삭제해 나가면 각 요소들을 재배치할 필요가 없기 때문에 더 빠름
- 중간 데이터 추가/삭제 시
  - 링크만 변경해주면 되기 때문에 LinkedList가 훨씬 빠르다.
  - ArrayList는 삭제 후 각 요소들을 재배치하기 때문에 처리 속도가 늦다.


##### LinkedList 예제

~~~java
public class LinkedListEx1 {
    public static void main(String[] args) {
        ArrayList al = new ArrayList(2000000);
        LinkedList ll = new LinkedList();

        System.out.println("순차적으로 추가하기");
        System.out.println("ArrayList : " + add1(al));
        System.out.println("LinkedList : " + add1(ll));
        System.out.println();
        //순차적으로 추가하기
        //ArrayList : 90
        //LinkedList : 210

        System.out.println("중간에 추가하기");
        System.out.println("ArrayList : " + add2(al));
        System.out.println("LinkedList : " + add2(ll));
        System.out.println();
        //중간에 추가하기
        //ArrayList : 2009
        //LinkedList : 11

        System.out.println("중간에서 삭제하기");
        System.out.println("ArrayList : " + remove2(al));
        System.out.println("LinkedList : " + remove2(ll));
        System.out.println();
        //중간에서 삭제하기
        //ArrayList : 1310
        //LinkedList : 110

        System.out.println("순차적으로 삭제하기");
        System.out.println("ArrayList : " + remove1(al));
        System.out.println("LinkedList : " + remove1(ll));
        System.out.println();
        //순차적으로 삭제하기
        //ArrayList : 7
        //LinkedList : 29
    }
    // 순차적으로 추가
    public static long add1(List list) {
        long start = System.currentTimeMillis();
        for(int i=0; i<1000000; i++)
            list.add(i +"");
        long end = System.currentTimeMillis();
        return end - start;
    }
    // 중간에 추가
    public static long add2(List list) {
        long start = System.currentTimeMillis();
        for(int i=0; i<10000; i++)
            list.add(500, "X");
        long end = System.currentTimeMillis();
        return end - start;
    }
    // 순차적으로 삭제 : 역순으로 마지막 요소부터 삭제하면
    // 각 요소들을 이동하여 재배치할 필요 없음
    public static long remove1(List list) {
        long start = System.currentTimeMillis();
        for(int i=list.size()-1; i>=0; i--)
            list.remove(i);
        long end = System.currentTimeMillis();
        return end - start;
    }
    //중간 데이터 삭제하기
    // 처음 0 삭제, 이동. 1삭제, 이동, 2삭제, ...
    public static long remove2(List list) {
        long start = System.currentTimeMillis();
        for(int i=0; i<10000; i++)
            list.remove(i);
        long end = System.currentTimeMillis();
        return end - start;
    }
}
~~~

# Algorithmday_3 정리 (2021.11.30 화요일)

## Vector
- ArrayList와 동일한 내부 구조
- 스레드 동기화(Synchronization)되어 있기 때문에 여러 스레드가 동시에 접근하여 추가, 삭제 하더라도 스레드에 안전.

##### Vector 실습 예제

##### VectorEx.java

~~~java
public class VectorEx {
    public static void main(String[] args) {
        List<Board> list = new Vector<Board>();
        list.add(new Board("제목1","내용1","글쓴이1"));
        list.add(new Board("제목2","내용2","글쓴이2"));
        list.add(new Board("제목3","내용3","글쓴이3"));
        list.add(new Board("제목4","내용4","글쓴이4"));
        list.add(new Board("제목5","내용5","글쓴이5"));

        list.remove(2);
        list.remove(3);

        for(int i = 0; i < list.size(); i++) {
            Board board = list.get(i);
            System.out.println(board.subject + "\t" + board.content + "\t" + board.writer);
        }
        /*제목1	 내용1	글쓴이1
          제목2	 내용2	글쓴이2
          제목4	 내용4	글쓴이4*/
    }
}
~~~

# Algorithmday_3 정리 (2021.11.30 화요일)

## this
- 클래스 내에서 객체 자신을 가리키는 레퍼런스
- 컴파일러에 의해 자동 생성(사용자가 별도로 선언하지 않음)
- 용도
  - 1. 전달 받은 매개변수 값으로 멤버 변수의 값을 설정할 때
  - 2. 객체 자신의 레퍼런스 반환하는 경우

~~~java
public class Board {
	String subject; // 멤버변수
	String content;
	String writer;
	// 객체 생성 시 자동으로 생성자가 호출되면서
	// 전달되는 값들을 매개변수가 받음
	(String subject, String content, String writer) : 매개변수
전달되는 값을 받아서
메소드 내에서 지역 변수로 사용
메소드 내에서 this.를 사용하지 않으면 매개변수로 인식
(이름이 같은 멤버 변수로 인식하지 못함)
따라서 매개변수와 멤버 변수를 구분하기 위해 멤버 변수 앞에 this를 붙임
	public Board(String subject, String content, String writer) {
		this.subject = subject;
		this.content = content;
		this.writer = writer;

        // this.subject는 멤버변수 String subject
        // subject;는 매개변수 subject
	}
~~~

# Algorithmday_3 정리 (2021.11.30 화요일)

## Set
- Set컬렉션
- Set인터페이스
  - 수학의 집합에 비유
  - 저장 순서가 유지되지 않음
  - 객체 중복 저장 불가
  - 구현 클래스 : HashSet, LinkedHashSet, TreeSet
  - 전체 객체를 대상으로 한 번씩 반복해 가져오는 반복자(Iterator) 제공
  - 인덱스로 객체를 검색해서 가져오는 메소드 없음
  - get() 메소드 없음

#### Iterator
- java.util 패키지의 Iterator\<E> 인터페이스
- 컬렉션 프레임워크에서 컬렉션에 저장된 요소들을 읽어 오는 방법을 표준화한 것
- 요소가 순서대로 저장된 컬렉션에서 요소를 순차적으로 검색할 때 사용
- Vector\<Integer> v = new Vector\<Integer>();
- Iterator\<Integer> it = v.iterator();
- 벡터 v의 요소를 순차적으로 검색할 iterator 객체 반환 
- it.hasNext()
- it.next()


##### Set 예제

##### HashSetEx.java

~~~java
public class HashSetEx {
    public static void main(String[] args) {
        Set<String> set = new HashSet<String>();
        // 중복 값은 한 번만 저장
        set.add("Java");
        set.add("JDBC");
        set.add("Servlet/JSP");
        set.add("Java");
        set.add("MyBatis");

        System.out.println("총 객체 수 : " + set.size()); // 총 객체 수 : 4
        System.out.println();
        Iterator<String> iterator = set.iterator(); // 전체 객체를 대상으로 한 번씩 반복해 가져오는 반복자
        while (iterator.hasNext()) { // 들어있는 객체 수 만큼 반복
            System.out.println(iterator.next());
        }
//        Java
//        JDBC
//        MyBatis
//        Servlet/JSP

        System.out.println();
        set.remove("JDBC");
        set.remove("MyBatis");
        for(String element : set) {
            System.out.println(element);
        }
//        Java
//        Servlet/JSP

        System.out.println();
        set.clear();
        if(set.isEmpty()) {
            System.out.println("비어 있음");
        }
        // 비어 있음
    }
}
~~~

##### HashSetLotto.java

~~~java
public class HashSetLotto {
    public static void main(String[] args) {
        // 중복 값 저장 하지 않는 특성 이용하여 로또 번호 생성
        Set<Integer> set = new HashSet<Integer>();
        int count = 0;
        for(; set.size() < 6;) {
            count++;
            int num = (int)(Math.random()*45) + 1;
            set.add(num);
            System.out.println(count);
        }
        System.out.println("Set");
        System.out.println(set);

        // LinkedList 생성되며 동시에 값 할당
         LinkedList<Integer> list = new LinkedList<Integer>(set);
        System.out.println("List");
        System.out.println(list);

        System.out.println("Reverse");
        Collections.reverse(list); // 반대 인덱스부터 출력
        System.out.println(list);

        System.out.println("Sorted List"); // 오룸차순 정렬
        Collections.sort(list);
        System.out.println(list);

        System.out.println("Sorted List Reverse");
        Collections.reverse(list); // 정렬 후 사용하면 내림차순 정렬 가능
        System.out.println(list);
    }
}
~~~

# Algorithmday_3 정리 (2021.11.30 화요일)

## Map
- Map 인터페이스
- 키(Key)와 값(Value)의 쌍으로 이루어진 데이터의 집합
- 키와 값은 모두 객체
- 키는 중복될 수 없지만 값은 중복 가능
- 기존에 저장된 데이터와 중복된 키 값을 저장하면 기존의 값은 없어지고 마지막에 저장된 값이 남음(값을 덮어쓴다)
- 구현 클래스 : HashMap, HashTable, LinkedHashMap, Properties, TreeMap
- 일반적으로 Key의 타입은 String 많이 사용한다.
- HashMap을 생성 하려면 Key와 Value 모두 매개변수 작성을 해야 한다.
- Map\<K, V> map = new HashMap\<K, V>();

##### HashMap 예제

##### HashMapEx1.java

~~~java
public class HashMapEx1 {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<String, Integer>();
        // 갹체 저장
        map.put("홍길동", 85);
        map.put("이몽룡", 90);
        map.put("홍길동", 80);
        map.put("성춘향", 95);
        System.out.println("총 Entry 수 : " + map.size()); // 총 Entry 수 : 3
        System.out.println(map); // {성춘향=95, 홍길동=80, 이몽룡=90}
        System.out.println(map.get("홍길동")); // 80 (Key 홍길동의 Value 출력
        System.out.println(map.keySet()); // [성춘향, 홍길동, 이몽룡] Key 값만 출력됨
        for(String key : map.keySet()) {
            System.out.println(key + " : " + map.get(key));
        }
//        성춘향 : 95
//        홍길동 : 80
//        이몽룡 : 90
        map.remove("홍길동", 85); // 홍길동은 80인데 85를 넣으면 지워지지 않음
        System.out.println("총 Entry 수 : " + map.size()); // 총 Entry 수 : 3
        
        map.remove("홍길동");
        System.out.println("총 Entry 수 : " + map.size()); // 총 Entry 수 : 2

        map.clear();
        System.out.println("총 Entry 수 : " + map.size()); // 총 Entry 수 : 0
    }
}
~~~

##### HashMapEx2.java

~~~java
public class HashMapEx2 {
    public static void main(String[] args) {
        HashMap<String, String> map = new HashMap<String, String>();
        Scanner scan = new Scanner(System.in);
        map.put("apple", "사과");
        map.put("summer", "여름");
        map.put("school", "학교");
        map.put("bus", "버스");
        map.put("water", "물");
        while (true) {
            System.out.print("찾고 싶은 단어는? ");
            String str = scan.next();
            if(str.equals("exit")) {
                System.out.println("종료합니다");
                System.exit(0);
            }
            else {
                if(map.keySet().contains(str)) {
                    System.out.println(map.get(str));
                }
                else {
                    System.out.println("없는 단어 입니다.");
                }
            }
        }
    }
}
~~~

##### HashMapEx3.java

~~~java
public class HashMapEx3 {
    public static void main(String[] args) {
        HashMap<String, String[]> pNum = new HashMap<String, String[]>();
        pNum.put("친구1",
                new String[] {"010-1111-1111", "02-1111-1111", "friend1@google.com"});
        pNum.put("친구2",
                new String[] {"010-2222-2222", "02-2222-2222", "friend2@google.com"});
        pNum.put("친구3",
                new String[] {"010-3333-3333", "02-3333-3333", "friend2@google.com"});
        pNum.put("동기",
                new String[] {"010-4444-4444", "02-4444-4444", "sametime@google.com"});
        pNum.put("부장님",
                new String[] {"010-5555-5555", "02-5555-5555", "boss@google.com"});
        System.out.println("총 그룹 수 : " + pNum.size());

        // 모든 정보 조회
        for(String key : pNum.keySet()) {
            System.out.print(key + " : ");
//            String[] pList = pNum.get(key);
//            for(String one : pList) {
            for(String one : pNum.get(key)) {
                System.out.print(one + " | ");
            }
            System.out.println();
        }
        System.out.println();
        System.out.print("\n동기 검색 : ");
        if(pNum.containsKey("동기")) {
            for(String one : pNum.get("동기")) {
                System.out.print(one + " | ");
            }
        }
        System.out.println();
        System.out.print("\n사장님 검색 : ");
        if(pNum.containsKey("사장님")) {
            for(String one : pNum.get("사장님")) {
                System.out.print(one + " | ");
            }
        } else {
            System.out.println("연락처 없음");
        }
    }
}
~~~

# Algorithmday_3 정리 (2021.11.30 화요일)

## Collection 클래스
- java.util. 패키지에 포함된 클래스
- 컬렉션을 다루는 유용한 메소드 지원
- sort() : 정렬
- reverse() : 반대로 정렬
- max() / min() : 최대값 / 최소값 
- binarySearch() : 검색

##### Collection 예제

##### CollectionEx1.java

~~~java
public class CollectionEx1 {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<String>();

        list.add("트랜스포머");
        list.add("스타워즈");
        list.add("매트릭스");
        list.add("터미네이터");
        list.add("아바타");

        System.out.print("리스트 순서 : ");
        for(String movie : list) {
            System.out.print(movie + " | ");
        }
        System.out.println();
        System.out.print("오름차순 정렬 : ");
        Collections.sort(list);
        printList(list);

        System.out.println();
        int index = Collections.binarySearch(list, "스타워즈");
        System.out.println("스타워즈는 " + index + " 번 인덱스 입니다.");

        System.out.println();
        System.out.print("내림차순 정렬 : ");
        Collections.reverse(list);
        printList(list);
    }
    static void printList(ArrayList<String> list) {
        Iterator<String> it = list.iterator();
        while (it.hasNext()) {
            String element = it.next();
            String sep;
            if(it.hasNext()) {
                sep = " -> ";
            }
            else {
                sep = "\n";
            }
            System.out.print(element + sep);
        }
    }
}
~~~

# Algorithmday_3 정리 (2021.11.30 화요일)

## Tree
- 트리
- 자료들의 항목이 가지들로 연결될 수 있게 자료가 구성되어 있는 구조
  - node(자료(항목))와 edge(간선(가지))로 구성.
- 계층적인 구조
- 부모-자식 관계의 노드들로 구성

## 사진

### 트리의 용어
- 노드(node) : 트리를 구성하는 각 자료 항목
 - 근 노드(root node)
   - 트리 구조를 시작하는 노드
   - 최상위에 존재하는 하나의 노드
 - 자식 노드
   - 임의의 노드에 연결된 다음 레벨의 노드들의 집합
   - D의 자식 노드는 H, I, J
 - 부모 노드
   - 임의의 노드에 연결된 상위 계층의 노드
   - B는 E, F의 부모
 - 차수(degree)
   - 한 노드에 연결된 가지의 수 (노드가 갖고 있는 자식 노드의 개수)
   - D의 차수는 3
 - 레벨(level)
   - root node부터 0으로 시작해서 아래 가지로 갈수록 레벨이 1씩 증가함
   - F는 레벨 2
 - 트리의 깊이(depth)
   - 어떤 특정 노드에서 root node에 이르는 경로의 길이
   - F의 깊이 : 2
   - L의 깊이 : 3
   - 레벨 값 = 깊이 값
 - 트리의 높이(height)
   - 트리의 최대 레벨 + 1
   - 사진의 트리는 높이가 4인 트리다.

### 트리 구조의 저장
- 배열을 이용한 방법
  - 연속적인 기억 공간을 그대로 이용하는 배열의 구조에 트리를 저장
  - 각 노드 당 최대 차수 3만큼 기억 장소 확보
  - 최대 기억 장소 : 총 노드의 개수(9) x 트리의 차수(3) + 1 = 28

## 사진

- 연결 리스트를 이용한 방법

### 이진 트리
- 왼쪽 서브 트리와 오른쪽 서브 트리라고 부르는 2개의 분리된 트리로 구성된 노드들의 유한 집합
- 이진 트리는 모든 노드들의 차수는 2를 초과할 수 없음
- root 노드만 있어도 이진 트리로 인정
- 왼쪽과 오른쪽의 반향성 존재
- 트리 (a)와 트리 (b)는 다른 트리

## 사진

- 서브 트리가 왼쪽이거나 오른쪽이 아닌 아래로 향한 트리는 이진 트리가 아님

## 사진

### 트리의 운행(Tree Traverse)
- 트리 구조의 각 노드를 전부 한번씩 방문하여 검색해내는 방법
- 레벨 순서 운행 방법
  - 상향식 레벨 순서 운행법
  - 하향식 레벨 순서 운행법
- 노드 위치에 따른 운행벅
  - 전위 / 중위 / 후위 운행법
- 이진 트리의 운행법
  - 일반적인 트리의 운행보다 간단
  - 나타낼 수 있는 조합의 수는 여섯 가지이지만, 왼쪽 서브트리가 오른쪽 서브트리보다 선행한다는 제약을 주면 3가지 운행법만 존재
  - 전위 : __root__ - left - right
  - 중위 : left - __root__ - right
  - 후위 : left - right - __root__

#### 전위 운행

## 사진

- 경로 : A - B - D - H - E - I - J - C - F - G - K

#### 중위 운행

## 사진

- 경로 : H - D - B - I - E - J - A - F - C - G - K

#### 후위 운행

## 사진

- 경로 : H - D - I - J - E - B - F - K - G - C - A