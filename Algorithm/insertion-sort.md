# [Algorithm](https://github.com/hyojaekim/TIL/tree/master/Algorithm) / [🏠 Home](https://github.com/hyojaekim/TIL)

### 삽입 정렬(Insertion Sort)

카드 게임을 하면 나도 모르게 한 장씩 숫자를 보고 정렬하는 방법과 유사하다.

앞의 원소들과 비교하면서 원소들을 뒤로 옮기면서 지정된 자리에 삽입하는 방식이다.

필요할 때에 한해서만 삽입을 진행하기 때문에 데이터가 이미 정렬된 상태라면 어떤 알고리즘보다 빠르다는 장점이 있다.

버블 정렬, 선택 정렬과 마찬가지로 O(N^2)으로 동일하지만, 3개 중에서는 가장 뛰어난 알고리즘이다.

```java
public String sort(int[] array) {
    for (int i = 0; i < array.length - 1; i++) {
        int j = i;
        while (array[j] > array[j + 1]) {
            int temp = array[j];
            array[j] = array[j + 1];
            array[j + 1] = temp;
            j--;
        }
    }
    return Arrays.toString(array);
}
```


### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/Algorithm/insertion-sort.md#algorithm---home)
