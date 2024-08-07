# 12장 메서드(함수): 좋은 클래스에는 좋은 메서드가 있다

## 12.1 반드시 현재 클래스의 인스턴스 사용하기

- 인스턴스 변수를 안전하게 조작하도록 매서드를 설계하면, 클래스 내부가 정상적인 상태인지 보장 할 수 있다.
- 메서드는 반드시 현재 클래스의 인스턴스 변수를 사용하도록 설계한다. -> 예외가 있긴 하지만 이것이 기본 원칙이다.

## 12.2 불변을 활용해서 예상할 수 있는 메서드 만들기

- 가변 인스턴스 변수을 변경하는 메서드는 의도하지 않게 다른 부분에 영향이 줄 수 있어 예상치 못한 동작이 발생할 수 있어 유지보수가 어려워 진다.

## 12.3 묻지 말고 명령하라

- 메서드를 호출하는 쪽에서눈 복잡한 처리를 하지 않는 것이 좋다.

## 12.4 커멘드 / 쿼리분리

- 메서드는 커맨드 또는 쿼리 중에 하나만 하도록 설계해야한다. -> CQS패턴
  - command : 상태를 변경하는 것
  - query : 상태를 리턴하는 것
  - modifier : 커맨드와 쿼리를 동시에 하는 것

## 12.5 매개변수

- 불변 매개변수로 만들기
  - 매개 변수를 변경하면 값의 의미가 바뀌어서 어떤 의미를 나타내는지 유추하기 어렵다.
  - 매개 변수에 final 수식자를 붙여서 불변으로 만들어야 한다.
  - 매개 변수를 변경하고 싶으면 불변 지역 변수를 만들고 이 값을 변경하는 형태로 구현한다.
- 플래그 매개변수 사용하지 않기
- null 전달하지 않기
  - null을 활용한 로직은 NPE가 발생할 가능성이 있고, null 체크를 해야하는 문제가 잇어서 로직이 복잡해지는 문제가 발생한다.
  - null에 의미를 부여하면 안된다.
- 출력 매개변수 사용하지 않기
  - 매개변수를 출력값으로 사용하면 가독성 저하의 원인이 된다.
- 매개변수는 최대한 적게 사용하기
  - 매개변수가 많다는 것은 해당 메서드가 여러가지 기능을 한다는 의미이다.
  - 메서드가 여러가지 기능을 하게 되면 로직이 복잡해지는 문제가 발생한다.

## 12.6 리턴 값
