# [Javascript](https://github.com/hyojaekim/TIL/tree/master/Javascript) / [🏠 Home](https://github.com/hyojaekim/Javascript)

## let, const, var

### var

Scope는 함수 단위로 결정되는 변수이다. (function-scope)

#### 접근 가능
```javascript
var a = 123
function() {
  console.log(a) //123
}

for (var b = 0; b < 10; b++) {
  console.log(b) //0 1 2 3 4 5 6 7 8 9
}
console.log(b) //10
```

```javascript
function() {
  var a = 1234
}

console.log(a) //접근 불가능

function() {
  for (var b = 0; b < 10; b++) {
    console.log(b) //0 1 2 3 4 5 6 7 8 9
  }
}

console.log(b) //접근 불가능
```

`immediately-invoked function expression (or IIFE, pronounced "iffy")`

IIFE라는 것을 이용하면 접근 가능하게 만들 수는 있지만, 변수 선언하려고 너무 많은 일을 하고 있는 것 같다.

### let, const

Scope는 블럭 단위로 결정되는 변수이다. (block-scope)
ES2015(ES6)에서 let과 const 키워드가 등장. (var보다 이점이 많다)

#### 공통점
변수를 재선언하는 것이 불가능하다.

var는 아래와 같은 코드를 작성해도 오류없이 잘 동작한다..

```javascript
var a = 100
var a = 200 //가능

let b = 100
let b = 200 //불가능

const c = 100
const c = 200 //불가능
```

#### 차이점

1. let은 재할당이 가능하지만, const는 불가능하다.

```javascript
let a = 100
a = 100 //가능

const b = 100
b = 200 //불가능
```

2. let은 선언 후에 나중에 할당이 가능하지만, const는 바로 할당해야 한다.

```javascript
let a
a = 100 //가능

const b //불가능
```

### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/Javascript/js_position.md#ETC---home)
