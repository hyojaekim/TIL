# [Algorithm](https://github.com/hyojaekim/TIL/tree/master/Algorithm) / [🏠 Home](https://github.com/hyojaekim/TIL)

### 병합 정렬(Merge Sort)

`분할 정복` 방법을 채택한 알고리즘이다. 결과적으로 퀵 정렬과 동일하게 O(n log n) 시간 복잡도를 가진다.

`퀵 정렬`은 피벗 값에 따라 한 곳으로 치우치게 되면 최악의 경우 O(n^2) 시간 복잡도를 가지는 단점이 있다.

`병합 정렬`은 정확히 반절씩 나눈다는 점에서 최악의 경우에도 O(n log n)을 보장한다.

### 그렇다면 왜 O(n log n) 시간 복잡도를 가질까?
병합 정렬은 `일단 반으로 나누고 나중에 합쳐서 정렬한다.`

그림으로 보자.

![merge sort](./img/merge-sort(1).png)

너비 8개, 높이 3개로 모든 정렬이 완료된 것을 볼 수 있다.

높이 3개는 log 8은 3이므로 n(너비) * log n(높이)는 n log n으로 병합 정렬의 시간 복잡도는 O(n log n)을 보장한다.

### 왜 너비는 n일까?
시작 줄을 보면 각각의 원소 모두 정렬이 되어 있는 상태이다. 그 다음 줄부터 합치는 과정을 보면, n번 비교하여 합치는걸 볼 수 있다. 따라서 너비는 n이다.


### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/Algorithm/merge-sort.md#algorithm---home)
