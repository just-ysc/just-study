# Entity, Value Object(VO), Data Transfer Object(DTO)

## Entity

- <b>식별성</b>과 <b>연속성</b>을 가진 객체

### 식별성

- 객체를 유일하게 식별할 수 있는 식별자를 가졌을 때 식별성을 띤다고 할 수 있다.

### 연속성

- 생명 주기 동안 식별자를 제외한 다른 속성이 변경될 수 있는 성질
- Entity는 고유의 생명 주기를 갖는 객체이고, 생명 주기 동안 식별자 외의 다른 속성들이 변경 가능한 가변 객체이다.

## Value Object

- 개념적인 식별성이 없이 특정 도메인의 서술적 측면을 나타내는 객체
- 식별자를 갖지 않으며, 일반적으로 모든 속성이 동일하면 동일한 객체로 취급한다.
- Value Object는 가급적 불변 객체로 설정하고, 속성 변경이 필요할 경우 새로운 객체를 생성하는 방식으로 사용해야 코드의 복잡성을 줄일 수 있다.

## Data Transfer Object

- 원격 호출 수를 줄이기 위해 연관된 도메인 객체로부터 데이터를 모아서 전달하기 위한 객체
- 데이터 전송 시의 직렬화 메커니즘을 DTO 내에서 처리할 수 있기 때문에, 직렬화 과정을 객체 내부에서 캡슐화할 수 있다는 장점도 갖는다.

## Reference

- https://veluxer62.github.io/explanation/about-entity-and-value-object/#entity
- https://github.com/benelog/blog/issues/27
- https://martinfowler.com/eaaCatalog/dataTransferObject.html