# Data Structure

### Categories
- [Quick Sort](#Quick Sort)

### Quick Sort

전체 값들을 정렬하지 않고, 기준값으로 왼쪽 부분집합과 오른쪽 부분집합으로 나누어서 분할하여 정렬하는 방식.

평균 시간복잡도는 (n log n)을 가지는데 왼쪽 집합이나 오른쪽 집합이 한 곳으로 치우치게 되면 최악의 경우 (n^2) 시간복잡도를 가진다.

```java
public static void quickSort(int[] numbers) {
  quickSort(numbers, 0, numbers.length - 1);
}

private static void quickSort(int[] numbers, int start, int end) {
  //정렬 후, 오른쪽 부분집합의 시작 인덱스를 가져온다.
  int rightPartIndex = partition(numbers, start, end);

  //왼쪽 부분집합의 개수가 1개가 넘으면 정렬한다.
  if (start < rightPartIndex - 1) {
    quickSort(numbers, start, rightPartIndex - 1);
  }

  //오른쪽 부분집합의 개수가 1개가 넘으면 정렬한다.
  if (rightPartIndex < end) {
    quickSort(numbers, rightPartIndex, end);
  }
}

private static int partition(int[] numbers, int start, int end) {
  //부분집합의 기준값
  int pivot = numbers[(start + end) / 2];

  //start 인덱스와 end 인덱스가 교차하지 않을 때 까지 루프를 돌린다.
  while (start <= end) {
    //start 값이 기준값보다 작으면 오른쪽으로 1칸 이동.
    while (numbers[start] < pivot) {
      start++;
    }
    //end 값이 기준값보다 크면 왼쪽으로 1칸 이동.
    while (numbers[end] > pivot) {
      end--;
    }
    //위에 while문에 부호를 반대로 하면 내림차순으로 변경할 수 있다.

    //start가 end가 멈추는 시점에 교차하지 않으면 서로 값을 바꾸고 1칸씩 이동.
    if (start <= end) {
      swap(numbers, start, end);
      start++;
      end--;
    }
  }
  return start;
}

private static void swap(int[] numbers, int start, int end) {
  int temp = numbers[start];
  numbers[start] = numbers[end];
  numbers[end] = temp;
}
```
