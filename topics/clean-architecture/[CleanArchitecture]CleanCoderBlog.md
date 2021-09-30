## 1. 관심사의 분리

- Hexagonal Architecture, Onion Architecture 등 시스템 아키텍처에 관한 아이디어들은 모두 “관심사의 분리”라는 동일한 목표를 가짐

  - 소프트웨어를 계층으로 나누어서 목표를 달성 → 비즈니스용 레이어 + 인터페이스용 레이어

  - 프레임워크, UI, 데이터베이스, 외부 기관과 무관

    - Oracle DB를 Mongo로 쉽게 교체할 수 있어야 한다는 말

  - 비즈니스 규칙을 독립적으로 테스트할 수 있음

    - UI, 데이터베이스 등이 없어도 테스트할 수 있어야 함



## 2. 종속성 규칙

- 클린 아키텍처가 작동하는 우선 규칙은 “종속성 규칙”

  - 내부 서클의 어떤 것도 외부 서클의 무언가에 대해 전혀 알 수 없음.

    - 바깥쪽 원에 선언된 함수,클래스,변수 등은 안쪽 원의 코드에서 언급되어서는 안됨

- 네 가지 계층을 제시

  - Entitiy

    - Enterprise wide business rules

    - 일반적이고 가장 높은 수준의 규칙

  - Use case

    - application specific business rules

    - 응용프로그램별 비즈니스 규칙을 캡슐화하고 구현

  - Apdapter

    - 외부 형식의 데이터를 Use case 및 엔터티에서 사용하는 내부 요소로 변환

    - Framewor and driver

    - 데이터베이스, 웹 프레임워크 등 프레임워크와 도구

- 꼭 4개의 원만 사용하진 않아도 되지만, 종속성 규칙을 항상 적용해야함.

- 데이터가 경계를 넘는 경우는, 내부 원에 가장 편한 형식(most convenient for the inner circle)으로.

  - Entities를 넘기거나, Database row를 넘기면 안된다.

  - isolated, simple, data structures 를 넘겨야 함

## 3. 결론

- 소프트웨어를 계층으로 분리하고

- 종속성 규칙을 준수하여

- 테스트 가능한 시스템을 만들자

