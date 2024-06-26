# 9장. 설계의 건전성을 해치는 여러 악마

## 데드 코드

**데드 코드(dead code)** 는 **절대로 실행되지 않는 조건 내부에 있는 코드**로, 도달 불가능한 코드(unreachable code)라고도 부릅니다.

```java
int getTotalScore (int score) {
    if (score > 100) {
        totalScore += 100;
    }
    if (score == 200) { // dead code
        totalScore += 400;
    }
}
```

1. 코드의 가독성이 떨어진다.
2. 버그가 될 가능성이 있다.

그러므로 데드 코드는 **발견하는 즉시 제거**하는 것이 좋습니다.

## YAGNI 원칙

**YAGNI 원칙**은 `You Aren't Gonna Need It.`의 약자로, **지금 필요 없는 기능을 만들지 말라**는 원칙입니다. 개발을 할 때 미래를 예측하고 미리 만들어 두는 경우가 있는데, 예측에 들어맞지 않는 로직은 데드 코드가 됩니다. 또한, 예측해서 코드를 미리 작성해 두어도 결국 시간 낭비입니다. 그러므로 지금 필요한 기능을 최대한 간단한 형태로 만드는 것이 가독성과 유지 보수성을 높입니다.

## 매직 넘버

**매직 넘버**는 로직 내부에 직접 작성되어 있어서, **의미를 알기 힘든 숫자**를 의미합니다.

```java
int getScore() {
    return 20;
}


int getBonus() {
    return 20 * 2;
}
```

매직 넘버는 구현자 본인만 의도를 이해할 수 있으며 가독성을 떨어트리므로, 매직 넘버 대신 **상수**를 활용합시다.

```java
private static final int DEFAULT_SCORE = 20;


int getScore() {
    return DEFAULT_SCORE;
}


int getBonus() {
    return DEFAULT_SCORE * 2;
}
```

## 문자열 자료형에 대한 집착

다음은 하나의 String 변수에 여러 값을 쉼표로 구분해서 저장하고 있습니다.

```java
// game name, default score
String game = "name,20";
```

이 경우 split 메서드 등을 사용해서 값을 꺼내 값을 꺼내 써야 합니다. 의미가 다른 여러 개 값을 하나의 String 변수에 무리하게 넣으면, 의미를 알기 어려워져 가독성이 크게 저하됩니다.

의미가 다른 값은 각각의 다른 변수에 저장하는 것이 좋습니다.

## 전역 변수

**전역 변수**는 **모든 곳에서 접근할 수 있는 변수**입니다.

여러 로직에서 전역 변수를 참고하고 값을 변경하면, **어디에서 어떤 시점에 값을 변경했는지 파악하기 대단히 힘듭니다.** 또한 전역 변수를 참고하고 있는 로직을 변경해야 할 때, **해당 변수를 참조하는 다른 로직에서 버그가 발생하는지도 검토**해야 합니다.

동기화가 필요한 경우에도 문제가 발생합니다. 동기화는 **제대로 설계하지 않으면 락을 얻기 위해 대기하는 시간이 길어져 퍼포먼스를 크게 떨어뜨립니다.** 그리고 동기화에 문제가 생기면 **데드락 상태에 빠질 수 있습니다.**

이러한 문제를 막기 위해서는 **영향 범위가 가능한 한 되도록 좁게 설계**해야 합니다. 그리고 만약 전역 변수를 사용하고 싶다면, **정말로 필요한지** 꼭 검토해 보기 바랍니다.

## null 문제

다음과 같은 코드는 `NullPointException`이 발생할 수 있습니다.

```java
class Member {
    private Equipment head;
    private Equipment body;
    private int defence;

    int getTotalDefence() {
        return defence + head.defence + body.defence;    }
}
```

NPE가 발생하지 않도록 하기 위해서는 null 체크를 해야 합니다. 그러나 null 체크 코드가 너무 많아지면 **가독성이 떨어지고** 실수로 null 체크를 하지 않는 곳이 생기면 곧바로 버그가 될 것 입니다.

null 체크를 하지 않으려면, **애초에 null을 다루지 않게 만들어야 합니다.** 구체적으로는 다음을 만족하는 설계입니다.

- null을 리턴하지 않는 설계
- null을 전달하지 않는 설계

**null에 의한 오류가 아예 발생하지 않게 만드는 구조**를 **null 안전**이라고 합니다. null 안전을 구현하기 위한 기능으로 **null 안전 자료형**이 있습니다. 이 자료형은 null을 아예 저장할 수 없게 만드는 자료형입니다.

## 예외를 catch 하고서 무시하는 코드

다음 코드는 어떤 원인으로든 문제가 생기면 예외를 던지도록 구현되어 있습니다.

```java
try {
   file.get(fileName);
}
catch (Exception e) {
}
```
이러한 코드는 오류가 나도 **오류를 탐지할 방법이 없습니다.**
예외를 catch 하고서 무시하고 있기에 어느 시점에 어떤 코드에서 문제가 발생했는지 찾기 어렵습니다.
문제가 발생할 때는 즉시 알려주어 잚롯된 상태를 막는 것이 좋은 구조입니다.

## 설계 질서를 파괴하는 메타 프로그래밍
**메타 프로그래밍**은 **프로그래밍 실행 중에 해당 프로그램 구조 자체를 제어하는 프로그래밍**입니다.
자바에서는 리플랙션 API를 사용하여, 메타 프로그래밍을 활용해 클래스 구조를 읽고 씁니다.
그러나 리플렉션을 사용하면 다음과 같은 문제가 있습니다.

1. final로 지정한 변수의 값 변경이 가능하다.
2. private로 외부에서 접근하지 못하게 만든 변수에도 접근할 수 있다.

그러므로 메타 프로그래밍을 사용하고 싶다면 시스템 분석 용도로 한정하거나 아주 작은 범위에서만 활용하는 등 리스크를 최소화해야 합니다.

## 기술 중심 패키징

**기술 중심 패키징**은 **구조에 따라 폴더와 패키지를 나누는 것**입니다.
예를 들면, MVC 아키텍처 구조를 그대로 가져와 `models, views, controllers`로 폴더를 구성하는 것입니다.
이렇게 하면, 비즈니스 클래스의 관련성을 알기 매우 힘들어집니다.
그러므로 **비즈니스 클래스는 비즈니스 개념을 기준으로 폴더를 구분**하는 것이 좋습니다.

## 샘플 코드 복사해서 붙여넣기

샘플 코드를 그대로 복사하고 붙여 넣어 구현하면 **설계 측면에서 좋지 않은 구조가 되기 쉽습니다.**
샘플 코드는 어디까지나 참고만 하고, 클래스 구조를 잘 설계해서 사용합시다.