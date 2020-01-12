# [Algorithm](https://github.com/hyojaekim/TIL/tree/master/Algorithm) / [🏠 Home](https://github.com/hyojaekim/TIL)

### BubbleSort

선택 정렬(Select Sort)과 비슷한 알고리즘으로, `인접한 두 원소의 크기를 비교하여`, `조건에 맞지 않으면 자리를 교환`하여 정렬하는 알고리즘이다.

시간 복잡도는 `2개의 원소를 계속해서 비교하기 때문에 최선, 평균, 최악의 경우 모두 O(n^2)`이다.

```java
public static String bubbleSort(int[] numbers) {
    for (int i = 0; i < numbers.length; i++) {
        //사이클 마다 끝에 있는 숫자는 정렬을 한 상태이므로 -1씩 줄어든다.
        for (int j = 1; j < numbers.length - i; j++) {
            //큰 숫자가 뒤로 간다. (등호 반대로 하면 큰 숫자부터 정렬)
            if (numbers[j-1] > numbers[j]) {
                int temp = numbers[j-1];
                numbers[j-1] = numbers[j];
                numbers[j] = temp;
            }
        }
    }
    return Arrays.toString(numbers);
}
```

### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/Algorithm/bubble-sort.md#algorithm---home)
