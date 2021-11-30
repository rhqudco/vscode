# Algorithmday_2 정리 (2021.11.29 월요일)

### 욕심쟁이 기법(Greedy Method) 이어서....
- 최적 대합을 구성할 수 있는 집합을 만들기 위해 필요한 원소들 각 단계마다 하나씩 선택해 나가는 방법
- 선택을 하는 매 순간마다 현재 상태에서 가장 좋아보이는 원소를 선택하는 전략
- 최적의 해를 찾는 전형적인 방법
- 즉, 각 순간 지역적으로 가장 좋아 보이는 선택이 모여 최종적으로도 가장 좋을 것이라 생각하기 때문에 나온 기법
- 최적화 문제를 해결할 수는 없지만 많은 경우의 문제에 적용 가능

#### 욕심쟁이 기법 적용 예(이어서....)
- 최단 경로 문제(Dijkstra의 최단 경로 알고리즘)
  - 하나의 출발점에서 모든 종착점으로의 최단 경로를 찾는 문제
  - 네트워크에서 하나의 시작 정점에서 모든 다른 정점까지 최단경로를 찾는 알고리즘
- 최소 비용 신장 트리(Prim 알고리즘, Kruscal 알고리즘)
    - MST(Minimum Spanning Tree)
    - 트리를 구성하는 간선들의 가중치를 합한 것이 최소가 되는 신장트리
    - 네트워크에 있는 모든 정점들을 가장 적은 수의 간선과 비용으로 연결하는 신장트리
    - 응용
      - 도시들을 모드 연결하면서 도로의 길이가 최소가 되도록 하는 문제
      - 단자들을 모두 연결하면서 전선의 길이가 최소가 되도록 하는 문제
      - 전화선의 길이가 최소가 되도록 전화 케이블 망을 구성하는 문제
      - 파이프를 모두 연결하면서 파이프의 총 길이가 최소가 되도록 하는 문제

#### 최단 경로 문제(Dijkstra의 최단 경로 알고리즘)
- 하나의 출발점에서 모든 종착점으로의 최단 경로를 찾는 문제
- 네트워크에서 하나의 시작 정점에서 모든 다른 정점까지 최단경로를 찾는 알고리즘
- 집합 S
  - 시작 정점 V로 부터 최단 경로가 이미 발견된 정점들의 집합
- distance 배열
  - 최단 경로를 알려진 정점만을 통하여 각 정점까지 가는 최단 경로의 길이
  - 매 단계에서 가장 distance 값이 적은 (최적의)정점을 S에 추가

## 사진

#### 프림(Prim)의 알고리즘
- 한번에 하나의 간선을 선택하여 최소 비용 신장 트리 T에 추가
- 구축 전 과정을 통해 하나의 트리만을 계속 확장
- 이 과정은 트리가 n-1개의 간선을 가질 때 까지 계속

## 사진

#### 크루스컬(Kruscal)의 알고리즘
- 한번에 하나의 간선을 선택하여 최소 비용 신장 트리 T에 추가
- 비용이 가장 적은 간선을 선정하되, 이미 T에 포함된 간선들과 사이클을 형성하지 않는 간선만을 추가
- 비용이 같은 간선들을 임의의 순서로 하나씩 추가

## 사진

### 동적 프로그래밍 기법(Dynamic Programming)
- 분할 정복 기법과 유사하게 부분 문제의 해답을 이용하는 방식으로 문제를 해결하는 방식
- 주어진 문제를 여러 개의 소문제로 분할하여 문제를 해결
- 상향식 설계 기법
  - 작은 문제부터 먼저 해결한 후 그 결과를 큰 문제에서 활용함으로써 효율성을 높이는 방법

#### 동적 프로그래밍 방식 적용 방법
- 분할 정복식처럼 문제를 나눈 후 주어진 부분 문제들을 한 번 계산한 후에는 특정 장소에 저장
- 이 부분 문제의 해가 필요할 때 이를 다시 계산하지 않고 이전에 저장해둔 결과 이용
- 일반적으로 부분 문제의 값을 저장하는 장소는 배열 사용

### 분할 정복 기법 VS 동적 프로그래밍 기법
- 분할 정복 기법(하향식)
  - 분할되는 소문제가 독립적이라 소문제를 재귀적으로 풀어 그 결과를 합침
  - 중복된 계산이 계속 발생
  - 중복 문제를 방지하기 위해 동적 프로그래밍 기법 사용
- 동적 프로그래밍 기법(상향식)
  - 부분 문제의 해답을 이용하는 방식으로 문제 해결(분할 정복 기법과 동일)
  - 소문제의 계산 결과로 표(배열)에 저장해 놓고 필요할 때 저장된 값 사용
  - 따라서 중복 계산을 하지 않는다

#### 동적 프로그래밍 적용 대상
- 최소치 또는 최대치를 구하는 최적하 문제에 적용
- 최적해는 기본적인 소문제의 최적해로부터 더 큰 크기의 소문제의 최적해를 구하는 과정을 거침
- 최적화 문제의 최적해는 여러 개가 있을 수 있지만 그 중 하나를 구하면 됨.

#### 동적 프로그래밍 방법 적용 예
- 피보나치 수열
- 조약돌 놓기 문제
- 행렬 경로 문제
- 연쇄 행렬 곱셈
- 이항 계수
- 최단 경로 구하기

#### 조약돌 놓기 문제
- 조약돌을 놓는 방법(제약조건) 
  - 각 열에 적어도 하나의 조약돌을 놓아야 한다.
  - 가로나 세로에 인접한 두 칸에 동시에 조약돌을 놓을 수 없다.
  - 목표 : 돌이 놓인 자리에 있는 수의 합을 최대가 되도록 조약돌 놓기

