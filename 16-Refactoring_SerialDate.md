## 16. SerialDate 리팩토링

#### 16.1 돌려보자
- 단위 테스트가 실행하는 코드와 실행하지 않는 코드를 조사. (현재 50% 정도)
- 먼저, 클래스를 철저히 이해하고 리팩토링 하려면 독자적인 단위 테스트 케이스를 구현하자. (92%)

#### 16.2 고쳐보자
- import 문을 `java.text.*`과  `java.util.*` 형태로 줄인다
- Javadoc 주석은 HTML 형태를 사용. `<ul> <li>` 따위를 `<pre>`로 수정
- SerialDate를 DayDate로 이름 변경
- MonthConstants 클래스는 달을 정의하는 static final 상수 모음에 불과 하므로 enum으로 정의하는 것이 마땅하다.
	- 달을 int로 받던 메소드는 이제 Month로 받는다. -> Validate 함수가 필요없다.
- createInstance를 makeDate라는 좀 더 서술적인 이름으로 바꾼다.
- 정리하자.
	1. 처음에 나오는 주석은 너무 오래되었다. 간단히 고치고 개선
	2. enum을 모두 독자적인 원시 파일로 이동
	3. 정적 변수와 메소드를 DateUtil이라는 새 클래스로 옮겼다.
	4. 일부 추상메소드를 DayDate 클래스로 끌어올렸다.
	5. Month.make를 Month.fromInt
	6. 새 메서드를 생성해 중복을 없앴다.
	7. 숫자 1을 없애고, Month.JANUARY.toInt()로 적절히 변경

#### 결론
- 버그 몇개를 고치고, 코드 크기가 줄고 명확해졌다.
