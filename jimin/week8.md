## 9.1 데드 코드
* 데드 코드: 절대로 실행되지 않는 조건 내부에 있는 코드

데드 코드는 발견하는 즉시 제거하는 것이 좋고, IDE의 정적 분석 도구에 데드코드 식별하는 기능이 있으니 활용하는 것도 좋다.

## 9.2 YAGNI 원칙
* YAGNI: You Aren't Gonna Need It

소프트웨어에 대한 요구는 매일 변화하므로, 미리 예측해서 코드를 작성하더라도 대부분 맞지 않다. 따라서 지금 필요 없다면 굳이 만들어두지 말자

## 9.3 매직 넘버 
* 매직 넘버: 의미를 알기 힘든 숫자

상수를 사용해 매직 넘버를 사용하지 않도록 하자.

## 9.4 문자열 자료형에 대한 집착

```java
String title = "어쩌구,저쩌구,104";
```
위와 같이 `split` 메서드를 사용해 String 변수에 넣지말고, 의미가 다른 값은 각각 다른 변수에 저장하는 것이 좋다.

## 9.5 전역 변수
* 전역 변수: 모든 곳에서 접근할 수 있는 변수

자바에서 `public static`선언하면 모든 곳에서 접근할 수 있는데, 이렇게 선언한다면 다음과 같은 문제가 있다.
1. 어디에서 어떤 시점에 값을 변경했는지 파악하기 어려움
2. 전역 변수를 참조하고 있는 로직 변경 시, 해당 변수를 참조하는 다른 로직에서 버그가 발생하는지 검토 필요
3. 동기화가 필요하다면, 락을 얻기 위해 대기하는 시간이 길어질 수 있고 동기화에 문제가 생긴다면 데드락 상태에 빠질 수 있음
  * 참고로 전역 변수 뿐만 아니라 데이터 클래스도 성능상 문제 발생할 수 있음

따라서 여러 곳에서 참조하는 전역 변수나 거대 데이터 클래스를 사용할 때 주의가 필요하다. 되도록이면 사용 스코프를 작게 가져가도록 해야한다.

## 9.6 null 문제
NPE에 대비해 방어 로직을 넣어야 하는데, 이는 가독성이 떨어지고 null 체킹을 하지 않는다면 바로 버그가 생긴다.
`null`을 입력되지 않은 상태로 표현하게 된다면 큰 손실을 불러일으킬 수 있다.

**null을 리턴/전달하지 말기**

```java
Equipment EMPTY = new Equipment("장비 없음", 0, 0, 0);
```
null에 의미를 두기보다, 위와 같이 empty 값을 정의해 사용하자.

**null 안전**
아예 언어에서 null 안전 자료형을 지원한다면, 이를 적극적으로 사용하는 것이 좋다. (ex. 코틀린)

## 9.7 예외를 catch 하고 무시하는 코드
try-catch 로 예외를 잡고 무시하지 말자. catch로 잡았다면 최소한 로그로 남기고 상위 레이어의 클래스로 오류를 통지하는 것이 좋다.

## 9.8 설계 질서를 파괴하는 메타 프로그래밍 
* 메타 프로그래밍: 프로그램 실행 중, 해당 프로그램 구조 자체를 제어하는 프로그래밍 (ex. 리플렉션 API)

메타 프로그래밍을 사용하면 값을 의미로 변경할 수 있으므로 잘못된 상태로부터 클래스를 보호하는 설계가 의미 없어진다. 또한  단순 String 값을 넘겨 클래스를 가져오므로, 클래스 명 변경 추적이 힘들다.

따라서 메타 프로그래밍을 사용하고 싶다면 시스템 분석 용도로 한정하거나 아주 작은 범위에서만 활용해야 한다.

## 9.9 기술 중심 패키징
UseCase, Entities, ValueObjects 와 같이 기술 중심으로 패키징 하는 것보다 비즈니스 개념을 기준으로 폴더를 구분하는 것이 좋다.

## 9.10 샘플 코드 복사해서 붙여넣기
그대로 복붙하지 말고, 클래스 구조를 잘 설계해서 사용하자.

## 9.11 은 탄환 
'어떤 문제를 해결하는 비장의 무기' 는 SW 개발에는 없다. 문제와 목적에 따라 적절한 기술을 잘 선택하도록 하자.