## 사진

#### 행렬 경로 문제
- 양수 또는 음수 원소들로 구성된 (n,n)행렬
- 행렬의 좌상단에서 시작하여 우하단까지 이동
- 제약 조건
  - 오른쪽이나 아래로만 이동 가능
  - 왼쪽, 위, 대각선 이동 불가
- 목표
  - 행렬의 좌상단에서 시작하여 우하단까지 이동하되
  - 방문한 칸에 있는 수들을 더한 값이 최소가 되도록 한다.

## 사진

## 자료 구조
- 순차 리스트
  - 배열 / 행렬 / 레코드
  - 스택 / 큐 / 데크
- 연결 리스트
  - 단일 연결리스트
  - 원형 연결리스트
  - 이중 연결리스트
- 트리
  - 일반 트리
  - 이진 트리

### 순차 리스트
- 각 자료가 메모리 중에서 서로 이웃해 있는 구조
- 선형 구조라고도 함
- 메모리에 연속되어 저장
- 배열 / 행렬 / 레코드 / 스택 / 큐 / 데크

### 배열
- 크기와 데이터형이 같으며 동일한 이름을 같은 원소들의 연속적 저장 영역
- 배열의 원소는 메모리 내에서 연속적으로 순서대로 저장
- 각 배열의 원소는 첨자([0]~[n])로 구별

### 레코드
- 서로 다른 데이터 형태와 크기로 구성되어 있는 이질적 데이터 구조
- 예 : 다양한 사람들에 대한 자료들인 이름, 주민등록번호, 주소 등 서로 관계있는 여러 자료를 한 개의 조로 묶어서 구성
- 배열과 차이점 : 배열은 데이터 원소의 크기와 형태가 동일하지만 레코드는 데이터 원소의 크기, 형태 서로 다르다.

### 스택(Stack)
- 선형 리스트 구조의 특별한 형태
- 리스트 내의 데이터 삽입과 삭제가 Top라고 하는 한쪽 끝에서만 일어나는 데이터 구조
- 데이터 구조에서는 기억 장치에 데이터를 일시적으로 쌓아 두었다가 필요할 때 꺼내서 사용할 수 있는 메모리나 레지스터의 일부를 항당하여 사용하는 임시적인 기억을 말함
- Push / Pop으로 가장 마지막에 삽입한 데이터를 제일 먼저 삭제
- LIFO(Last In First Out)리스트라고도 불린다.

## 사진

- TOP(Top Point)
  - 스택에 대한 삽입과 삭제가 이루어지는 위치
  - 가장 최근에 입력된 항목의 위치를 가리키는 포인터
  - 출력 우선 순위가 가장 높은 원소를 가리키는 포인터
  - 초기에 TOP는 0부터 시작하지만 배열로 스택 구현 시 배열 첨자가 0부터 시작하므로 TOP은 -1로 초기화 한다.
- BOTTOM
  - TOP의 반대쪽으로 노드의 입출력 불가
- PUSH
  - 스택에 새로운 노드 입력(삽입)
  - TOP = TOP + 1
- POP
  - 스택에서 노드 삭제
  - TOP = TOP - 1
- 오버플로우(Overflow)
  - 스택이 가득차 있을 때(TOP == n(n은 스택의 크기)) 스택에 더 이상 삽입할 수 없는 경우
  - 스택에 삽입 전 오버플로우가 발생하는지 확인해야 함.(isFull())
- 언더플로우(Underflow)
  - 스택이 비어있을 때(TOP == 0) 노드가 없어서 노드를 더 이상 삭제할 수 없는 경우
  - 스택 삭제 전 언더플로우가 발생하는지 확인해야 함.(isEmpty())
- 스택에서 사용되는 연산
  - 삽입 (push)
    - if TOP == n then overflow exist
    - TOP = TOP + 1
    - stack[TOP]  <-  insert_data
  - 삭제 (pop)
    - if TOP = 0 then underflow exist
    - deleted_data <- stack[TOP]
    - TOP = TOP -1

##### 스택 예제
1. 배열을 사용한 스택 구현
   - index가 0부터 시작하므로 초기 상태를 -1로 설정
   - top = -1 이면 empty, pop하면 underflow 발생

- MyStack.java (메소드 구현)

~~~java
package AlgoPractice.stack;

public class MyStack {
    // 멤버 변수
    private int stackSize; // 스택 크기
    private int top; // 스택 포인터
    private char[] stackArr; // 스택(배열 변수만 선언하고 할당, 크기 설정 안됨)

    // 생성자
    public MyStack(int stackSize) {
        top = -1;
        this.stackSize = stackSize; // 스택 크기만 설정
        stackArr = new char[this.stackSize]; // 스택 배열 생성
    }

