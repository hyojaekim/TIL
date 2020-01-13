# [Java](https://github.com/hyojaekim/TIL/tree/master/Java) / [🏠 Home](https://github.com/hyojaekim/TIL)

### 객체지향 프로그래밍(OOP)

```
실제 세계를 모델링하여 사람의 사고와 가장 비슷하게 프로그래밍하는 패러다임.
```

<hr>

### 특징

#### 1. 캡슐화 (Encapsulation)
리모컨을 사용할 때, 내부 회로는 사용자가 알 필요가 없듯이, **객체의 내부를 숨기는 것이다.**

#### 2. 상속 (Inheritance)
상위 부모 객체의 속성을 자식이 물려받아 코드의 재사용성을 높일 수 있다.

#### 3. 다형성 (Polymorphism)
다형성을 구현하는 방법 2가지가 있다.
```
오버 로딩
같은 클래스 안에 이름은 같지만 매개변수가 다른 메소드가 여러 개 존재 할 수 있다.

오버 라이딩
상위 클래스가 가지고 있는 메소드를 하위 클래스에서 재정의 하는 것으로, 인자와 이름이 같지만 행동은 다르게 할 수 있다.
```
#### 4. 추상화 (Abstraction)
객체의 공통된 속성과 행위를 추출하는 것을 말한다.

<hr>

### OOP 5대 원칙 (SOLID)

#### 1. 단일 책임 원칙(SRP, Single Responsibility Principle)
객체는 단 **하나의 책임만 가져야 한다.**

#### 2. 개방-폐쇄 원칙(OCP, Open Closed Principle)
**기존 코드를 변경하지 않고**, **기능을 추가** 할 수 있어야 한다. OCP를 가능케 하는 중요 메커니즘은 추상화와 다형성이다.

* 변경 될 부분과, 그렇지 않은 부분을 나눌 수 있어야 한다.
* 구현에 의존하기 보다는 정의한 인터페이스에 의존하도록 코드를 짜야 한다.

#### 3. 리스코프 치환 원칙(LSP, Liskov Substitution Principle)
**자식 클래스는 최소한 자신의 부모 클래스에서 가능한 행위는 수행할 수 있어야 한다.**

```java
List<String> test = new ArraysList();
test.add("123");

test = new LinkedList();
test.add("123");
```

어떤 자료 구조를 사용하든 생성 하는 부분만 바꾸어 주면 문제가 없고, add()는 변화에는 닫혀 있고, 변경과 확장에는 열려 있어 LSP와 OCP 모두 찾을 수 있다.

#### 4. 인터페이스 분리 원칙(ISP, Interface Segregation Principle)
**인터페이스를 클라이언트에 특화되도록 분리** 시키라는 설계 원칙.

#### 5. 의존 역전 원칙(DIP, Dependency Inversion Principle)
의존 관계를 맺을 때 **자주 변화하는 것보다는 거의 변화가 없는 것에 의존하라는 것이다.**

DIP를 만족한다는 것은 의존관계를 맺을 때, 구체적인 클래스보다 인터페이스나 추상 클래스와 관계를 맺는다는 것을 의미한다.

### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/Java/oop.md#java---home)
