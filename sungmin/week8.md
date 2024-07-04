# 9장 설계의 건전성을 해치는 여러 악마

## 9.1 데드 코드

- 절대로 실행되지 않는 조건 내부에 있는 코드를 데드 코드 또는 도달 불가능한 코드라고 부른다.
- 데드 코드는 코드의 가독성을 떨어트린다.
- 데드 코드는 즉시 제거하는 것이 좋다.

## 9.2 YAGNI원칙

- 실제 개발을 할 때 미래를 예측하고, 미리 만들어 두는 경우가 있다.
  - 미래를 예측하고 미리 만들어 둔 코드는 추후에 사용하는 경우도 있지만, 사용하지 않게 되는 경우가 많다.
  - 이런 코드는 추후에 버그의 원인이 되기도 한다.
- YAGNI는 'You Aren't Gonna Need It.'의 약자이며, '지금 필요 없는 기능을 만들지 말라' 라는 의미이다.
- 예측해서 코드를 미리 작성해 두는 것은 시간 낭비이며, 지금 필요한 기능을 최대한 간단한 형태로 만다는 것이 가독성과 유지 보수성을 높인다.

## 9.3 매직넘버

- 설명 없는 숫자는 개발자를 혼란스럽게 만든다.
- 의미를 알기 힘든 숫자를 매직 넘버라고 하며, 매직 넘버는 구현자 본인만 의도를 이해할 수 있다.
- 또한 매직 넘버는 동알한 값이 여러 위치에 등장하여 중복 코드를 만들어내며, 여러 곳에서 사용한 동일한 의미를 가진 매직 넘버를 수정하다보면 버그가 될 수 있다.
- 매직 넘버는 상수로 등록해서 관리하는 것이 좋다.

## 9.5 전역 변수

- 모든 곳에서 접근 할 수 있는 변수를 전역 변수라고 한다.
- 자바 언어 사양에는 전역 변수가 없다.
  - 하지만 아래와 같이 변수를 public static으로 선언하면 모든 곳에서 접근이 가능하다.

  ``` java
  public OrderManager {
    public static int currentOrderId;
  }
  ```

- 전역 변수는 모든 곳에서 참조 할 수 있고 조작도 할 수 있는 변수이지만 잘못 사용하면 버그가 발생 할 수 있다.
  - 여러 로직에서 전역 변수를 참고하고 변경한다면 어떤 시점에서 값이 변경했는지 파악하기 힘들다.

## 9.6 null 문제

- null이란 초기화하지 않은 메모리영역에서 값을 읽으려면 문제가 발생하며, 이를 피하기 위해 null이 발명 되었다.
- null은 메모리 접근과 관련된 문제를 방지하기 위한 최소한의 구조로서 null자체가 `잘못된 처리`를 의미한다.

### 9.6.1 null을 리턴/전달하지 말기

- null을 체크 하지 않으려면, 애초에 null을 다루지 않게 만들어야 한다.
- null을 리턱하지 않는 설계
- null을 전달하지 않는 설계

### 9.6.2 null안전

- null 안전이란 null에 의한 오류가 아예 발생하지 않게 만드는 구조이다.
- null 안전을 구현하기 위한 기능으로 null 안전 자료형이 있다.
- null 안전 자료형은 null을 아예 저장할 수 없게 만드는 자료형이며, 코틀린은 기본적으로 모든 자료형에 null 안전 자료형을 사용한다.

## 9.7 예외를 catch하고서 무시하는 코드

``` java
try {
  cartItem.add(product);
} catch (Exception e) {

}
```

- 다음과 같은 코드는 try-catch로 예외를 catch해놓고도 별다른 처리를 하지 않고 있다.
- 이렇게 예외를 무시하는 경우 에러 추적이 어려울 뿐더러 서비스에 버그가 발생하게 된다.
- catch 구문에서는 최소한 로그를 기록하고, 상위 레이어 클래스로 오류를 통지하는 것이 좋다.

``` java
try {
  cartItem.add(product);
} catch (Exception e) {
  log.error("cart add error : " + e)
  throw e;
}
```

## 9.8 설계 질서를 파괴하는 메타 프로그래밍

- 프로그램 실해 중 해당 프로그램 구조 자체를 제어하는 프로그래밍을 메타 프로그래밍이라고 부른다.
- 자바에서 메타 프로그래밍을 활용해 클래스 구조를 읽고 쓸 때는 리플렉션 API를 사용한다.
- 자바로 대표되는 정적 자료형 언어는 정적 분석으로 정확한 코드 분석이 가능하다는 장점이 있다.
  - 하지만 메타 프로그래밍은 이러한 장점조차 무너뜨린다.
- 메타 프로그래밍을 사용하면, 뭔가 특별한 능력을 배운것 같아 기분이 좋을 수 있지만, 단점을 이해하지 못하고 사용하면 유지 보수와 변경이 정말 힘들어진다.

## 9.9 기술 중심 패키징

- 구조에 따라 폴더와 패키지를 나는 것을 기술 중심 패키징이라고 한다.
- 레일즈나 장고, 스프링 같은 웹 프레임워크에서 MVC 아키텍처를 채택하고 있다.
- 비즈니스 개념을 나타내는 클래스를 비즈니스 클래스라고 부르면, 비즈니스 클래스는 기술 중심 패키징에 따라 폴더를 구분하면 관련성을 알기 매우 힘들다.
  - **비즈니스 클래스는 관련된 비즈니스 개념을 기준으로 폴더를 구분하는 것이 좋다.**

## 9.10 샘플 코드 복사해서 붙여넣기

- 공식 홈페이지나 기술 커뮤니티 등에 있는 샘플 코드는 어디까지나 참고만하고, 클래스 구조를 잘 설계해서 사용핻야한다.