    // 메서드
    // 스택이 비었는지 isEmpty() 결과는 true(비었을 때) / false(가득  찼을 때)로 반환
    public boolean isEmpty() {
        if(top == -1) return true;
        else return false;
    }
    // 스택이 차있는지 isFull() 결과는 true(가득 찼을 때) / false(가득 아닐 때)로 반환
    public boolean isFull() {
        if(top == stackSize-1) return true;
        else return false;
    }
    // 스택에 데이터를 삽입하는 push()
    // 1. 삽입 전 overflow 발생하는지 확인
    // 2. overflow가 아니면 삽입 push 시작
    // 3. top 위치 확인 후 top+1(++top)에 삽입
    // 삽입을 위한 매개변수를 받고 반환 값은 없다.
    public void push(char input) {
        if(isFull()) {
            System.out.println("Stack is Full\nOverFlow!!!\npush Failed");
        }
        else {
            // push 할 때 먼저 1증가
            stackArr[++top] = input;
        }
    }
    // 스택에 데이터를 삭제하는 pop()
    // 1. 데이터 삭제 전 underflow 검사
    // 2. underflow가 아니면 데이터 삭제
    // 3. top 위치 확인 후 top위치 삭제 후 top-1
    // 삭제한 문자를 반환
    public char pop() {
        if(isEmpty()) {
            System.out.println("Stack is Empty\nUnderFlow!!!\npop Failed");
            return 'E'; // 형식적인 반환 값
        }
        else {
            return stackArr[top--];
        }
    }
    // 스택의 최상위 데이터 출력하는 peek()
    // 1. 스택에 값이 있는지 확인 isEmpty()
    // 2. 최상위 데이터(top위치) 리턴
    public char peek() {
        if(isEmpty()) {
            System.out.println("Stack is Empty \n ");
            return 'E'; // 형식적인 반환 값
        }
        else {
            return stackArr[top];
        }
    }
    //  스택을 비우는 clear()
    // 1. top = -1로
    // 2. stack 값 모두 삭제
    public void clear() {
        top = -1;
    }
    // 스택의 전체 데이터를 출력하는 showStack()
    // 출룍먼 하고 반환 값은 없다
    // 1. 출력 전 비었는지 확인(반환 값 없음)
    // 2. 스택 모든 요소 값 출력
    public void showStack() {
        if(isEmpty()) {
            System.out.println("Stack is Empty");
        }
        else {
            System.out.print("Stack Items : ");
            for(int i = 0; i <= top; i++) {
                System.out.print(i + ":" + stackArr[i] + " ");
            }
            System.out.println("\ntop : " + top);
            System.out.println("top index is " + stackArr[top]);
        }
    }
}
~~~

- MyStackMain (Main 메소드)

~~~java
package AlgoPractice.stack;

public class MyStackMain {
    public static void main(String[] args) {
        int stackSize = 5; // 스택 크기
        MyStack myStack = new MyStack(stackSize);

        System.out.print("스택 초기 : ");
        myStack.showStack();

        System.out.println();
        System.out.println("pop 수행");
        myStack.pop();

        System.out.println();
        System.out.println("a, b, c push 수행");
        myStack.push('a');
        myStack.push('b');
        myStack.push('c');
        myStack.showStack();

        System.out.println();
        System.out.println("최상위 값 : " + myStack.peek());

        System.out.println();
        System.out.println("d, e, push 수행");
        myStack.push('d');
        myStack.push('e');
        myStack.showStack();

        System.out.println();
        System.out.println("f push 수행");
        myStack.push('f');

        System.out.println();
        System.out.println("pop 두 번 수행");
        System.out.println("pop 한 값 : " + myStack.pop());
        System.out.println("pop 한 값 : " + myStack.pop());
        myStack.showStack();

        System.out.println();
        System.out.println("clear 수행");
        myStack.clear();
        myStack.showStack();

        System.out.println();
        System.out.println("h push 수행");
        myStack.push('h');
        myStack.showStack();
    }
}
~~~

2. 자바에서 제공하는 스택 클래스를 사용한 스택 구현

- UtilStack.java(util에서 제공하는 메인 메소드로 구현)

~~~java
package AlgoPractice.stack;

import java.util.Stack;

public class UtilStack {
    public static void main(String[] args) {
        Stack<String> stk = new Stack<String>();

        stk.push("메시");
        stk.push("호날두");
        stk.push("고병채");

        for(int i =0; i<stk.size(); i++) {
            System.out.println(i + " : " + stk.get(i)); //get은 값만 출력(pop이 아님)
        }
        System.out.println();
        System.out.println("스택 크기 : " + stk.size());
        System.out.println("최상위 값 : " + stk.peek());

        System.out.println();
        System.out.println("호날두가 들어 있나? : " + stk.contains("호날두"));
        System.out.println("호날두가 들어 있나? : " + stk.contains("음바페"));

        System.out.println();
        System.out.println("pop 수행1 : " + stk.pop());
        System.out.println("pop 수행2 : " + stk.pop());
        for(int i =0; i<stk.size(); i++) {
            System.out.println(i + " : " + stk.get(i)); //get은 값만 출력(pop이 아님)
        }

        System.out.println();
        System.out.println("clear 수행");
        stk.clear();
        System.out.println("empty ? -> " + stk.empty());

        try {
            System.out.println();
            System.out.println("pop 수행3 : " + stk.pop());
        } catch (Exception e) {
            System.out.println();
            System.out.println(e.toString());
        }

    }
}
~~~

### 큐(Queue)
- 선형 리스트 구조의 특별한 형태
- 기억장소의 한쪽 끝에서 데이터 입력이 이루어지고, 다른 한쪽에서 데이터의 삭제가 이루어지는 구조
- 먼저 삽입한 데이터가 먼저 삭제되는 선입선출(FIFO : First In First Out)구조
- 전위 포인터(Front)
  - 데이터가 삭제되는 끝을 가르키는 포인터
- 후위 포인터(Rear)
  - 데이터가 삽입되는 끝을 가르키는 포인터

## 사진

- 큐에서 오버플로우 해결 방법
  - 후위 포인터(Rear)의 값이 n(큐의 크기)과 같을 때 새로운 데이터를 삽입하면 오버폴르오 발생
  - 이동 큐(moving queue) 사용
    - 앞 부분이 비어 있는 경우 큐의 데이터를 앞 부분으로 이동
    - 문제 : 데이터 이동에 따른 시간적 부담

