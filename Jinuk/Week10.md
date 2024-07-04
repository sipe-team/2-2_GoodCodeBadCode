# 11. 주석: 유지보수와 변경의 정확성을 높이는 주석 작성 방법

- 내용이 낡은 주석
  - 주석과 코드가 일치하지 않는 사례
  - 구현을 변경할 때 주석도 함께 변경하는 것이 좋음
  - 유의할 점
    - 주석은 실제 코드가 아니다
    - 로직의 동작을 설명하는 주석은 낡기 쉽다

- 주석 때문에 이름을 대충 짓는 예
  - 메서드 이름을 지을 때, 명시적으로 지어서 주석이 필요 없게 하는 것이 제일 좋음
  - 낡은 주석 가능성 다운

- 의도와 사양 변경 시 주의 사항을 읽는 이에게 전달하기
  - 주석이 담아야 하는 내용
    - 로직이 움직이는 의도
    - 안전하게 변경하려면 주의해야 하는 것

- 주석 규칙
  - 로직을 변경할 때는 반드시 주석도 함께 변경
  - 로직의 내용을 단순히 설명하는 주석은 달지 않는다
  - 가독성이 나쁜 로직에 설명을 추가하는 주석은 달지 않고, 가독성을 높이는 방향으로 간다
  - 로직의 의도와 사양을 변경할 때 주의할 점을 주석으로 단다

- 문서 주석
  - Javadoc, Documentation comments, YARD 등 자체 코드별 문서 주석 기능도 있음
  - 이를 통해 API 문서 자동 생성 가능