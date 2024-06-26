# 10장 이름 설계: 구조를 파악할 수 있는 이름

## 10.1 악마를 불러들이는 이름

- 강한 결합을 해소하고, 결합이 느슨하고 응집도가 높은 구조로 만들려면 관심사 분리를 할 수 있어야 한다.
- 관심사 분리는 관심사에 따 분리한다는 소프트웨어 공학 개념이다.
- 관심사에 따라 분리하면, 결합도를 낮추고 응집도를 높일 수 있다.
- 관심사별로 클래스의 결합도를 낮추고 응집도를 높이면 관련된 사양이 변경되었을 때 관련 클래스만 확인하면 되어 개발 생상성이 향상 된다.
- 이름이 너무 포괄적이라서 목적이 불분명한 클래스를 **목적 불명 객체**라고 하고, 이 객체는 규모가 커지기 쉽다.
- 프로그래밍에서 이름은 가독성을 높이는 역할만 하는 것이 아닌 관심사 분리를 생각하고, 비즈니스 목적에 맞게 이름을 붙이는 것이 결합이 느슨하고 응집도가 높은 구조를 만드는데 굉장히 중요한 역할을 한다.
- 비즈니스 목적에 특화하여 이름을 붙이면 다음과 같은 효과가 생긴다
  - 이름과 관계없는 로직을 배제하기 쉬워짐
  - 클래스가 작아짐
  - 관계된 클래스 개수가 적으므로, 결합도가 낮아짐
  - 관계된 클래스 개수가 적으므로, 사양 변경 시 생각해야하는 영향 범위가 좁음
  - 목적에 특화된 이름을 갖고 있으므로, 어떤 부분을 변경해야 할 때 쉽게 찾을 수 있음
  - 개발 생산성이 향상됨
- 구체적인 목적을 알 수 있게, 목적을 기반으로 이름을 짓는 것이 좋다.
- 비즈니스 목적에 특화된 이름을 만들기 위해서는 어떤 비즈니스를 하는지 모두 파악해야하며, 이를 위해 SW가 추구하는 목적과 내용을 분석해야한다.

## 10.3 이름 설계 시 주의 사항

- 이름에 여러 의미가 섞이면 이름이 의미 하는 바를 다시 검토 해야며, 이후 이름을 변경하거나, 클래스를 나누어서 설계 해야한다.
- 팀원들과 대화 시에 등장하지만 실제 구현이 안되어 있는 경우, 추후 다른 사람이 해당 로직을 찾을 때 굉장히 힘이든다. 따라서 대화 시에 사용하는 클래스 이름을 신경 써야하고 이름 기반으로 메서드와 클래스를 설계해야한다.

## 10.4 의미를 알 수 없는 이름

- 이름을 설계 할 때는 `tmp`와 같은 이름을 사용하지 않고 목적이 무엇인지, 어떤 의미로 사용되는지 명확하게 선언해야한다.
- 기술 중심으로 이름을 설계 하면 `changeIntValue01`과 같이 어떤 의도인지 알 수 없다. 따라서 비즈니스 목적을 나타내는 이름에 적합한지를 체크 해야한다.
- 메서드 이름을 설계할 때 로직 구조를 그대로 나타내는 이름이 아닌 의도와 목적을 쉽게 이해하도록 이름을 붙여야 한다.
- 이름을 설계 할 떄는 의도에 맞게 메서드와 클래스 이름을 설계해야한다.

## 10.5 구조에 악영향을 미치는 이름

- 클래스 이름을 설계할 때는 `~Info` 또는 `~Data`와 같이 데이터만 갖는 클래스처럼 이름을 피하는것이 좋다.
- 이름을 설계 할 때는 어떤 컨텍스트가 둘러싸고 있는지 분석하여 이를 기반으로 각 컨텍스트 별로 클래스 이름을 설계해야한다.
- 클래스와 메서드 이름에 번호를 붙여 만드는 것을 `일련번호 명명`이라고 한다.
- 일련번호 명명을 사용할 때는 조직 차원에서 충분히 논의를 하고 대처 할 수 있어야한다.

## 10.6 이름을 봤을 떄, 위치가 부자연스러운 클래스

- 동사 + 목적어 형태의 메서드 이름은 주의 해서 사용해야한다.
- 동사 + 목적어로 이루어진 이름은 관계없는 책무를 가진 메서드일 가능성이 있다.
- 관심사가 다른 메서드가 섞이지 못하게 막으려면 되도록 메서드의 이름을 동사 하나로 구성되도록 설계한는 것이 좋다.
- boolean 자료형의 메서드를 추가할때는 `is~` 형태로 설계하는것이 좋다2

## 10.7 이름 축약

- 긴 이름이 싫어서 이름을 축약하는 경우가 있는데 이름 축약을 잘못하게 되면 무엇을 하는 지 이해하기 어렵다.
