# [ETC](https://github.com/hyojaekim/TIL/tree/master/ETC) / [🏠 Home](https://github.com/hyojaekim/TIL)

## 테스트 Timeout 문제

WebTestClient를 사용했을 때, timeout 관련 예외가 발생했다.

```java
java.lang.IllegalStateException: Timeout on blocking read for 5000 MILLISECONDS

...
```

기본적으로 WebTestClient는 timeout이 5000 (5초)를 기본값으로 가진다. 계속해서 timeout 관련 예외가 발생한다면 아래와 같이 해결 할 수 있었다.

```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
@AutoConfigureWebTestClient(timeout = "10000")//10 seconds
public class CommonTest {

    @Autowired
    private WebTestClient webClient;

    ...
```


### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/ETC/fail_test_timeout.md#ETC---home)
