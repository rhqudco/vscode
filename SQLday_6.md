# SQLday_6 정리 (2021.11.25 목요일)

## Statement vs PreparedStatement
- 쿼리문 전송을 위한 객체를 생성
- Statement
  - 문자열로 구성된 SQL문을 DBMS로 전송하면 내부적으로 SQL문을 JDBC 드라이버가 읽을 수 있는 형식으로 전처리 수행
  - SQL문이 수행될 때 마다 매번 전처리 수행
    - 반복적 작업으로 인해 성능 저하 발생할 수 있음
  - 쿼리문에 값이 다 입력되어 있어야하기 때문에 SQL문이 복잡해짐
- PreparedStatement
  - Statement 인터페이스의 하위 인터페이스
  - SQL이 실행될 때 마다 매번 전처리하지 않고 라이브러리 캐시에서 읽어와서 처리하기 때문에 성능이 좋다.
  - SQL문 구조는 같지만 조건이 수시로 변할 때 조건의 변수 처리를 '?'(PlaceHolder)로 지정할 수 있다
    - 바인딩 변수라고 함
  - 동일한 SQL문을 특정 값만 바꾸어서 여러 번 실행해야 할 때 또는, 인수가 많아서 SQL문이 복잡할 때 관리
  - 실무에서는 주로 PreparedStatement 사용
  - 바인딩 변수의 순서는 ?의 순서에 따라 결정됨.
  - 시작번호는 1부터 시작.
  - 바인딩 변수에 값을 저장하기 위해 set'자료형'() 메소드 사용
  - 바인딩 변수는 반드시 열의 값 자리에 위치한다.   
    - values(?,?,?,?,?,?,?

## DTO
- Data Transfer Object
  - 데이터 저장용 클래스(멤버 변수에 데이터 저장)
  - 데이터베이스에 데이터를 저장하거나 데이터베이스로부터 데이터를 조회할 때 데이터를 담아서 전달하기 위해 사용
  - 데이터 입력 -> DTO -> DAO(insert()로 전달) -> DB
  - 데이터 조회 -> DB -> DAO(select()로 데이터 읽어옴) -> 출력(또는 DTO에 담아서 출력 담당에게 전달)

##### DTO 예제 코드

~~~java
package db4;

public class ProductDTO {
    private String prdNo;
    private String prdName;
    private int prdPrice;
    private String prdMaker;
    private String prdColor;
    private String ctgNo;

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

## DAO
- Data Access Object
  - 데이터를 액세스 하는 클래스
  - 데이터베이스에 데이터를 저장하거나 데이터베이스에서 데이터를 가져올 때 사용
  - insert() / select() / update() / delete() 기능의 메소드 포함
  - DB 연결 (생성자)

##### DAO 예제 코드

~~~java
package db4;

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