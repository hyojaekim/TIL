# [ETC](https://github.com/hyojaekim/TIL/tree/master/ETC) / [🏠 Home](https://github.com/hyojaekim/TIL)

## 우아한 CRUD (1)

DB 테이블과 연관된 클래스는 어떻게 만들어야할까?

퍼시스턴스 프레임워크는 어떤 것을 써야 할까?

### 문제점

- 복잡한 연관 관계는 불필요한 쿼리가 많이 날아가게 된다.
- N + 1 쿼리 주의!
- Lazy loading이 모든 것을 해결해주지는 않는다.
- 만능 클래스가 뷰까지 바로 전달되면 더 복잡해질 수 있다.

### 해법 찾기

현장에서 많이 쓰는 이름

- Java Beans
- VO
- DTO
- Enity

### VO vs DTO

Value Object

- 값이 같다면 동일하게 간주되는, 식별성이 없는 객체 (Money, Color)
- DTO와 혼용해서 쓰여 왔다. (DTO와 동일한 의미라고 밝힌 서적도 있다)
- Data Holder의 의미로 폭넓게 생각하는 경향도 있다.

Data Transfer Object

- 레이어 간의 경계를 넘어서 데이터를 전달하는 역할

### Entity와 VO의 구분

Entity

- DB 테이블과 대응되는 객체

DDD의 용어

- ENTITY : 연속성과 식별성의 맥락에서 정의되는 객체 (ID가 다르면 다른 객체로 식별)
- VALUE OBJECT : 식별성 없이 속성만으로 동일성을 판단하는 객체

### ENTITY 감추기

외부 노출용 DTO 따로 만들기

DTO의 이름 고민

- 이슈 조회 JSON 응답 : IssueResponse, IssueDto, IssueDetailDto
- 이슈 생성 JSON 요청 : IssueCreationRequest, IssueCreationCommand
- 이슈 조회 조건 : IssueQuery, IssueCriteria
- 이슈 DB 통계 조회 결과 : IssueStatRow
- 이슈 + 코멘트 복합 조회 결과 : IssueCommentRow

### AGGREGATE로 ENTITY 간의 선긋기

AGGREGATE는?

- 하나의 단위로 취급되는 연관된 객체군, 객체망
  - ENTITY와 VO의 묶음
  - Transaction, Lock의 필수 범위
  - Documnet DB와 어울림
- AGGREGATE 1개당 REPOSITORY 1개 (리턴 타입 참고)

```java
public interface CrudRepository<AGGREGATE_ROOT, ID> extends Repository<AGGREGATE_ROOT, ID> {
    Optional<AGGREGATE_ROOT> findById(ID id);
    ...
}
```

### AGGREGATE 간의 참조

- ID로만 참조하기
[https://stackoverflow.com/questions/4919687/aggregate-root-references-other-aggregate-roots/4922100#4922100](https://stackoverflow.com/questions/4919687/aggregate-root-references-other-aggregate-roots/4922100#4922100)

### 여러 AGGREGATE에 걸친 조회

```java
  MilestoneEntity milestone = milestoneRepository.findByid(milestoneId);
  int issueCount = issueRepository.countByMilestoneId(milestoneId)

  var miletoneReponse  = MilestoneResponse.builder()
      .name(milestone.getName())
      .endedAt(milestone.endedAt())
      .issueCount(issueCount)
      .build();
```

각각의 REPOSITORY에서 조회를 하고, DTO로 합치기

- 한방 쿼리가 더 유리하지 않나?
  - 오히려 쿼리가 단순해서 DB 성능에 더 유리할 수 있다.

### JOIN이 필수적인 경우

WHERE절에 다른 AGGRAGATE의 속성이 필요한 경우

```
SELECT r.name, r.description, r,created_by, r.created_at
FROM repo r
    INNER JOIN account a ON a.id = r.created_by
WHERE a.email = :email
```

SELECT 결과까지 다른 AGGRAGATE의 속성을 포함할 경우

```
SELECT r.name, r.description, a.name AS creator_name , a.email
FROM repo r
    INNER JOIN account a ON a.id = r.created_by
WHERE a.email = :email
```

이런 쿼리는 REPOSITORY보다 DAO가 어울린다.

### REPOSITORY vs DAO

- AGGREGATE와 1 : 1로 대응되냐 안되냐에 차이

### Lazy loading 다시 생각하기

- Lazy loading이 필요하다는 것은 모델링을 다시 생각해봐야한다는 신호일수도 있다.

### Immutable & Rich Domain Object

Immutable 객체의 장점

- Cache 하기에 안전
- 다른 레이어에 메서드 파라미터로 보내도 값이 안 바뀌었다는 확신
- DTO류가 여러 레이어를 오간다면 Immutable하면 더 좋다.

Rich Domain Object

- 상태를 바꾸는 메서드가 포함될 수도 있다.
  - 상태를 바꿀 때의 정합성 검사를 포함
- 영속화될 Domain Object라면 상태를 바꾸는건 시스템의 상태를 바꾸는 경우에 한해야한다.
  - 메서드명은 행위를 잘 드러내야 한다. setTitle() → changeTitle()

### 퍼시스턴스 프레임워크

프레임워크의 특정 기능을 위해서 추구하는 객체 설계를 포기하는 상황이 적을수록 좋다. (프레임워크를 사용하기 위해 setter를 사용하는 경우)

1. JDK 13이상의 raw literal String
2. Groovy로 SQL 관리
3. Spring JDBC
4. JPA
  성숙한 사용자는 이미 2가지 프로그래밍 모델을 섞어서 쓰고 있을 가능성이 높다.
    - CUD, 단순R : Entity, Repository, 쿼리 자동 생성
    - 복잡한 R : 응답전용 DTO, + QueryDSL 등으로 개념적인 쿼리는 직접 작성

### 프레임워크 활용 전략

- CUD + 단순 R : JPA
- 복잡한 R
  - JPA를 써도 쿼리작성 및 최적화를 의식하면서 구현
- 하나의 프레임워크로 통일한다면 Spring Data JDBC도 고려해도 좋음

### 정리

- 선을 넘지 않는 ENTITY
  - 외부 레이어에 ENTITY 감추기
  - AGGREGATE 단위로 ENTITY간의 경계 의식하기 (ID만 참조)
  - 복합적인 READ 결과를 담을 클래스 분리
- 프레임워크는 설계를 거드는 역할이 되어야
  - 프레임워크에서 주는 제약이 설계에 도움을 주기도한다.
  - 편의성을 주는 기능이 설계를 해치는지 경계해야 한다.
- 때로는 다른 가치를 위해 더 긴 코드를 만들 수도 있다.
  - 고치기 쉬운 , 협업하기 쉬운, 확장하기 쉬운 코드

### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/ETC/woowa_crud_1.md#ETC---home)