## 사진

  - 원형 큐(circular queue) 사용
    - 선형 큐의 앞(front)과 뒤(rear)를 이어 놓은 형태의 큐
    - 새로운 항목을 삽입하기 위하여 rear를 시계방향으로 증가

## 사진

- 큐의 응용
  - 작업 도착 순서에 의한 스케줄링
  - front A - B - C - D rear
    - A -> B -> C -> D 순서로 작업

##### 큐 예제

- 큐 예제 1번
  - 앞이 비었는데도 오버플로우 발생 : 이동 없음

- MyQueue.java(배열을 통해 직접 구현 메소드)

~~~java
package AlgoPractice.queue;

// 앞이 비었는데도 오버플로우 발생 : 이동 없음
public class MyQueue {
    // 멤버 변수
    private int queueSize; // 큐의 용량
    private int front; // front -> 전위 포인터
    private int rear; // rear -> 후위 포인터
    private int num; // 현재 데이터 수
    private char[] queue;

    // 생성자에서 초기화
    public MyQueue(int queueSize) {
        // 배열을 사용하므로 초기값 -1로 설정
        front = -1;
        rear = -1;
        num = 0;
        this.queueSize = queueSize;
        queue = new char[queueSize];
    }

    // 큐가 비어있는지 상태 확인 isEmpty() true / false 반환
    public boolean isEmpty()  {
        if(front == rear) {
            front = -1;
            rear = -1;
            return true;
        }
        else return false;
    }

    // 큐가 가득 차있는 상태 확인 isFull()
    public boolean isFull() {
        return rear == queueSize -1;
    }

    // 큐에 데이터 삽입 enQueue()
    // 1. Full인지 확인
    // 2. 데이터 삽입
    public void enQueue(char item) {
        if(isFull()) {
            System.out.println("Queue is Full");
        }
        else {
            queue[++rear] = item;
            num++; // 데이터 수 증가
        }
    }

    // 큐에서 데이터 삭제 deQueue()
    // 1. Empty인지 확인
    // 2. 데이터 삭제
    // 3. 데이터 반환
    public char deQueue() {
        if(isEmpty()) {
            return 'E';
        }
        else {
            num--; // 데이터 수 감소
            front++;
            return queue[front];
        }
    }

    // 큐의 첫 번째 데이터 추출하는 peek()
    // 추출해서 반환
    public char peek() {
        if (isEmpty()) {
            System.out.println("Queue is Empty!!! peek Failed");
            return 'E';
        }
        else {
            return queue[front+1];
        }
    }

    // 큐 초기화 하는 clear()
    public void clear() {
        front = -1;
        rear = -1;
        System.out.println("Clear!!!");
    }

    // 큐에 들어있는 모든 데이터 출력하는 showQueue()
    // 1. 비었는지 확인
    // 2. 큐애 있는 모든 데이터 출력
    public void showQueue() {
        if(isEmpty()) {
            System.out.println("Queue is Empty!!! showQueue Failed");
        }
        else {
            System.out.print("Queue items : ");
            for(int i = front+1; i <= rear; i++) { // front + 1 부터 rear까지
                System.out.print(i + ":" + queue[i] + " ");
            }
            System.out.println("\nFront = " + (front+1) + " Rear = " + rear);
        }
    }
    //  데이터의 갯수를 반환하는 numOfDate()
    public int numOfDate() {
        return num;
    }
}
~~~

- 배열을 통해 직접 구현(Main 메소드)

~~~java
package AlgoPractice.queue;

public class MyQueueMain {
    public static void main(String[] args) {
        int queueSize = 5;
        MyQueue myQueue = new MyQueue(queueSize);

        myQueue.showQueue();
        System.out.println("데이터 : " + myQueue.numOfDate() + "개");

        System.out.println();
        System.out.println("a, b, c enQueue");
        myQueue.enQueue('a');
        myQueue.enQueue('b');
        myQueue.enQueue('c');
        myQueue.showQueue();
        System.out.println();
        System.out.println("데이터 : " + myQueue.numOfDate() + "개");

        System.out.println();
        System.out.println("peek() 수행(첫 번째 값) = " + myQueue.peek());

        System.out.println();
        System.out.println("deQueue 수행");
        System.out.println("삭제된 값 : " + myQueue.deQueue());
        myQueue.showQueue();
        System.out.println();
        System.out.println("데이터 : " + myQueue.numOfDate() + "개");

        System.out.println();
        System.out.println("peek() 수행(첫 번째 값) = " + myQueue.peek());

        System.out.println();
        System.out.println("d, e enQueue");
        myQueue.enQueue('d');
        myQueue.enQueue('e');
        myQueue.showQueue();
        System.out.println("데이터 : " + myQueue.numOfDate() + "개");

        // 0은 비었고 1~4까지 데이터 4개 있음
        System.out.println();
        System.out.println("f enQueue");
        myQueue.enQueue('f');
        myQueue.showQueue();
        System.out.println("데이터 : " + myQueue.numOfDate() + "개");
        // 앞 공간이 비었어도 rear가 QueueSize와 동일하기 때문에 가득 찼다고 오류 발

        System.out.println();
        System.out.println("clear() 수행");
        myQueue.clear();
        myQueue.showQueue(); // Empty

        myQueue.enQueue('g');
        myQueue.showQueue(); // Queue items : 0:g
    }
}
~~~

