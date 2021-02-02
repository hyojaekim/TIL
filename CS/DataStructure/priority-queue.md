### PriorityQueue

큐는 FIFO(First In First Out) 즉, 먼저 들어온 것은 먼저 나가는 선입선출 형태이다.

Java에서는 **PriorityQueue** 라는 큐가 존재한다. 간단하게 설명하자면 우선순위를 결정하여 들어온 순서와 상관없이 우선순위가 높은 것부터 나가게 된다.

```java
PriorityQueue<Integer> priorityQueue = new PriorityQueue<>();

priorityQueue.add(2);
priorityQueue.add(1);
priorityQueue.add(3);

// 1이 먼저 나온다.
priorityQueue.poll();
```

2, 1, 3을 순서대로 넣었을 때, 가장 먼저 나오는 것은 1이 먼저 나오게 된다.
큰 순서대로 넣으려면 아래와 같은 코드를 작성하면 된다.

```java
// 5 -> 큐의 길이
PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(5, Collections.reverseOrder());

priorityQueue.add(2);
priorityQueue.add(1);
priorityQueue.add(3);

// 3이 먼저 나온다.
priorityQueue.poll();
```

큐에 객체를 사용하려면, `Comparable<E>` 를 구현해야 한다.
