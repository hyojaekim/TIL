# [DataStructure](https://github.com/hyojaekim/TIL/tree/master/DataStructure) / [🏠 Home](https://github.com/hyojaekim/TIL)

## 큐(Queue)

### 과정 - **먼저 들어오면 먼저 나간다. (FIFO)**

**ENQUEUE**: 큐에 데이터를 삽입하는 과정
![Enqueue](./img/queue(1).png)

**DEQUEUE**: 큐에서 데이터를 빼내는 과정
![Dequeue](./img/queue(2).png)

---

### 큐의 활용
- 프린트 - 1쪽부터 먼저 나감

---

### Java로 구현하기

```java
interface Queue {
    void enqueue(Object data);
    Object dequeue();
    boolean isEmpty();
    void clear();
    Object peek();
}

public class TestQueue implements Queue {

    private int front;
    private int rear;
    private int queueSize;
    private Object[] result;

    public TestQueue(int queueSize) {
        this.front = -1;
        this.rear = -1;
        this.queueSize = queueSize;
        this.result = new Object[this.queueSize];
    }

    //큐의 가장 마지막에 데이터를 삽입합니다.
    @Override
    public void enqueue(Object data) {
        if (isFull()) {
            System.out.println("Insertion Fail!");
            return;
        }
        result[++rear] = data;
        System.out.println("Insertion Success!");
    }

    //큐가 가득 찼는지 확인 합니다.
    private boolean isFull() {
        return this.rear == this.queueSize - 1;
    }

    //큐의 첫 번째 위치에 있는 데이터를 반환하고 큐에서 삭제합니다.
    @Override
    public Object dequeue() {
        if (isEmpty()) {
            System.out.println("Dequeue Fail! Queue is empty!");
            return null;
        }
        System.out.println("Dequeue Success!");
        return result[++front];
    }

    //큐가 empty 상태인지 확인합니다.
    @Override
    public boolean isEmpty() {
        if (this.front == this.rear) {
            this.front = -1;
            this.rear = -1;
        }
        return this.front == this.rear;
    }

    //큐에 저장된 모든 데이터를 삭제하고 큐를 초기화합니다.
    @Override
    public void clear() {
        this.front = -1;
        this.rear = -1;
        this.result = new Object[this.queueSize];
        System.out.println("Queue Clear!");
    }

    //큐의 첫 번째 위치에 있는 데이터를 추출합니다.
    @Override
    public Object peek() {
        if (isEmpty()) {
            System.out.println("Peek Fail! Queue is empty!");
            return null;
        }
        System.out.println("Peek Success!");
        Object result = this.result[++front];
        this.result[front] = null;
        return result;
    }

    @Override
    public String toString() {
        StringJoiner stringJoiner = new StringJoiner(",");
        for (int i = 0; i < queueSize; i++) {
            if (result[i] != null) {
                stringJoiner.add(result[i].toString());
            }
        }
        return stringJoiner.toString();
    }
}
```


### [맨 위로 이동](https://github.com/hyojaekim/TIL/blob/master/DataStructure/queue.md#DataStructure---home)
