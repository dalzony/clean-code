# 3. 함수

함수를 짧게, 읽기 쉽게 만들자.

39p ~ 65p
@jihyun.song

---------

## 작게 만들어라!

 * 함수는 짧으면 짧을수록 좋다. 
 * 함수는 20줄도 길다.
 * 블록과 들여쓰기를 잘 하고, 들여쓰기는 2단을 넘어서지 말자.

## 한 가지만 해라! (SRP, Single Responsibility Principle)

 * 함수는 한가지 기능만을 정의해야한다.
 * 추상화 수준을 잘 정의하자.
 * 현재 함수 이름에서, 다른 의미있는 이름으로 추출할 수 있으면, 추출하자.

 => 열심히 함수 정의를 쪼개자.

## 함수 당 추상화 수준은 하나로!

 * 한 함수 내 모든 문장의 추상화 수준을 동일시켜라.
 * 내려가기 규칙 : TO 문단을 읽듯이 프로그램이 읽히도록 해라.
 
 ```
 TO 설정 페이지와 해제 페이지를 포함하려면, 설정 페이지를 포함하고, 테스트 페이지 내용을 포함하고, 해제 페이지를 포함한다.
  TO 설정 페이지를 포함하려면, 슈트이면 슈트 설정 페이지를 포함한 후 일반 설정 페이지를 포함한다.
  TO 슈트 설정 페이지를 포함하려면, 부모 계층에서 "SuiteSetUp" 페이지를 찾아 include 문과 페이지 경로를 추가한다.
   .
   .
   .
 ```

 => 쪼개는 기준이 명확해져라

## Switch 문
 
 * Abstract Factory를 통해 switch문을 숨긴다.
 * case에 따른 행위에 대한 method가 있는 적절한 파생 클래스를 만들고, switch문에서는 case에 따른 클래스의 인스턴스를 반환한다.

 => 객체를 생성하는 코드에서 단 한번만 참아준다.

## 서술적인 이름을 사용하라!

 * "코드를 읽으면서 짐작했던 기능을 각 루틴이 그대로 수행한다면 깨끗한 코드라 불러도 되겠다"
 * 이름은 길어도 된다.
 * 모듈 내에서 함수 이름은 같ㅌ은 문구, 명사, 동사를 사용한다.

## 함수 인수

 * 인수 개수 0개는 무항, 1개는 단항, 2개는 이항, 3개는 삼항, 4개 이상은 다항이다.
 * 삼항 이상은 피하자.
 * 최선은 입력 인수가 없는 경우고, 차선은 입력 인수가 1개인 경우다.

 #### 많이 쓰는 단항 형식

  * 인수에게 질문을 던지는 경우

	  ```
	  boolean fileExist("TestFile")
	  ```

  * 인수를 변환하여 결과를 반환하는 경우
	
	  ```
	  InputStream fileOpen("TestFile")
	  ```

  * (드물게)출력 인수가 없는 이벤트 형식
	
	  ```
	  passwordAttemptFailedNtimes(int attempts)
	  ```
	
  => 이벤트는 코드에 드러나도록 이름과 문맥에 주의!

 #### 플래그 인수

  * 쓰지말자.
  * 한번에 여러가지 처리하는 것과 같다. ex) render(true)를 쓰느니 renderForSuite()를 만들자.
 
 #### 이항 함수

  * 최대한 단항함수를 쓰자
  * 짝이 있는 경우는 쓰기 좋다. ex) assertEquals(expected, actual)

 #### 삼항 함수

  * 이항함수보다 이해하기 어렵다. 신중히 고려하라.

 #### 인수 객체

  * 인수가 2-3개 필요하다면 독자적인 클래스 변수를 고민해보자.
  
	  ```
	  Circle makeCircle(double x, double y, double radius);
	  Circle makeCircle(Point center, double radius); // 조금 더 의미를 담을 수 있다.
	  ```

 #### 인수 목록

  * 가변인수가 동등하다면 List 형 인수 하나로 취급하자.
  
	  ```
	  public String format(String format, Object... args)
	  ```

 #### 동사와 키워드

  * 단항함수: 함수와 인수가 동사/명사 쌍으로 ex) wirte(name)
  * 함수 이름에 키워드 넣기
  
	  ```
	  assertEquals(expected, actual);
	  
	  assertExpectedEqualsActual(expected, actual); // 인수를 기억 할 필요가 없어진다.
	  ```

## 부수 효과를 일으키지 마라!

  * 함수에선 한가지 일만 하자. ex) 클래스 변수 수정, 인수 수정, 전역변수 수정 등등
  * 출력 인수
	
	  ```
	  appendFooter(s);
	  s.appendFooter(); # s에 Footer가 붙을 것이란게 더 명확하게 표현된다.
	  ```

## 명령과 조회를 분리하라!

  ```
  if (attributeExists("username")) {
    setAttribut("username", "unclebob")
  }
  ```

## 오류 코드보다 예외를 사용하라!

  * 오류 처리도 한가지 작업이다. 오류 처리하는 함수는 오류만 처리한다.
  * 오류코드를 정의해서 오류코드를 반환하지 말자.
  * Try/Catch 블록 뽑아내기
  
  ```
  public void delete(Page page) {
    try {
      deletePageAndAllReferences(page);
    } catch (Exception e) {
      logError(e);
    }
  }

  private void deletePageAndAllReferences(Page page) throws Exception {
    deletePage(page);
    registry.deleteReference(page.name);
    configKeys.deleteKey(page.name.makeKey());
  }

  private void logError(Exception e) {
    logger.log(e.getMessage())
  }
  ```

## 반복하지 마라!

  * 중복코드를 만들면 안된다.
  * 중복을 제외시키면, 오류 발생확률도 적어지고, 가독성도 높아진다.

## 구조적 프로그래밍

  * Edsger Dijkstra의 구조적 프로그래밍 원칙(에츠허르 데이크스트라)
  * 모든 함수와 함수 내 모든 블록에 entry와 exit는 단 하나씩이다.
  * 루프안에서 break나 continue를 사용해선 안되고 goto는 절대로 안된다.
  * 함수가 아주 클 때만 상당한 이익을 제공한다.
  * 함수를 작게 만든다면, return, break, continue를 여러 차례 사용해도 괜찮다.
  * goto는 큰 함수에서만 의미가 있으므로, 작은 함수에선 절대 기피해야한다.

## 함수를 어떻게 짜죠?

  * 단위 테스트 케이스를 만들어라.
  * 코드를 다듬고, 함수를 만들고, 이름을 바꾸고, 중복을 제거한다. 메서드를 줄이고 순서를 바꾼다. 전체 클래스를 쪼개기도 한다.
  * 단위 테스트를 항상 통과하게 한다.

## 결론
  
  * 모든 시스템은 프로그래머가 설계한 DSL로 만들어진다.
  * 함수는 DSL의 동사이며, 클래스는 명사이다.
  * 길이가 짧고, 이름이 좋고, 체계가 잡힌 함수가 나오길 바란다.
  * 시스템이라는 이야기를 쉽게 풀어나갈 수 있을 것이다.








