# Algorithmday_4 정리 (2021.12.01 수요일)

## 정렬(Sort)
- 일련의 자료들을 자료 중에 포함된 몇 가지 항목을 우선대로 지정하여 그 순서에 따라 모든 자료를 나열하는 방법

#### 정렬 알고리즘 종류
- 버블 정렬(Bubble Sort)
- 선택 정렬(Selection Sort)
- 삽입 정렬(Insertion Sort)
- 쉘 정렬(Shell Sort)
- 퀵 정렬(Quick Sort)
- 이원 합병 정렬(2-Way merge Sort)
- 기수 정렬(Radix Sort)
- 힙 정렬(Heap Sort)

#### 정렬 알고리즘
- 단순하지만 비효율적인 방법 : 삽입 정렬, 선택 정렬, 버블 정렬
- 복잡하지만 효율적인 방법 : 퀵 정렬, 힙 정렬, 합병 정렬, 기수 정렬
- 정렬 알고리즘의 평가
  - 비교 횟수
  - 이동 횟수
- 모든 경우 최적인 알고리즘은 없으니 상황에 따라 선택하여 사용한다.

# Algorithmday_4 정리 (2021.12.01 수요일)
  
## 버블 정렬(Bubble Sort)
- 인접한 항목이 순서대로 되어 있지 않으면 서로 교환한다.
  - a = [7,6,5,2,1,4,8,9,3] 원본
  - a = [6,7,5,2,1,4,8,9,3] 7, 6 교환
  - a = [6,5,7,2,1,4,8,9,3] 7, 5 교환
  - a = [6,5,2,7,1,4,8,9,3] 7, 2 교환
  - a = [6,5,2,1,7,4,8,9,3] 7, 1 교환
  - a = [6,5,2,1,4,7,8,9,3] 7, 4 교환
  - a = [6,5,2,1,4,7,8,3,9] 7, 8 / 7, 9는 맞기 때문에 건너 뛰고(하지만 비교는 하기 때문에 성능에 영향을 끼친다.) 9, 3 교환
  - 까지 1라운드 종료 -> 다시 a[0], a[1]비교부터 시작
  - a = [5,6,2,1,4,7,8,3,9] 6, 5 교환
  - .....
  - a = [1,2,3,4,5,6,7,8,9] 가 될 때 까지 반복 위와 같은 과정 반복
  - 항목이 n개인 배열에 정렬을 하면 비교 횟수는 n(n-1)/2번의 비교를 한다.

## 사진

##### 버블 정렬 예제 코드

- BubbleSort.java