- 큐 예제 2번
  - 앞이 비었기 때문에 앞으로 이동해서 오버플로우 해결
  - MyQueueMove 클래스
    - isFull()
      - rear가 마지막 인덱스와 동일하고 데이터 수가 queueSize와 동일하면 full 상태
    - enQueue()
      - full 인지 확인
      - 현재 Queue를 0번 인덱스부터 시작하도록 이동

- MyQueueMove.java

~~~java
package AlgoPractice.queue;

// 앞이 비었는데도 오버플로우 발생 : 해결 하는 방법
public class MyQueueMove {
    // 멤버 변수
    private int queueSize; // 큐의 용량
    private int front; // front -> 전위 포인터
    private int rear; // rear -> 후위 포인터
    private int num; // 현재 데이터 수
    private char[] queue;

    // 생성자에서 초기화
    public MyQueueMove(int queueSize) {
        // 배열을 사용하므로 초기값 -1로 설정
        front = -1;
        rear = -1;
        num = 0;
        this.queueSize = queueSize;
        queue = new char[queueSize];
    }

    // 큐가 비어있는지 상태 확인 isEmpty() true / false 반환
    public boolean isEmpty()  {
        if(front == rear) {
            front = -1;
            rear = -1;
            return true;
        }
        else return false;
    }

    // 큐가 가득 차있는 상태 확인 isFull()
    public boolean isFull() {
        if ((rear == queueSize - 1) && (queueSize == num)) {
            return true;
        }
        else return false;
    }

    // 큐에 데이터 삽입 enQueue()
    // 1. Full인지 확인
    // 2. 데이터 삽입
    public void enQueue(char item) {
        if(isFull()) {
            System.out.println("Queue Full!");
        } else if(num != 0 && rear == queueSize -1){
            // rear가 마지막 인덱스와 동일하지만
            // 데이터가 1개라도 들어 있는 경우
            // queue 이동 : 현재 queue를 복사해서
            // 시작 인덱스 0으로 덮어 씀
            //System.arraycopy(소스, 시작인덱스, 대상, 시작인덱스, 길이);
            System.arraycopy(queue, front+1, queue, 0, queue.length - 1);
            System.out.println("큐 이동 발생");
            rear--;
            front = -1;

            queue[++rear] = item; // rear 다음 위치에 데이터 삽입
            num++;
        }else {
            queue[++rear] = item; // rear 다음 위치에 데이터 삽입
            num++;  			  // 데이터 수 증가
        }
    }


    // 큐에서 데이터 삭제 deQueue()
    // 1. Empty인지 확인
    // 2. 데이터 삭제
    // 3. 데이터 반환
    public char deQueue() {
        if(isEmpty()) {
            return 'E';
        }
        else {
            num--; // 데이터 수 감소
            front++;
            return queue[front];
        }
    }

    // 큐의 첫 번째 데이터 추출하는 peek()
    // 추출해서 반환
    public char peek() {
        if (isEmpty()) {
            System.out.println("Queue is Empty!!! peek Failed");
            return 'E';
        }
        else {
            return queue[front+1];
        }
    }

    // 큐 초기화 하는 clear()
    public void clear() {
        front = -1;
        rear = -1;
        System.out.println("Clear!!!");
    }

    // 큐에 들어있는 모든 데이터 출력하는 showQueue()
    // 1. 비었는지 확인
    // 2. 큐애 있는 모든 데이터 출력
    public void showQueue() {
        if(isEmpty()) {
            System.out.println("Queue is Empty!!! showQueue Failed");
        }
        else {
            System.out.print("Queue items : ");
            for(int i = front+1; i <= rear; i++) { // front + 1 부터 rear까지
                System.out.print(i + ":" + queue[i] + " ");
            }
            System.out.println("\nFront = " + (front+1) + " Rear = " + rear);
        }
    }
    //  데이터의 갯수를 반환하는 numOfDate()
    public int numOfData() {
        return num;
    }
}
~~~

- MyQueueMoveMain.java

~~~java
package AlgoPractice.queue;

public class MyQueueMoveMain {
    public static void main(String[] args) {
        int queueSize = 5;
        MyQueueMove myQueueMove = new MyQueueMove(queueSize);

        myQueueMove.showQueue();
        System.out.println("데이터 : " + myQueueMove.numOfData() + "개");

        System.out.println();
        System.out.println("a, b, c enQueue");
        myQueueMove.enQueue('a');
        myQueueMove.enQueue('b');
        myQueueMove.enQueue('c');
        myQueueMove.showQueue();
        System.out.println();
        System.out.println("데이터 : " + myQueueMove.numOfData() + "개");

        System.out.println();
        System.out.println("peek() 수행(첫 번째 값) = " + myQueueMove.peek());

        System.out.println();
        System.out.println("deQueue 수행");
        System.out.println("삭제된 값 : " + myQueueMove.deQueue());
        myQueueMove.showQueue();
        System.out.println();
        System.out.println("데이터 : " + myQueueMove.numOfData() + "개");

        System.out.println();
        System.out.println("peek() 수행(첫 번째 값) = " + myQueueMove.peek());

        System.out.println();
        System.out.println("d, e enQueue");
        myQueueMove.enQueue('d');
        myQueueMove.enQueue('e');
        myQueueMove.showQueue();
        System.out.println("데이터 : " + myQueueMove.numOfData() + "개");

        // 현재 큐 상태 : 0은 비었고, 1~4까지 4개 데이터가 들어 있음
        // 큐 이동 없는 경우
//		System.out.println("\nf enqueue 수행");
//		q.enqueue('f');   // Queue Full!
//		q.showQueue();    // Queue items : 1:b 2:c 3:d 4:e
//		System.out.println("\n데이터 : " + q.numOfData()); // 데이터 : 4

        // 앞 공간이 비었더라도 rear가 stackSize(인덱스 4, 5개)와 동일하면 오버플로우 발생
        // --> 해결1 : 이동 큐, 해결2 : 원형 규

        // 이동 큐
        System.out.println("\nf enQueue 수행");
        myQueueMove.enQueue('f');   // 큐 이동 발생
        myQueueMove.showQueue();    // Queue items : 0:b 1:c 2:d 3:e 4:f
        System.out.println("\n데이터 : " + myQueueMove.numOfData()); // 데이터 : 5

        System.out.println("\ng enQueue 수행");
        myQueueMove.enQueue('g'); // Queue Full!
        myQueueMove.showQueue();  // Queue items : 0:b 1:c 2:d 3:e 4:f

        System.out.println("\ndeQueue 수행");
        System.out.println("삭제된 값 : " + myQueueMove.deQueue()); // 삭제된 값 :b
        myQueueMove.showQueue();  // Queue items : 1:c 2:d 3:e 4:f

        System.out.println("\nclear 수행 ");
        myQueueMove.clear();
        myQueueMove.showQueue(); // Queue Empty

        System.out.println("\nh enQueue 수행");
        myQueueMove.enQueue('h'); // Queue Full!
        myQueueMove.showQueue(); // Queue items : 0:h
    }
}
~~~

