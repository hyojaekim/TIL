# [Java](https://github.com/hyojaekim/TIL/tree/master/Java) / [🏠 Home](https://github.com/hyojaekim/TIL)

### String은 어떻게 생성할까?

```
String content = "test";
String content = new String("test");
```

String을 생성하는 방법에는 2가지 경우가 있다. 하지만 두 생성 방식에 따라 차이점이 있을까? 한번 알아보자.

```
String str1 = "test";
String str2 = "test";
String str3 = new String("test");
```

1. str1 == str2 (true)
2. str1 == str3 (false)

힙에 string pool이 있는데 자바에서는 문자열을 string pool로 관리된다.
`str1 == str2`가 같은 이유는 str1이 생성되면 string pool에 "test" 문자열을 만들고 str2는 만들어진 "test" 문자열을 참조하기 때문에 같다.

반면에 str3은 새로운 객체를 힙에 생성하기 때문에 다른 주소를 가져 str1과 다르다. 힙에 저장된 String을 intern() 메소드를 사용하게 되면 string pool에 등록할 수 있다.

마지막으로 정리하자면, String과 new String()은 값은 같지만 메모리 영역이 다르다는 차이점이 있다. new String()도 intern() 메소드를 사용해서 같은 영역에 위치하도록 등록 할 수 있다.

그렇다면 어떻게 사용할까?

한번 쓰고 버려질 문자열은 new String()으로 객체를 만들어서 GC 대상이 되도록 만들고, 왠만하면 ""으로 생성하자!

### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/Java/string.md#java---home)
