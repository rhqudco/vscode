# day_10 정리 (2021.11.12 금요일)

## 자료 타입
- 자바에서 추가적으로 제공되는 자료 타입
  - 자료구조의 한 종류
  - 쉽게 쓰기 위해 미리 클래스가 정의
  
### 리스트
- List 인터페이스를 구현한 클래스들
  - ArrayList, LinkedList
  - 선형자료구조의 한 종류

~~~java
package DataType;

import java.util.ArrayList;

public class Ex01 {
    public static void main(String[] args) {
        //객체 생성(크기가 없는)
        ArrayList arr = new ArrayList();
        // 원소를 추가 하는 방법(add)
        arr.add("10");
        arr.add("20");
        arr.add("30");
        // 원소 확인 (get(인덱스 번호))
        System.out.println(arr.get(0));

        // 배열의 크기를 확인하고 싶은 경우(size)
        System.out.println(arr.size());

        // 원하는 위치에 원소 삽입(add(인덱스 번호, 값))
        arr.add(1, "15");

        // 배열 내의 모든 원소를 확인하고 싶은 경우에는 순회
        for(int i = 0; i < arr.size(); i++) {
            System.out.println(arr.get(i));
        }

        // 배열의 원소를 검색하는 경우 contains(찾는 값) 결과는 true or false로 반환
        System.out.println(arr.contains("15"));

        // 배열에서 원소를 삭제하는 경우(remove)
        // 매개변수가 객체인 경우(기본타입이 아닌 경우)
        arr.remove("10");
        for(int i = 0; i < arr.size(); i++) {
            System.out.println(arr.get(i));
        }

        // 매개변수가 숫자(인덱스)인 경우
        arr.remove(1);
        for(int i = 0; i < arr.size(); i++) {
            System.out.println(arr.get(i));
        }
    }
}
~~~

### Generics
- 명시된 타입 이외에 다른 타입의 원소를 넣을 수 없다.
- 자동으로 타입이 확인되는 이점이 있다.

~~~java
package DataType;

import java.util.ArrayList;

public class Ex02 {
    public static void main(String[] args) {
        ArrayList arr = new ArrayList();

        // 원소의 타입이 String인 것을 알고 있다.
        arr.add("Java");
        arr.add("Python");
        arr.add("C++");

        // 배열 내의 원소 꺼내온다.
        // ArrayList는 원소의 타입을 Object로 인식
        // String str = arr.get(0); 는 오류!
        // 항상 타입변환을 염두해 두어야 한다.
        String str = (String) arr.get(0);
        System.out.println(str);

        // ArrayList<타입> 이름 = new ArrayList();
        // 만들 때 타입을 명시하면 타입체크가 필요 없음.
        ArrayList<String> sarr = new ArrayList<String>();

        sarr.add("Java");
        sarr.add("Python");
        sarr.add("C++");
        String sstr = sarr.get(0);
        System.out.println(sstr);
    }
}
~~~

### Map
- (key, value)형태 자료형
- 배열은 사용할 때 인덱스가 정해져있지만 Map은 key를 이용하여 접근할 수 있다.
- Map 인터페이스를 구현해서 정의된 여러가지 클래스들
  - HashMap
  - LinkedHashMaep
  - TreeMap
  - etc...

~~~java
package DataType;

import java.util.HashMap;
import java.util.Map;

public class Ex03 {
    public static void main(String[] args) {
        // key도 value도 문자열 형태<key, value>
        HashMap<String, String> map = new HashMap<String, String>();

        // 원소를 추가하는 경우(put)
        map.put("first", "wkdehdrjs");
        map.put("second", "dnjsqls");

        // 원소 확인 (get)
        System.out.println(map.get("first"));

        // 전체 원소를 확인하는 방법
        // entrySet()
        // [key=value]로 출력
        System.out.println(map.entrySet());

        // for each
        for(Map.Entry<String, String> item: map.entrySet()) {
            System.out.println("key : " + item.getKey() + ", value : " + item.getValue());
        }
        // 키만 확인
        System.out.println(map.keySet());

        for(String key : map.keySet()) {
            System.out.println(map.get(key));
        }

        // 원소를 삭제하는 경우(remove)
        // 키에 해당하는 원소 삭제하고 값을 리턴한다.
        System.out.println(map.remove("first"));

        // 크기확인 (size)
        System.out.println(map.size());
    }
}
~~~