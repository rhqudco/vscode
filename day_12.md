# day_12 정리 (2021.11.16 화요일)

## 다차원 배열

~~~java
int[][] arr2D = new int[5][5];
// 2차원 배열의 선언

int[][] arrInit = {{10,20,30},{40,50,60}};
// 초기화된 2차원 배열의 선언
// 배열의 원소로 배열을 갖는다
// 문자열 배열도 2차원 배열과 동일한 형태

// 2차원 배열에서 원소에 대한 참조
// arrInit[0] = {10,20,30} 이다
// arrInit[0][1] = 20 이다
// [행][열]

// 2차원 배열의 순회
for(int i = 0; i < arrInit.length; i++) {
    System.out.println(Arrays.toString(arrInit[i]))
}
//[10, 20, 30]
//[40, 50, 60] 출력됨

for(int i = 0; i < arrInit.length; i++) {
    for(int j = 0; j < arrInit[i].length; j++) {
        System.out.Println(arrInit[i][j]);
    }
}
//10
//20
//30
//...
//60 출력됨
~~~