~~~java
public class BubbleSort {
    public static void main(String[] args) {
        int [] arr = {5,2,8,3,1};
        bubbleSort(arr);
        System.out.println(Arrays.toString(arr));
    }
    static void bubbleSort(int[] arr) {
        // 이전 값을 뒤에 넣기 위해 임시 저장소 필요
        int temp = 0;
        // 총 라운드 : 배열 크기 - 1번
        for(int i = 0; i < arr.length; i++) {
            // 각 라운드별 비교 횟수 : 배열크기 - 라운드 횟수
            for(int j = 0; j < arr.length-1-i; j++) {
                if(arr[j] > arr[j+1]) {
                    temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
        }
    }
}
~~~

# Algorithmday_4 정리 (2021.12.01 수요일)

## 선택 정렬(Selection Sort)
- 잘못된 위치에 들어가 있는 원소를 찾아서 그것을 올바른 위치에 넣는 원소 교환 방식으로 정렬
- 가장 작은 원소를 찾아 첫 번째 위치의 원소와 교환
- 두 번째로 작은 원소를 찾아 두 번째 위치의 원소와 교환
- 첫 번째 원소를 키로 지정하고 뒤 원소와 비교해서 작은 값을 앞으로 보내는 방식
- 두 번째 원소를 키로 지정하고 뒤 원소와 비교해서 작은 값을 앞으로 보내는 방식
- 정렬될 때 까지 과정 반복
- 초기 : 5, 2, 8, 3, 1
- 1라운드
  - 키는 첫 번째 원소
  - 2, 5, 8, 3, 1 (5와 2교환)
  - 1, 5, 8, 3, 2 (2와8, 3을 비교 했지만 2가 작기 때문에 교환하지 않고, 2와 1교환)
- 2라운드
  - 1, 5, 8, 3, 2
  - 키는 두 번째 원소
  - 1, 3, 8, 5, 2 (5와 8을 비교 했지만 5가 더 작아서 그대로 두고 5와 3을 비교해서 두 원소 위치 교환)
  - 1, 2, 8, 5, 3 (네 번째 위치 원소까지 비교 했으니 다섯 번째 위치 원소와 비교 3과 2의 위치 교환)
- 3라운드
  - 1, 2, 8, 5, 3
  - 키는 세 번째 원소
  - 1, 2, 5, 8, 3 (8과 5 비교해서 위치 교환)
  - 1, 2, 3, 8, 5 (네 번째 위치 원소까지 비교 했으니 다섯 번째 위치 원소와 비교 5와 3 위치 교환)
- 4라운드
  - 1, 2, 3, 8, 5
  - 키는 네 번째 원소
  - 1, 2, 3, 5, 8 (8과 5 비교, 두 원소 위치 교환)
  - 완성

##### 선택 정렬 예제 코드

- SelectionSort.java

~~~java
public class SelectionSort {
    public static void main(String[] args) {
        int [] arr = {5,2,8,3,1};
        selectionSort(arr);
        System.out.println(Arrays.toString(arr));
    }
    static void selectionSort(int[] arr) {
        int temp;
        // 총 라운드 : 배열 크기 - 1 번 진행
        for(int i = 0; i < arr.length-1; i++) {
            // i 다음부터 끝까지 비교
           for(int j = i+1; j < arr.length; j++) {
                if(arr[i] > arr[j])  {
                    temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
        }
    }
}
~~~

# Algorithmday_4 정리 (2021.12.01 수요일)

## 삽입 정렬(Insertion Sort)
- 정렬되어 있지 않은 부분의 왼쪽 끝에서 삽입할 원소를 찾아서 정렬되어 있는 부분의 적절한 위치에 삽입
- 정렬 안 된 부분의 숫자 하나가 정렬된 부분에 삽입됨으로써, 정렬된 부분의 원소 수가 1개 늘어나고, 동시에 정렬이 안 된 부분의 원소 수는 1개 줄어든다.
- 이를 반복하면 결국 정렬 안 된 부분에는 아무 원소도 남지 않고 정렬된 부분에 모든 원소가 존재
- 정렬 방법
  - 정렬되어 있지 않은 부분의 왼쪽에서 삽입할 원소 k 선택
  - 빈자리 확보를 위해 k를 꺼내서 임시 장소에 보관
  - 정렬되어 있는 부분에서 k보다 큰 원소들을 오른쪽으로 이동하여 k가 들어갈 빈자리 확보
  - 확보된 빈자리에 k삽입
  - 모든 원소들이 정렬될 때 까지 반복
- 안정된 정렬 방법
- 많은 이동 횟수(레코드가 클 경우 불리하다)
- 이미 정렬이 어느정도 되어 있으면 효율적
- 시간 복잡도
  - 최상의 경우(이미 정렬되어 있는 경우)
    - 비교 : n-1번
    - 이동 : 2(n-1)번
  - 최악의 경우(역순으로 정렬되어 있는 경우 모든 단계에서 앞에 놓은 자료 전부 이동)
    - 비교 : n(n-1) / 2
    - 이동 : n(n-1) / 2 + 2(n-1)

## 사진

##### 삽입 정렬 예제 코드

- InsertionSort.java

~~~java
public class InsertionSort {
    public static void main(String[] args) {
        int [] arr = {5,2,8,3,1};
        insertSort(arr);
        System.out.println(Arrays.toString(arr));
    }
    static void insertSort(int[] arr) {
        for(int i = 1; i<arr.length; i++) {
            // 선택한 값
            int temp = arr[i];
            // 선택한 값의 이전 원소의 인덱스 번호 저장
            int index = i - 1;
            // 현재 값이 이전 원소보다 작으면 큰 값은 뒤로 이동
            while (index >= 0 && temp < arr[index]) {
                // 이전 원소를 한 칸씩 뒤로 이동
                arr[index+1] = arr[index];
                index--;
            }
            arr[index+1] = temp;
        }
    }
}
~~~

# Algorithmday_4 정리 (2021.12.01 수요일)

## 쉘 정렬(Shell Sort)
- 원소의 비교 연산과 먼 거리의 이동을 줄이기 위해 몇 개의 서브 리스트로 나누어 삽입 정렬 반복 수행
- 삽입 정렬의 개념을 확대하여 일반화 시킨 정렬 방법
- 삽입 정렬의 최대 문제점은 요소들이 이동할 때 이웃한 위치로만 이동한 것
- 쉘 정렬에서는 요소들이 멀리 떨어진 위치로도 이동할 수 있기 때문에 쉘 정렬이 삽입 정렬보다 속도가 빠름.
- 정렬 방법
  - 정렬에서 사용할 간격 결정
    - 전체 원소 수 n의 1/3, 다시 이것의 1/3....
    - 간격이 작아질수록 짧은 거리를 이동하고 원소 이동이 적음
  - 첫 번째 간격에 따라 서브 리스트로 분할
    - 각 서브 리스트에 대하여 삽입 정렬 수행
  - 두 번째 간격에 따라 서브 리스트로 분할
    - 각 서브 리스트에 대하여 삽입 정렬 수행
  - 마지막 간격에 따라 서브 리스트로 분할(마지막 간격은 무조건 1이다)
    - 각 서브 리스트에 대하여 삽입 정렬 수행
    - 각 모든 원소를 1개의 그룹으로 여기는 것이고 이는 삽입 정렬 그 자체이다.

## 사진

##### 쉘 정렬 예제 코드

- ShellSort.java

~~~java
public class ShellSort {
    public static void main(String[] args) {
        int [] arr = {30,60,90,10,40,80,40,20,10,60,50,30,40,90,80};
        shellSort(arr);
        System.out.println("최종");
        System.out.println(Arrays.toString(arr));
    }
    static void shellSort(int[] arr) {
        int n = arr.length;
        for(int i = n/2; i > 0; i/=2) {
            System.out.println("간격 i = " + i);
            for(int j = i; j < n; j++) { // 삽입 정렬을 위해 서브 리스트의 두 번째 값을 가지고 비교
                int index = j - i;
                int temp = arr[j];
                // 삽입 정렬 수행
                while (index >= 0 && arr[index] > temp) {
                    arr[index+i] = arr[index];
                    index -= i;
                }
                arr[index + i] = temp;
            }
            // 각 간격마다 정렬 결과
            System.out.println(Arrays.toString(arr));
            System.out.println();
        }
    }
}
~~~

# Algorithmday_4 정리 (2021.12.01 수요일)

## 퀵 정렬(Quick Sort)
- 분할 정복 정렬 방법 중 하나
- 전체 리스트를 2개의 부분 리스트로 분할하고
- 각각의 서브 리스트를 다시 퀵 정렬로 정렬
  - 기준 값보다 큰 값들은 오른쪽으로, 작은 값들은 왼쪽으로 재 배열
- 정렬 방법
  - 전체 리스트에서 한 원소를 기준 값(pivot)으로 선정
  - 피벗을 기준으로 두 개의 서브 리스트로 분할
    - 왼쪽 : 피벗보다 작은 값의 원소들로 구성
    - 오른쪽 : 피벗보다 크거나 같은 값의 원소들로 구성
  - 각각의 파티션(서브 리스트)에 대해 다시 퀵 정렬을 순환 적용
    - 피벗 선정 및 파티션 분할
- 퀵 정렬 수행 순서
- 피벗(pivot) : 가장 왼쪽 숫자를 피벗으로 선정
- 두 개의 변수 : low와 high(이동)
  - low는 왼쪽에 위치
  - high는 오른쪽에 위치 
- low : 오른쪽으로 이동하면서 피벗 보다 큰 숫자를 찾음
  - 피벗 보다 작으면 통과, 큰 숫자를 찾으면 정지
- high : 왼쪽으로 이동하면서 피벗 보다 작은 숫자를 찾음
  - 피벗 보다 크면 통과, 작은 숫자를 찾으면 정지
- 정지된 위치의 숫자들 서로 교환
- low와 high가 교차하면 종료. high와 pivot 교환

## 사진


##### 퀵 정렬 예제 코드

- QuickSort.java

~~~java
public class QuickSort {
    public static void main(String[] args) {
        int [] arr = {8,5,4,6,3,1,2,7,9};
        quickSort(arr,0,arr.length-1);
        System.out.println(Arrays.toString(arr));
    }
    static void quickSort(int[] arr, int low, int high) {
        if(low >= high) {
            return;
        }
        int pivot = low;
        int i = low + 1;
        int j = high;
        int temp;
        while(i <= j) { // 교차할 때 까지 반복 j가 i보다 크면 while문 종료
            while(i <= high && arr[i] < arr[pivot]) { // 피벗보다 큰 값을 만날 때 까지 반복
                i++;
            }
            while (j > low && arr[j] >= arr[pivot]) { // 피벗보다 작은 값을 만날 때 까지 반복
                j--;
            }
            if(i > j) { // 교차한 상태가 되면 피복과 j 교환
                temp = arr[j];
                arr[j] = arr[pivot];
                arr[pivot] = temp;
            }
            else { // i와 j값 교환
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
        quickSort(arr, low, j-1);
        quickSort(arr, j+1, high);
    }
}
~~~

# Algorithmday_4 정리 (2021.12.01 수요일)

## 이원 합병 정렬(Two-way Merge Sort)
- 정렬된 2개의 리스트를 혼합하여 완전히 정렬된 하나의 리스트로 합하는 정렬 방식
- 1. 6, 9, 2, 12, 8, 34, 23, 33, 56, 17, 56, 32
  2. (6, 9), (2, 12), (8, 34), (23, 33), (17, 56), (32, 56)
  3. (2, 6, 9, 12), (8, 23, 33, 34), (17, 36, 56, 56)
  4. (2, 6, 9, 9, 12, 23, 33, 34), (17, 36, 56, 56)
  5. {2, 6, 8, 9, 12, 17, 23, 32, 33, 34, 56, 56}


# Algorithmday_4 정리 (2021.12.01 수요일)

## 기수 정렬(Radix Sort)
- 정렬할 원소의 키 값을 나타내는 숫자의 자리수(radix)를 기초로 정렬하는 기법(사전식 정렬 방법)
- 정렬하고자 하는 값을 버킷에 넣어 정렬
- 버킷으로 큐 사용
- 데이터가 입력되는 곳, 출력되는 곳 : 먼저 들어온 것이 먼저 출력
- 버킷의 개수는 키의 표현 방법과 밀접한 관계
  - 이진법을 사용한다면 버킷은 2개
  - 알파벳 문자를 사용한다면 버킷은 26개
  - 십진법을 사용한다면 버킷은 10개
- 기수 정렬 방법
  - 첫 번째 패스 (1라운드)
    - 정렬할 키의 가장 작은 자리수를 기준으로 분배 정렬
  - 두 번째 패스
    - 두 번째 작은 자리수를 기준으로 분배 정렬
    - 키 값이 같은 경우 이전 정렬에서의 순서를 그대로 유지
- 키의 가장 큰 자리수까지 반복 수행
- 한 자리 수의 기수 정렬 수행 예
  - 단순히 자리 수에 따라 버킷에 넣었다가 꺼내면 정렬된다.

## 사진

# Algorithmday_4 정리 (2021.12.01 수요일)

## 힙 정렬 (Heap Sort)
- 정렬할 원소를 힙(heap)이라는 자료 구조를 이용하여 정렬하는 방법
- 힙 구조
  - __완전 이진 트리로, 각 노드의 키 값이 자식 노드들의 키 값보다 작지 않은 트리__ 로서 __힙 루트는 트리 중 가장 큰 값__ 을 나타냄
- 힙 정렬 방법
  - 주어진 데이터로 이진 트리를 구성한 후 힙 구조 알고리즘과 힙 정렬 알고리즘을 수행
- 힙 구조 알고리즘
- 제일 늦게 구성된 트리 선택
  - 부모 노드와 자식 노드 중 가장 큰 값 선택
  - 부모 노드와 자식 노드 중 가장 큰 값을 비교하여 자식 노드가 크면 서로 위치 교환 (큰 값을 위로 보냄)

## 사진 두 장

- 힙 정렬 알고리즘
  - 근 노드의 값을 배열의 맨 마지막에 저장 (근 노드 삭제에 해당)
  - 빈 근 노드의 자리에선 자식 노드 가장 가장 큰 값 위치
  - 빈 자식 노드의 자리에는 서브 트리의 자식 노드 중 맨 마지막 노드 값으로 채움
  - 맨 마지막 노드부터 차례로 제거됨

## 사진

- 힙의 노드들이 배열에 저장된 모습

## 사진

- 원래 힙의 마지막 노드 40과 루트 90을 바꿈 

## 사진

- 힙 조건 위배 검사 후 조건에 위배 됐기 때문에 조건에 따라 노드를 움직여준다.

## 사진

- 또 힙 조건에 위배 됐기 때문에 노드 위치를 조정 후 조건을 만족했기 때문에 확정 후 제일 마지막 노드 확정

## 사진

- 80과 20이 교환된 후 힙 조건을 만족한 결과

## 사진

- 70과 10이 교환된 후 힙 조건을 만족한 결과

## 사진 6 7 8

- 위 과정 반복하고 마지막 결과

# Algorithmday_4 정리 (2021.12.01 수요일)

## 탐색(Search)
- 데이터의 집단 내에서 특정 데이터를 찾는 구조
- 탐색 알고리즘의 효율성은 탐색 집단의 구조가 어떻게 구성되어 있느냐에 따라 영향을 받음
- 컴퓨터가 가장 많이 하는 작업 중 하나

##### 탐색에 사용되는 자료 구조
- 배열, 연결 리스트, 트리, 그래프 등

##### 탐색 방법
- 순차 탐색
- 이진 탐색
- 보간 탐색
- 이진 트리 탐색

#### 순차 탐색(Sequential Search)
- 정렬되지 않은 데이터의 항목들을 처음부터 마지막까지 하나씩 검사하여 원하는 항목을 찾아가는 방법
- 탐색 방법 중 가장 간단하고 직접적인 방법
- 크기가 적은 리스트에서는 효율적이지만 크기가 큰 리스트에서는 매우 비 효율적
- 장점
  - 하나씩 비교하기 때문에 탐색 용이
  - 탐색 알고리즘 간단
- 단점 
  - 탐색 시간이 느리며 수행 시간이 많이 걸림
- 9 5 8 3 7일 때 8을 찾는 경우 첫 인덱스부터 순차 탐색 하면 3번째에 찾음.
- 9 5 8 3 7일 때 2를 찾는 경우 첫 인덱스부터 순차 탐색 하면 탐색 실패.

#### 이진 탐색(Binary Search)
- 전체 데이터 집합을 두 부분으로 나누어 검색하고자 하는 값이 어느 부분에 속하는 가를 결정하여 그 부분에 대하여 순환적으로 탐색을 수행하는 방법
- 정렬된 리스트에서 중간에 위치한 키 값과 찾고자 하는 값이 같으면 탐색 성공
- 탐색 실패 했을 때 다시 중간 항목을 기준으로 두 부분중 한쪽 리스트를 선택하여 키를 정한 후 다시 이진 탐색해서 찾으면 성공
- 그래도 없으면 다시 나머지 다른 한 쪽 이진 탐색
- 특징
  - 분할 정복 기법에 의한 탐색 방법 중 하나
  - 리스트가 정렬되어 있는 경우 적합한 탐색 방법
  - 따라서 이진 탐색 방법을 적용할 경우 먼저 리스트 항목을 정렬시켜야 함
  - 레코드 삽입, 삭제가 빈번하게 발생되는 경우 리스트 재구성을 위해 항목의 이동이 발생하기 때문에 삽입, 삭제가 거의 없는 리스트에 적합
- 5를 탐색.
- [1, 3, 5, 6, 7, 9, 11, 20, 30] 중간 값을 키로 설정 (키 : 7)
- [1, 3, 5, 6] 이 탐색 영역이 된다. (5가 7보다 작기 때문에)
- [1, 3, 5, 6] 3을 키로 설정, 5와 비교
- 5가 3보다 크니 [5, 6]이 다시 탐색 영역
- [5, 6] 5를 키로 설정 찾고자 하는 값은 5 탐색 완료

#### 보간 탐색(Interpolation Search)
- 탐색하고자 하는 키 값의 위치를 예측하여 탐색하는 방법
- 사전이나 전화번호부를 탐색하는 방법과 동일
  - 사전을 찾을 때 'ㅎ'으로 시작하는 단어는 사전의 뒷 부분에서 찾고 'ㄱ'으로 시작하는 단어는 앞 부분에서 찾는 것과 같은 원리
- 보간 탐색은 이진 탐색과 유사하지만 리스트를 반이 아닌 불균등하게 분할하여 탐색
- 리스트가 정렬되어 있는 경우 적합
- 많은 데이터가 균등하게 분포되어 있는 경우 보간 탐색이 이진 탐색보다 우수

[##_Image|kage@YwcbC/btrmKZdEnbf/TfUeCBKYDZsISML0zWp8Q1/img.png|alignCenter|width="100%"|_##]

#### 이진 트리 탐색(Binary Tree Search)
- 탐색 속도와 항목을 효율적으로 수정할 수 있도록 주어진 리스트를 이진 트리로 구성하여 탐색하는 방법
- root node를 중심으로 좌측 트리는 root node 보다 작은 값, 우측 트리는 큰 값이 존재하도록 구성
- 이진 탐색과 이진 트리 탐색의 차이점
  - 근본적으로는 같은 원리
  - 이진 탐색은 삽입, 삭제시에 앞뒤 원소를 이동시켜야 하지만 이진 트리 탐색에서는 비교적 빠른 시간안에 삽입 삭제 가능
  - 삽입, 삭제가 빈번하다면 반드시 이진 트리 탐색 사용.
- 이진 탐색 트리에서 탐색
  - root node에서 시작
  - 키 값 = root node 탐색 종료
  - 키 값 > root node 오른쪽 서브트리만 탐색
  - 키 값 < root node 왼쪽 서브트리만 탐색
  - 탐색 성공하면 값 반환
  - 결과가 공백이면 실패
- 이진 탐색 트리에서 삽입
  - 키 값이 x인 원소를 삽입한다.
  - x를 키 값으로 가지고 있는 원소가 있는지 탐색
  - 탐색이 실패하면 탐색이 종료된 위치에 원소 삽입.
- 이진 탐색 트리에서의 삭제
  - 삭제하려는 원소의 키 값이 주어졌을 때 이 키값을 가진 원소를 탐색
  - 원소를 찾으면 삭제 연산 수행

##### 해당 노드의 자식수에 따른 세가지 삭제 연산

###### 자식이 없는 단말 노드의 삭제
- 제거할 노드가 단말 노드면 그대로 삭제

[##_Image|kage@dwQ57j/btrmKCiHjH3/DnKkKunZwyJQ2aj16hcjxK/img.png|alignCenter|width="100%"|_##]

###### 자식이 하나인 노드의 삭제
- 삭제되는 노드 자리에 그 자식 노드 트리를 위치

[##_Image|kage@vr6xp/btrmKZrbBxz/Sv23WeevRMQbpC5n8wIB61/img.png|alignCenter|width="100%"|_##]

###### 자식이 둘인 노드의 삭제
- 삭제되는 노드의 좌측 트리 중 제일 오른쪽 단말 노드로 대체

[##_Image|kage@3XR8C/btrmK0KoZ96/tUUA99AgiNfkLhC4gSPtq1/img.png|alignCenter|width="100%"|_##]

##### 이진 탐색 트리 예제

- Node.java

~~~java
public class Node {
    int value;
    Node leftchild;
    Node rightchild;

    // 생성자
    public Node(int value) {
        this.value = value;
        leftchild = null; // 객체이므로 null로 초기화
        rightchild = null;
    }
}
~~~

- BinaryTree.java

~~~java
public class BinaryTree {
    Node rootNode = null;

    public void insertNode(int element) {
        if(rootNode == null) { // 루트가 빈 경우 즉, 아무 노드도 없으면 노드 생성
            rootNode = new Node(element);
        }
        else {
            Node head = rootNode;
            Node currentNode;
            while (true) {
                currentNode = head;
                // 현재 루트보다 작은 경우 왼쪽으로 탐색
                if(head.value > element) {
                    head = head.leftchild;
                    // 왼쪽 자식 노드가 비어 있는 경우, 해당 위치에 추가할 노드 삽입
                    // 현재 currentNode는 head를 가리키고 있음
                    if(head == null) {
                        currentNode.leftchild = new Node(element);
                        break;
                    }
                }
                else { // 현재 루트보다 큰 경우 오른쪽으로 탐색
                    head = head.rightchild;
                    // 왼쪽 자식 노드가 비어 있는 경우, 해당 위치에 추가할 노드 삽입
                    // 현재 currentNode는 head를 가리키고 있음
                    if(head == null) {
                        currentNode.rightchild = new Node(element);
                        break;
                    }
                }
            }
        }
    }
    // 전위 순회 root - left - right
    public void preorderTree(Node root, int depth) {
        if(root != null) {
            for(int i = 0; i < depth; i++) {
                System.out.print("ㄴ");
            }
            System.out.println(root.value); // root
            preorderTree(root.leftchild, depth+1); // left
            preorderTree(root.rightchild, depth+1); // right
        }
    }
    // 중위 순회 left - root - right
    public void inorderTree(Node root, int depth) {
        if(root != null) {
            inorderTree(root.leftchild, depth+1); // left
            for(int i = 0; i < depth; i++) {
                System.out.print("ㄴ");
            }
            System.out.println(root.value); // root
            inorderTree(root.rightchild, depth+1); // right
        }
    }
    // 중위 순회 left - right - root
    public void postorderTree(Node root, int depth) {
        if(root != null) {
            postorderTree(root.leftchild, depth+1); // left
            postorderTree(root.rightchild, depth+1); // right
            for(int i = 0; i < depth; i++) {
                System.out.print("ㄴ");
            }
            System.out.println(root.value); // root
        }
    }
    public void searchBTree(Node n, int target) {
        try {
            if(target < n.value) {
                System.out.println("타겟이 " + n.value + "보다 작음");
                searchBTree(n.leftchild, target);
            }
            else if(target > n.value) {
                System.out.println("타겟이 " + n.value + "보다 큼");
                searchBTree(n.rightchild, target);
            }
            else {
                System.out.println("타겟이 " + n.value + "임");
            }
        } catch (Exception e) {
            System.out.println("찾지 못함.");
        }
    }
}
~~~

- BinaryTreeMain.java

~~~java
public class BinaryTreeMain {
    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();

        tree.insertNode(5);
        tree.insertNode(2);
        tree.insertNode(8);
        tree.insertNode(1);
        tree.insertNode(10);
        tree.insertNode(6);
        tree.insertNode(9);
        tree.insertNode(3);
        tree.insertNode(7);

        // 트리 운행(순회)
        tree.preorderTree(tree.rootNode, 0);
        System.out.println();
        tree.inorderTree(tree.rootNode, 0);
        System.out.println();
        tree.postorderTree(tree.rootNode, 0);
        System.out.println();
        // 이진 트리 검색
        tree.searchBTree(tree.rootNode, 10);
    }
}
~~~

# Algorithmday_4 정리 (2021.12.01 수요일)

## 해싱(Hashing)
- 해시 함수와 해시 테이블을 이용하여 데이터를 빠르게 저장하고 탐색하는 방법
- 데이터를 해시 테이블이라는 배열에 저장하고 데이터의 키 값으로 해시 함수를 통하여 테이블의 주소를 반환해서 원하는 데이터를 찾는 방식

#### 해시 테이블
- 값의 연산에 의해 직접 접근 가능한 구조

#### 해시 함수
- 해시 테이블에서 키 값을 주소로 변환하는데 사용되는 함수
- 계산이 빠르고 간단해야 하며, 다른 키 값이 같은 주소를 산출하는 경우가 적어야 함

## 사진

#### 해시 함수 종류
- 나눗셈법
- 중간 제곱법
- 폴딩법
- 기수 변환법
- 자리수 분석법

##### 나눗셈법
- 키 값을 정수로 보고 이를 적당한 양의 정수(주소, 해시 테이블의 크기 등)로 나누어서 그 나머지를 해시 주소로 하는 방법
- h(k) = k mod n
- h() : 해시 함수
- k : 키 값
- n : 나누는 수
- 특징
  - 주소 계산법이 매우 간단하지만 나누는 수 n을 적당하게 선택하는 것이 쉽지 않음
- n 선택 시 고려 사항
  - n 값은 충돌 발생의 가능성을 최소화하도록 선정
  - 따라서 나누는 값 n은 소수로 정하는 것이 좋다
- 나눗셈법 예
  - 키 값 : 172148
  - 주소 공간 영역 : 7000
  - 주소 공간 영역에 가까운 소수 : 6997
  - 해시 주소 : 4220
    - 172148 / 6997 = 몫 : 24, 나머지 4220

##### 중간 제곱법
- 키 값을 제곱한 다음 그 제곱값의 중간 부분의 적당한 자리수를 해시 주소로 정하는 방법
- 중간 제곱법 예
  - 키 값 k = 7642
  - k^2 = 58247424
  - 해시 테이블의 주소 : 2474
    - 58 __2474__ 24

##### 폴딩법
- 키를 같은 크기의 부분으로 나누고(접고), 이들을 모두 더하거나 XOR등을 취하여 해시 주소를 정하는 방법
- 이동 폴딩법
  - 오른쪽 끝을 맞추어 더한 값을 해시 주소로 정하는 방법
  - 탐색키 : (1 2 3 | 2 0 3 | 2 5 1 | 1 6 2 | 1 0)
  - 123 + 203 + 251 + 162 + 10 = 740

#### 해시 충돌
- 해시 테이블에 데이터를 삽입할 때 서로 다른 데이터가 같은 주소에 배당되는 것
- 오버플로우 라고 하기도 한다.
- 해결법
  - 선형 조사법
  - 2차 조사법
  - 체이닝

##### 선형 조사법
- 충돌이 일어난 항목을 해시 테이블의 다른 위치에 저장하는데 충돌이 발생한 자리에서 그 다음 버킷들을 차례로 하나씩 조사하여 최초로 나오는 빈 버킷에 데이터를 삽입
- 장점
  - 주소 계산 간단
- 단점
  - 조사 시간 많이 걸림
  - 해시 테이블 상 데이터의 위치가 일정한 키에 의해 집단으로 뭉치는 경향 발생

##### 2차 조사법
- 충돌이 발생했을 때 원래 주소로부터 2차 함수 되는 거리만큼 떨어진 곳을 차례로 탐색해서 최초로 나오는 빈 곳에 데이터 삽입
- 장점
  - 주소 계산 간단
  - 데이터들의 위치가 일정한 키를 중심으로 뭉치려는 경향을 어노 정도 배제할 수 있다.
- 단점
  - 해시 테이블 모든 버킷이 다 조사되지 않는다.

##### 체이닝 법
- 각 버킷에 삽입과 삭제가 용이한 연결 리스트를 구성하는 방법
- 해시 테이블 자체는 포인터의 배열로 만들고, 같은 버킷에 해당되는 데이터들을 체인(연결리스트)로 만들어서 연결
- 장점
  - 삽입, 삭제 시 문제 없음
- 단점
  - 포인터 연산이기 때문에 동적인 기억 장소 할당 필요
  - 링크 필드로 사용되는 부가적인 기억 장소 필요

## 사진