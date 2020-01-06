# [Spring](https://github.com/hyojaekim/TIL/tree/master/Spring) / [🏠 Home](https://github.com/hyojaekim/TIL)

### Controller와 RestController의 차이
Controller는 주로 View를 반환하기 위해 사용하고, RestController는 주로 데이터를 반환하기 위해 사용한다.

목적에 따른 차이도 있지만, 흐름에도 차이가 있다.

Controller는 `DispatcherServlet` -> `HandlerMapping` -> `Controller`에서 ***View를 거쳐서*** 알맞는 View를 리턴한다.
RestController는 `DispatcherServlet` -> `HandlerMapping` -> `Controller`까지 같지만 ***View를 거치지 않고*** 데이터를 반환한다.

### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/Spring/Controller&RestController.md#Spring---home)
