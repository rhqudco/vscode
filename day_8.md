# day_8 정리 (2021.11.10 수요일)

## 객체 배열
- 클래스를 통해 정의한 속성으로 배열을 만들 수 있다.
  
~~~java
package Class_Practice;

import java.util.Random;

class Student {
    int hakbun;
    int score;
}
public class Method06 {
    public static void main(String[] args) {
        Random rand = new Random();
        // 객체 배열(기본형 타입만 배열이 될 수 있는것은 아니다.)
        // 학생 객체 5개를 담을 수 있는 배열
        // 배열에 아직 객체는 들어있지 않다.
        // 객체를 담을 수 있는 메모리 공간만 확보
        Student[] sArray = new Student[5];

        // 첫번째 학생 == 배열의 0번 인덱스
        //sArray[0] = new Student();

        // 배열에는 첫 번째 학생의 객체가 만들어지게 됩니다.
        // System.out.println(Arrays.toString(sArray));
        // 객체 배열 첫 번째 학생의 주소가 출력됨.

        // 첫번째 학생은 배열의 0번 인덱스를 통해서 접근
        //System.out.printf("학번: %d, 성적: %d\n", sArray[0].hakbun, sArray[0].score);
        // sArray[0].hakbun sArray[0].score

        // 5명의 학생 정보를 담을 수 있도록 객체를 배열에 만듦.
        // 학번과 성적 입력
        for(int i = 0; i < 5; i++) {
            sArray[i] = new Student();
            sArray[i].hakbun = 1001+i;
            sArray[i].score = rand.nextInt(100)+1;
        }

        // 입력된 학번, 성적을 확인
        for(int i = 0; i < 5; i++) {
            System.out.println("학번 : " + sArray[i].hakbun + " 점수 : " + sArray[i].score);
        }
    }
}
~~~