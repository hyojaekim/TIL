# [Java](https://github.com/hyojaekim/TIL/tree/master/Java) / [🏠 Home](https://github.com/hyojaekim/TIL)

### String & StringBuilder & StringBuffer의 차이점

##### \* String - 불변 (Immutable)

- '+' 연산자로 문자를 추가하면, 이어서 추가하는 것이 아니라 새로운 객체를 만들어낸다. 계속해서 객체를 만들기 때문에 오버헤드가 발생하여 성능이 떨어질 수 있다.
- 객체는 불변하기 때문에 조회연산은 가장 빠르게 읽을 수 있는 장점이 있다.

```
문자열 연산이 적고, 조회가 많고, 멀티쓰레드 환경에서 사용하면 좋다!
```

##### \* StringBuilder & StringBuffer - 가변 (Mutable)

- 연산이 필요할 경우 크기를 변경시켜 문자열을 변경한다.
- StringBuffer는 멀티쓰레드환경에서 synchronized키워드가 가능하므로 동기화가 가능하다. 즉, thread-safe하다.
- StringBuilder는 동기화를 고려하지 않기 때문에 싱글쓰레드 환경에서 StringBuffer에 비해 연산처리가 빠르다.

```
문자열 연산이 많고, 멀티쓰레드 환경에서 StringBuffer를 사용하고 싱글쓰레드 환경이나 쓰레드를 신경 쓸 필요가 없는 경우에는 StringBuilder를 사용하자!
```

### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/Java/create-string.md#java---home)
