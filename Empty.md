## JSON 형식
- key-value 쌍으로 이루어진 자료구조
- key : value와 같은 형식으로 구분한다.
- key값만 알고 있으면 value를 추출할 수 있다는 장점이 있다.
  - 예
    - "MyName" : "Mr. Go"
    - key는 MyName, value는 Mr. Go(String)가 된다.
    - value값으로 int, Array 등 다양한 자료형이 올 수 있다.
    - "age" : 25
    - "drink" : ["soju", 16.5, "cold"]
- '{ }'를 이용하여 여러 정보를 하나로 묶을 수 있다.
  - car1이 key가 되고, '{  }'안에 key-value들이 묶여진 구조를 객체(Object)라고 한다.
  - 객체도 value가 될 수 있다.
~~~
"car1" : {
    "Name" : "Sonata",
    "Maker" : "Hyundai",
    "Price" : 30000000
},
"car2" : {
    "Name" : "Granduer",
    "Maker" : "Hyundai",
    "Price" : 40000000
},
"car3" : {
    "Name" : "K7",
    "Maker" : "KIA",
    "Price" : 40000000
}
~~~

- 위와 같은 구조를 배열로 만들 수 있다.
  - '[  ]'를 이용하면 된다.
  - car 라는 key 배열 안에 Object가 배열로 들어간 형태로 value를 가진다.
  - Name이라는 key를 조사하면 "Sonata", Grandeur", "K7"의 정보를 얻을 수 있다.

~~~
"car" : [ {
    "Name" : "Sonata",
    "Maker" : "Hyundai",
    "Price" : 30000000
}, {
    "Name" : "Granduer",
    "Maker" : "Hyundai",
    "Price" : 40000000
}, {
"   Name" : "K7",
    "Maker" : "KIA",
    "Price" : 40000000
}]
~~~

## JSONObject, JSONArray

### JSONArray
- 이름 그대로 배열 구조이다.
- 배열 안에는 문자열, 숫자, 배열, 객체 등을 담을 수 있다.
- 대괄호('[ ]')를 통해 값을 담고, comma(',')를 통해 값을 구분한다.
- index를 통해 값을 꺼낼 수 있기 때문에 순서에 대한 고려가 있어야 편하게 사용할 수 있다.

### JSONObject
- 하나 이상 key-value 쌍을 중괄호('{ }')를 통해 담고 있는 객체 구조.
- key와 value 사이 구분은 colon(':')으로 함.
- key-value(키-값) 구분은 comma(',')로 함.
- 순서가 구분되지 않은 집합체.