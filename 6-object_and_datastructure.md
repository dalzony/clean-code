# 객체와 자료구조

오타주의..

## 자료 추상화

(1)
```java
public class Point {
	public double x;
	public double y;
}
```

(2)
```java
public interface Point {
	double getX();
	double getY();
	void setCartesian(double x, double y);
	double getR();
	double getTheta();
	void setPolar(double r, double theta);
}
```

(3)

```java
public interface Vehicle {
	double getFuelTankCapacityInGallons();
	double getGallonOfGasoline();
}
```

(4)

```java
public interface Vehicle {
	double getPercentFuelRemaining();
}
```

* 구현을 외부로 노출하면 안된다. (1)보다 (2)가 더 좋음
  - 단지 (1)을 private하게 하는 것이 중요한게 아님, 추상화가 필요 --> interface 사용
* 정보가 어디서 오는지 드러나면 안된다 (3)보다 (4)가 더 좋음


## 자료/객체 비대칭

(1)~(4) : 객체와 자료구조 사이의 벌어진 차이

책을 봅시다...(todo: 코드 옮기기)

1. `객체`는 추상화 뒤로 `자료`를 숨긴 채 자료를 다루는 `함수`만 공개
2. `자료구조`는 `자료`를 그대로 공개하며 별다른 `함수`는 제공하지 않음

객체가 항상 좋은 것이 아니라, 절차적인 코드가 적합한 상황에는 사용하자.

## 디미터 법칙

[ Remind .. ]

* 객체 : 자료를 숨기고 함수를 공개--> 조회함수로 내부를 공개하면 안된다.

[ 디미터 법칙 ]

"클래스 C의 메서드 f는 다음과 같은 객체의 메서드만 호출해야함"

* 클래스 C
* f가 생성한 객체
* f 인수로 넘어온 객체
* C 인스턴스 변수에 저장된 객체

=> 위 객체에서 혀용된 메서드가 반환하는 객체의 메서드는 호출하면 안된다 (낯선사람 경계하고 친구하고만 놀으렴!)

### 기차 충돌

* 기차 충돌 예

```java
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
```

다음과 같이 고치는 것이 좋다.

```java
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scrtchDir.getAbsolutePath();
```

### 잡종구조
### 구조체 감추기

## 자료 전달 객체

* 자료구조체 : 공개변수만 있고 함수가 없는 클래스 = `자료전달객체`(Data Transfer Object, DTO)
  - db통신, 소켓 메시지분석등을 할 때 유욕한 구조체
  - 데이터페이스에 저장된, 가공되지 않은 정보.
  - bean 구조가 일반적인 형태 (private변수를 조회/설정 함수로 조작)
  
* 활성 레코드 DTO의 특수한 형태.
  - 공개 변수 있거나, 비공개 변수에 조회/설정 함수가 있는 자구조.
  - save와 find까지 제공
  - 데이터베이스 테이블이나 다른 소스에서 자료를 직접 변환한 결과.
  - 활성레코드에 비즈니스 규칙 메서드를 추가해서 객체처럼 쓰지 말것. -> 자료구조도 아니고 객체도 아닌 잡종이 되기 때문
  - "활성 레코드는 자료구조로 취급한다" & "비즈니스 로직을 담으면서 내부자료(주로 활성레코드의 인스턴스)를 숨기는 객체는 따로 생성"
  
## 결론

* 객체는 동작을 공개하고 자료는 숨긴다 : 새 객체 타입 추가는 쉽지만, 새 동작 추가는 어렵다.
* 자료구조는 동작없이 자료를 노출 : 기존 자료구조에 새 동작 추가는 쉽지만, 기존 함수에서 새 자료구조 추가는 어렵다.

둘중 상황에 맞게 객체를 쓰거나, 자료구조 with절차적 코드를 쓰면 된다.
