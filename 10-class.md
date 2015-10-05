# 10. 클래스

클린 클래스를 다뤄보자. 자바 관례를 따른다.

@jihyun.song

---------

## 클래스 체계

다음과 같은 순으로 클래스를 정의하자. by 표준 자바 관례

 * 변수목록
	 * 정적 공개 상수 (public static)
	 * 정적 비공개 변수 (private static)
	 * 비공개 인스턴스 변수 (private)
	 * 공개 변수는 꼭 쓰지 말자
	 
 * 함수
    * 공개 함수 (public function)
    * 비공개 함수 (private function)는 호출되는 공개함수 바로 밑으로 순차적으로.   	

### 캡슐화 (encapsulation)
 변수와 utility성 함수는 공개하지 않는 편이 좋다. 그러나 숨기기 힘들다면 최대한 protected를 이용하자. 캡슐화를 풀어주는 거는 최후의 방법...
 
 
## 클래스는 작아야 한다.

클래스 생성 규칙은 무조건 작게 만들기.

함수와는 다르게 책임(RDD, Responsibility-Driven Design)을 센다.
 
클래스 이름에서, 모호한 단어를 빼고 if, and, or, but을 사용하지 않고 25단어 이내로 표현할 수 있게 만든다.

### 단일 책임 원칙 (SRP, Single Responsibility Principle)

클래스나 모듈을 변경할 이유가 단 하나여야만 한다는 원칙이다.

큰 클래스 몇 개가 아니라 작은 클래스 여럿으로 이뤄진 시스템이 더 바람직하며, 작은 클래스를 이루면 변경할 이유가 하나뿐이므로 작은 클래스들을 통해서 시스템을 구현하도록 한다.

"돌아가는 소프트웨어"보다 "깨끗하고 체계적인 소프트웨어"에 초점을 두자.


### 응집도 (Cohesion)

클래스는 인스턴스 변수 수가 작아야한다.

응집도가 높다 == 클래스에 속한 메소드와 변수가 서로 의존하며 논리적인 단위로 묶인다는 의미이다.

응집도는 최대한 높게 유지하자.

```
=> 하나의 클래스에서는 하나(n)의 인스턴스 변수를 최대한 이용하고 관련있는 메서드들이 뭉쳐있어야한다.
```


#### 응집도를 유지하면 작은 클래스 여럿이 나온다.

큰 함수를 작은 함수로 쪼개자

변수가 통일된다면, 해당 변수를 클래스 인스턴스 변수로 바꾸자.

코드는 책을 참고


### 변경하기 쉬운 클래스

책 참고

``` java
public class PrintPrimes {
    public static void main(String[] args) {
        final int M = 1000;
        final int RR = 50;
        final int CC = 4;
        final int WW = 10;
        final int ORDMAX = 30;
        int P[] = new int[M + 1];
        int PAGENUMBER;
        int PAGEOFFSET;
        int ROWOFFSET;
        int C;
        int J;
        int K;
        boolean JPRIME;
        int ORD;
        int SQUARE;
        int N;
        int MULT[] = new int[ORDMAX + 1];
        J = 1;
        K = 1;
        P[1] = 2;
        ORD = 2;
        SQUARE = 9;
        while (K < M) {
            do {
                J = J + 2;
                if (J == SQUARE) {
                    ORD = ORD + 1;
                    SQUARE = P[ORD] * P[ORD];
                    MULT[ORD - 1] = J;
                }
                N = 2;
                JPRIME = true;
                while (N < ORD && JPRIME) {
                    while (MULT[N] < J)
                        MULT[N] = MULT[N] + P[N] + P[N];
                    if (MULT[N] == J) JPRIME = false;
                    N = N + 1;
                }}
            while (!JPRIME) ;
            K = K + 1;
            P[K] = J;
            PAGENUMBER = 1;
            PAGEOFFSET = 1;
            
            while (PAGEOFFSET <= M) {
                System.out.println("The First " + M + " Prime Numbers --- Page " + PAGENUMBER);
                System.out.println("");
                for (ROWOFFSET = PAGEOFFSET; ROWOFFSET < PAGEOFFSET + RR;
                     ROWOFFSET++) {
                    for (C = 0; C < CC; C++)
                        if (ROWOFFSET + C * RR <= M) System.out.format("%10d", P[ROWOFFSET + C * RR]);
                    System.out.println("");
                }
                System.out.println("\f");
                PAGENUMBER = PAGENUMBER + 1;
                PAGEOFFSET = PAGEOFFSET + RR * CC;
            }
        }
    }
}

```

### 변경으로부터 격리

Concrete Class와 Abstract Class를 통해서 구현이 미치는 영향을 격리하자.

ex) Big Integer





