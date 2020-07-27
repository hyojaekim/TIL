# [Javascript](https://github.com/hyojaekim/TIL/tree/master/Javascript) / [🏠 Home](https://github.com/hyojaekim/Javascript)

## async & await

> 비동기 처리 패턴 중 가장 최근에 나온 기법

### 기본 문법
```javascript
async function 함수명() {
  await 비동기_처리_메서드_명();
}
```

1. 함수 앞에 `async` 예약어를 붙인다.
2. 내부 로직 중 HTTP 통신을 하는 비동기 처리 코드 앞에 `await`를 붙인다.

***주의!***
비동기 철리 메서드가 꼭 프로미스 객체를 반환해야 한다.
(일반적으로 Axios등 프로미스를 반환하는 API 호출 함수)

### await를 사용하지 않았다면?

> 데이터를 받아온 시점에 콜백 함수나 .then() 등을 사용해야 한다.

### 예외 처리

`try catch`

프로미스에서 에러 처리를 위해 `.catch()`를 사용해야 했는데 async는 `catch { }`를 사용한다.

### 장점

1. 비동기 처리할때 콜백이나 프로미스를 사용하게 되면 가독성이 떨어지고, 코드가 길어진다. async를 이용하면 이를 보완할 수 있다.

2. 기존의 비동기 처리 방식으로 사고하지 않아도 된다.

### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/Javascript/async-await.md#ETC---home)