- 큐 예제 3번
  - java.util.Queue 인터페이스를 LinkedList로 구현
  - ArrayList로 구현할 경우 추가/삭제 시 데이터 이동이 필요하기 때문

- QueueLinkedList.java

~~~java
package AlgoPractice.queue;

import java.util.LinkedList;
import java.util.Queue;

public class QueueLinkedList {
    public static void main(String[] args) {
        Queue<String> q = new LinkedList<String>();

        // 큐에 값 추가
        System.out.println("큐에 값 4개 삽입");
        q.add("홍길동");
        q.add("이몽룡");
        q.add("성춘향");

        q.offer("김철수");

        System.out.println("\n큐의 내용 출력");
        System.out.println(q);  			// [홍길동, 이몽룡, 성춘향, 김철수]
        System.out.println(q.toString());	// [홍길동, 이몽룡, 성춘향, 김철수]

        System.out.println("\n큐의 크기 : " + q.size()); //큐의 크기 : 4 (데이터 수)
        System.out.println("\npeek 수행. 첫 번째 값 출력 : " + q.peek()); // 홍길동

        System.out.println("\n첫 번째 값 삭제 : " + q.poll()); // 홍길동
        System.out.println(q); 								// [이몽룡, 성춘향, 김철수]

        // 또는 remove() 사용
        System.out.println("\n첫 번째 값 삭제 : " + q.remove()); // 이몽룡
        System.out.println(q);								  // [성춘향, 김철수]

        // remove("검색어")는 검색해서 삭제 가능
        System.out.println("\n검색한 값 삭제(없는 경우) : " + q.remove("강길동"));
        System.out.println("\n검색한 값 삭제(찾은 경우) : " + q.remove("김철수"));
        System.out.println(q);
    }
}
~~~

### 데크(deQue : double endedQueue)
- 삽입과 삭제가 양끝에서 이루어지는 구조
- 스택과 큐를 하나의 선형 리스트 구조에 복합시킨 형태
- end1과 end2 포인터 사용
- 양쪽 끝에서의 오버플로우의 가능성을 줄이기 위해 데크 내의 중심 근처에부터 저장 가능

## 사진

##### 데크 예제

- DequeArray.java

~~~java
package AlgoPractice.deque;

import java.util.ArrayDeque;
import java.util.Deque;

public class DequeArray {
    public static void main(String[] args) {
        Deque<String> deque = new ArrayDeque<String >();

        System.out.println("데이터 3개 삽입");
        deque.add("사과");
        System.out.println(deque);
        deque.add("딸기");
        System.out.println(deque);
        deque.add("망고");
        System.out.println(deque);
        deque.offer("수박");
        System.out.println(deque); // [사과, 딸기, 망고, 수박]

        System.out.println();
        System.out.println("앞쪽에 삽입");
        deque.addFirst("배");
        System.out.println(deque); // [배, 사과, 딸기, 망고, 수박]

        System.out.println();
        System.out.println("그냥 삽입");
        deque.add("용과");
        System.out.println(deque); // [배, 사과, 딸기, 망고, 수박, 용과]

        System.out.println();
        System.out.println("뒤쪽에 삽입");
        deque.addLast("용과"); // add랑 비슷하게 들어감 / 똑같은 값 삽입 가능
        System.out.println(deque); // [배, 사과, 딸기, 망고, 수박, 용과, 포도]

        System.out.println();
        System.out.println("peek 수행 : " + deque.peek());
        System.out.println("deQue 사이즈 : " + deque.size());

        System.out.println();
        System.out.println("순회");
        for (String item : deque) {
            System.out.print(item + " ");
        }
        System.out.println();

        System.out.println();
        System.out.println("데이터 꺼내기");
        System.out.println("remove : " + deque.remove());
        System.out.println(deque);

        System.out.println();
        System.out.println("찾아서 삭제");
        System.out.println("사과 remove : " + deque.remove("사과")); // true
        System.out.println(deque);

        System.out.println();
        System.out.println("찾아서 삭제");
        System.out.println("코코넛 remove : " + deque.remove("코코넛")); // false
        System.out.println(deque);

        System.out.println();
        System.out.println("앞쪽에 삽입");
        deque.addFirst("용과");
        System.out.println(deque);

        System.out.println();
        System.out.println("찾아서 삭제");
        System.out.println("용과 remove : " + deque.remove("용과")); // true
        System.out.println(deque);
        // [용과, 딸기, 망고, 수박, 용과, 용과] -> [딸기, 망고, 수박, 용과, 용과]

        System.out.println();
        System.out.println("remove All : " + deque.removeAll(deque)); // 전체 삭제
        System.out.println(deque);

        System.out.println();
        System.out.println("데이터 3개 삽입");
        deque.add("사과");
        System.out.println(deque);
        deque.add("딸기");
        System.out.println(deque);
        deque.add("망고");
        System.out.println(deque);
        deque.offer("수박");
        System.out.println(deque); // [사과, 딸기, 망고, 수박]

        System.out.println();
        System.out.println("poll : " + deque.poll()); // 맨 앞에 있는 값 삭제
        System.out.println(deque); // [딸기, 망고, 수박]

        System.out.println();
        System.out.println("pollFirst : " + deque.pollFirst());
        System.out.println(deque); // [망고, 수박]

        System.out.println();
        System.out.println("pollLast : " + deque.pollLast());
        System.out.println(deque); // [망고]

        // deQue를 Stack처럼 사용
        System.out.println();
        System.out.println("push 수행");
        deque.push("밤"); // addFirst와 동일
        deque.push("밤");
        System.out.println(deque);

        System.out.println();
        System.out.println("pop 수행 : " + deque.pop()); // 맨 앞 삭제
        System.out.println(deque);
    }
}
~~~

