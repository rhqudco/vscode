# day_4 정리 (2021.11.04 목요일)
## 제어문
### 반복문
#### while
~~~java
while (조건문) {
    <수행할 문장1>
    <수행할 문장2>
    <수행할 문장3>
    ...
} // 수행할 문장 중 조건문의 조건을 달성시킬 수 있게 변수를 바꿔줘야 한다.
  // 그렇지 않으면 무한반복하게 된다.
~~~
#### for
~~~java
for(초기치; 조건문; 증가치)  {
    <수행할 문장1>
    <수행할 문장2>
    <수행할 문장3>
    ...
}
~~~
#### for each
- Iterate 객체에 특화되어 있는 반복문.
- 첫 번째 원소부터 마지막 원소까지 차례대로 접근 가능한 형태.
- Iterate객체 원소의 개수만큼 반복
- Iteration
  - "반복"이라는 의미
  - Iterate : 반복 가능한 모든 객체들.
  - 배열, String, ArrayList 등
~~~java
// for each문의 구조.
for (type var: iterate) {
    body-of-loop
}
// for each문의 예시
ArrayList<String> numbers = new ArrayList<String>();
numbers.add("one");
numbers.add("two");
numbers.add("three");

for(String number: numbers) {
    System.out.println(number);
}
~~~