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

## 자료/객체 비대칭

## 디미터 법칙

## 자료 전달 객체