## 제네릭(Generic)
- 클래스(인터페이스)나 메서드를 타입 파라미터를 이용하여 선언하는 기법

~~~java
public class 클래스명<T> {......}
~~~

~~~java
public interface 인터페이스명<T> {.........}
~~~

~~~java
class Gen<T> {
    private T value;
}
~~~

- 클래스 설계 시 타입 <T>는 아직 결정되지 않았음
- 모든 종류의 타입을 다룰 수 있음
- 선언 시 클래스 또는 인터페이스 이름 뒤에 <> 붙임
- <> 사이에 타입 파라미터 위치 -> <T>
- 타입 파라미터
  - 일반적으로 대문자 알파벳 한 문자로 표현
  - E : Element
  - T : Type
  - V : Value
  - K : Key
- 개발 코드에서는 타입 파라미터 자리에 구체적인 타입을 지정해야 함 

~~~java
Gen<String> gen = new Gen<String>();
~~~

~~~java
Gen<Integer> gen = new Gen<String>();
~~~

- 클래스 내부에서 사용할 데이터 타입을 클래스 외부에서 지정
- <> 에는 기본 데이터 타입은 올 수 없다.
  - <int> 불가능
  - <Integer>가능
    - Wrapper 클래스 사용
    - 기본 데이터 타입에 대응되는 클래스
    - 기본 데이터 타입을 객체로 포장
- 제네릭을 사용하는 코드의 이점
  - 컴파일 시 강한 타입 체크 가능
    - 실행 시 타입 에러가 나는 것 방지
    - 컴파일시 미라 타입을 강하게 체크해서 에러를 사전에 방지
  - 강제 형 변환 과정을 제거 가능(프로그램 성능 향상)

- 제네릭을 하지 않을 경우

~~~java

List list = new ArrayList();
list.add(“abc”);
String str = (String) list.get(0); 
// Object 타입 반환 -> String 타입으로 형 변환
// 강제 타입 변환 발생
~~~

- 제네릭을 사용할 경우

~~~java
List<String> list = new ArrayList<String>();
list.add(“abc”);
String str = list.get(0); 
// 강제 타입 변환 발생하지 않음
// 제네릭 : 컴파일 시 타입 결정
~~~

- 오버라이드 메소드 : 실행 시 결정 (동적 다형성 이용)

- 제네릭은 클래스나 인터페이스를 설계할 때 구체적인 타입을 명시하지 않고 타입 파라미터로 대체 했다가 실제 클래스가 사용될 때 구체적인 타입을 지정하여 타입 변환을 최소화시킴으로서 프로그램 성능을 향상 시킬 수 있고 컴파일 시에 미리 타입을 강하게 체크해서 에러를 사전에 방지 하기 위한 방법


## 연결 리스트
- 단일 연결 리스트
- 원형 연결 리스트
- 이중 연결 리스트

### 선형 리스트(linear list)
- 각 데이터가 배열과 같이 연속되는 기억장소에 순차적으로 저장되는 자료 구조
- 1차원 배열과 비슷한 구조이지만, 원소의 개수가 유동적
- 원소를 나열한 순서가 원소들의 순서가 됨
- 원소들의 논리적인 순서와 메모리에 저장하는 물리적인 순서가 같은 구조로 되어 있음
- 순차 자료구조에는 원소들이 순서대로 연속 저장되어 있기 때문에 시작위치와 원소의 길이를 알면 특정 원소의 위치를 알 수 있음

## 사진

- 리스트에서 처리할 수 있는 연산
  - 길이 : 리스트의 길이를 구하는 연산
  - 접근 : 리스트의 내용을 조사하거나 변경하기 위해 위치를 찾는 연산
  - 검색 : 리스트의 노드들 중에서 필요한 노드 (i번째)를 찾는 연산
  - 저장 : i번째에 노드에 새로운 값을 기억시키는 연산
  - 삽입 : 리스트에 새로운 노드를 삽입시키는 연산
  - 삭제 : 리스테엇 노드를 제거하는 연산
  - 복사 : 리스트의 전체 또는 일부를 복사하여 새로운 노드(리스트)를 만드는 연산
  - 정렬 : 어떤 기준으로 리스트를 정렬(오름차순/내림차순)하는 연산
  - 병렬 : 둘 또는 그 이상의 리스트를 하나의 리스트로 합치는 연산
  - 분리 : 한 리스트를 둘 또는 그 이상의 리스트로 나누는 연산

