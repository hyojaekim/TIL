# [ETC](https://github.com/hyojaekim/TIL/tree/master/ETC) / [🏠 Home](https://github.com/hyojaekim/TIL)

## OSIV(Open Session In View)

Spring Boot에서는 Default로 `Open Session In View`를 true로 설정하고 있다. OSIV는 `영속성 컨텍스트를 뷰 렌더링이 끝나는 시점까지 개방한 상태로 유지한다는 의미이다.`

#### 왜 등장하게 되었을까?

OSIV가 등장하게 된 이유는 View 레이어에 연관된 객체를 사용하면, `LazyInitializationException`이 발생하게 된다. 이를 해결하기 위해 OSIV가 등장하게 되었다.

#### 그렇다면 왜 발생할까?

findAll 메서드를 사용한다고 가정하자. 메서드가 종료되면

1. Transaction 종료
2. JDBC Connection disconnect
3. Hibernate Session 종료
4. 영속 객체는 Detached 상태가 된다.

`Detached`는 데이터베이스 식별자를 가지지만, 영속성 컨텍스트로부터 분리되었기 때문에 데이터베이스와의 동기화가 보장되지 않는 상태를 의미한다.

즉, Service 레이어에서 관리되는 Transaction이 View 레이어로 넘어가면서 종료되었기 때문에 LazyInitializationException이 발생하게 된다.

OSIV은 뷰 렌더링 시점에 Detached 상태의 객체의 프록시를 초기화 할 수 없기 때문에 뷰 렌더링 시점까지 영속성 컨텍스트를 유지하여, 작업 단위를 요청 시점부터 뷰 렌더링까지 확장하기 위해 사용한다.

#### OSIV 장단점

OSIV 패턴을 적용한다면 LazyInitializationException 문제가 발생하지 않기 때문에 장점이 될 수 있지만, 단점도 될 수 있다.

Transaction의 범위가 커지게 되면, 그 만큼 DB 커넥션을 붙잡고 있어야 한다는 단점이 있어 성능 이슈의 주 원인이라고 한다.

또, 레이어 아키텍처를 생각하면 뷰 레이어까지 트랜잭션이 지속되어야 하는게 맞나?, 뷰 레이어에서 객체를 사용하는게 맞나? 의심해보자.


### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/ETC/OSIV.md#ETC---home)
