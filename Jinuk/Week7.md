# 8. 강한 결함: 복잡하게 얽혀서 풀 수 없는 구조

1. 결합도와 책무
   - 책무를 고려하지 않은 설계 예시
     - 로직의 위치에 일관성이 없음
     - 어떤 클래스는 편의를 위해 다른 클래스의 메서드를 무리하게 사용
   - 단일 책임 원칙
     - 클래스가 담당하는 책임은 하나로 제한해야 한다.
     - 책임을 대신 지는 클래스가 만들어지면, 다른 클래스가 제대로 성장할 수 없음
     - 유효성 검사와 관련된 책임을 모두 한 클래스 안에서 해결
     - 관심사에 따라 분리해서 독립되어 있는 구조 - 느슨한 결합
   - DRY 원칙
     - 반복을 피해라
     - 그러나 같은 로직, 비슷한 로직이라도 개념이 다르면 중복을 허용해야 함
     - 강한 결합 상태가 될 수 있고, 단일 책임 원칙이 깨질 수 있음

2. 다양한 강한 결합 사례와 대처 방법
   - 상속과 관련된 강한 결합
     - 슈퍼 클래스에 의존하게 되는 현상
       - 슈퍼클래스가 서브클래스를 신경쓰지 않고 변화하는 경우가 있어서, 문제가 발생하기 쉬움
     - 상속보다 컴포지션
       - 프라이빗한 인스턴스 변수로 갖고 사용하는 것
     - 상속을 사용하는 나쁜 일반화
       - 무리하게 일반화하려다 보면, 강한 결합이 생길 수 있음
     - 반드시 단일 책임 원칙을 염두에 두고 상속을 구현하여야 함
   - 인스턴스 변수별로 클래스 분할이 가능한 로직
     - 메서드와 인스턴스 변수간의 의존 관계까 일대일인 경우, 서로 다른 클래스로 분리하여 강결합 문제를 없앨 수 있음
     - 영향 스케치 그리기
   - 특별한 이유 없이 public 사용하지 않기
     - public으로 인해 강결합이 일어날 가능성이 커짐
     - 가시성을 적절하게 제어해 주는 것이 좋음
   - private 메서드가 너무 많다는 것은 책임이 너무 많다는 것
     - 규모가 커진 클래스에는 여러 메서드가 정의되지만, 그만큼 책임이 많아짐
   - 높은 응집도를 오해해서 생기는 강한 결합
     - 응집도가 높다는 개념을 두고, 관련이 깊은 로직을 한곳에 모았지만 강결합 구조를 만드는 현상
   - 스마트 UI
     - 화면 표시 담당 클래스 중 직접적인 관련이 없는 책무가 구현된 클래스
     - 서로 다른 클래스로 분할 필요
   - 거대 데이터 클래스
     - 데이터 클래스가 너무 커지는 경우
     - 전역 변수와 동일한 문제 발생 가능
   - 트랜잭션 스크립트 패턴
     - 메서드 내부에 일련의 처리가 하나씩 길게 작성되어 있는 구조
     - 데이터 클래스와 데이터 처리 클래스가 나누어져 있을 때 자주 발생
     - 응집도가 낮아지고 결합도 강해짐
   - 갓 클래스
     - 너무 많은 책임을 담당하는 로직이 난잡하게 섞여 있는 클래스
   - 대처 방법
     - 객체 지향 설계, 단일 책임 원칙에 따른 설계 필요