- 선형 리스트의 특징
  - 기억 장소를 최대로 이용할 수 있는 구조이지만
  - 기억 장소에 저장되어 있는 정보들의 삽입, 삭제, 교환 등의 변화 시에는 복잡한 처리 필요
    - 삽입 및 삭제 후에는 리스트를 다시 정리하여 전체 리스트의 순서를 유지하는 작업 필요 
    - 자료 이동이 많음
  - 따라서, 항목 이동에 관련된 수행 시간을 줄이기 위해 순서리스트를 비순차적으로 표현하는 것이 필요 (연결 리스트 : linked list)
- 선형 리스트에 노드 삽입
  - 3번에 새로운 노드를 삽입 시
  - 세 번 이동하여 3을 비워둔 상태에서 새로운 노드 삽입

## 사진

- 선형 리스트의 단점
  - 데이터를 중간에 삽입하거나 중간 데이터를 삭제할 경우 많은 양의 데이터 이동 발생
  - 특히 데이터가 많을 경우 이동해야 하는 데이터 수가 더 많아짐
  - 또한, 크기가 다양한 여러 개의 선형 리스트들을 조작할 때 각각의 리스트에 대해 최대 크기를 가진 배열을 처음부터 준비해 두어야 하므로 기억 장소 낭비
  -  임의의 위치에 데이터를 삽입하거나 삭제가 용이하고 기억 장소를 낭비하지 않으며 삭제와 삽입 연산에 소요되는 시간을 절약하기 위한 새로운 형태의 선형 리스트(__단일 연결 리스트 (singly linked list)__) 필요

### 단일 연결 리스트 (singly linked list)
- 데이터를 연결(linked) 형태로 표현
- 리스트 내의 각 항목들이 순차적으로 저장될 필요 없이 기억 장소 내 어디든 저장되어 있어도 됨
- 다음 항목을 찾기 위해 각 항목들은 다음 항목을 가리키는 포인터를 갖고 있음
- 이 포인터를 링크(link)라고 부름

## 사진

- 단일 연결 리스트 기억 장소 내의 표현
  - 리스트 각 항목은 기억 장소의 순서대로 위치하지 않는다.
  - 링크라는 필드를 이용하여 리스트 원소들의 순서를 나타냄 
  - 리스트 끝에는 더 이상 원소가 없다는 것을 나타내기 위하여 마지막 원소의 링크 필드에 NULL(역슬래시)로 표시

## 사진
## 사진

- 단일 연결 리스트의 기본 연산
  - 노드 생성
  - 노드 삽입
  - 노드 삭제

- 단일 연결 리스트의 노드 생성1
  - 가용 기억 공간 중에서 리스트에 연결할 수 있도록 하나의 노드를 획득
  - 그 노드의 주소를 새로운 포인터에게 부여
  - HEAD 포인터가 새로 생성된 노드를 가리키게 함
  - 노드에 데이터 저장


- 단일 연결 리스트의 노드 생성2
  - 리스트에 노드가 하나도 없을 때 새로운 노드 1개를 삽입하는 경우
  - 새로운 노드를 얻어와서
  - HEAD가 새로운 노드를 가리키게 하고
  - 새로운 노드의 링크를 NULL로 설정

## 사진

- 단일 연결 리스트의 노드 생성3
  - 2개의 노드를 생성한 후
  - 첫 번째 노드에 데이터 A를 저장하고
  - 두 번째 노드에 데이터 B 저장

## 사진

- 단일 연결 리스트의 노드 삽입
  - 노드1과 노드2 사이에 새로운 노드를 삽입할 경우
  - 노드1이 새로운 노드를 가리키고
  - 새로운 노드가 노드2를 가리키게 함

## 사진

- 단일 연결 리스트의 노드 삽입의 경우
  - 리스트 맨 처음에 노드 삽입
    - 새로운 노드 얻어와서
    - 새로운 노드가 두 번째 노드를 가리키고
    - HEAD가 새 노드를 가리키게 함

## 사진

  - 리스트 맨 마지막에 노드 삽입
    - 새로운 노드를 얻어와서
    - 마지막 노드가 새로운 노드를 가리키고
    - 새로운 노드의 링크로 NULL값을 갖게 함

## 사진

  - 임의의 노드 X 다음에 삽입
    - 새로운 노드를 얻어와서
    - 새로운 노드가 임의의 노드 X 다음 노드를 가리키고
    - 임의의 노드 X가 새로운 노드를 가리키게 함

## 사진

- 단일 연결 리스트의 노드 삭제
  - 맨 처음 노드 삭제
    - 먼저 노드의 유무 확인 : 삭제할 노드가 없으면 언더플로우 발생
    - 삭제할 노드의 데이터는 저장해 놓고, 주소는 유 용공간에 추가

## 사진

  - 마지막 노드 삭제
    - 마지막 노드를 찾아서 삭제
    - 마지막 이전 노드의 링크를 NULL로 설정

## 사진

  - 중간 노드 삭제
    - 삭제하려는 노드 X 노드 앞의 노드 링크에 X 노드가 갖고 있는 링크 값을 저장하면 자연히 X노드는 리스트에서 삭제

## 사진