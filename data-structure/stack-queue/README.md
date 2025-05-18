# Stack & Queue

## Stack과 Queue의 차이를 설명해보세요.

- Stack은 LIFO (Last In, First Out)구조. 마지막에 들어온 것이 먼저 나
- Queue는 FIFO (First In, First Out) 구조이며, 먼저 들어온 것이 먼저 나감.

## JS에서는 Stack과 Queue를 어떻게 구현하나요?

Stack은 push와 pop을 사용해 배열로 쉽게 구현할 수 있음.
Queue는 push와 shift로도 가능.

- shift는 O(n) 연산이라 Linked List로 구현하면 더 효율적

## Queue를 class 기반으로 직접 구현해본 적 있나요?

```jsx
class Queue {
  constructor() {
    this.storage = {};
    this.head = 0;
    this.tail = 0;
  }
  enqueue(val) {
    this.storage[this.tail++] = val;
  }
  dequeue() {
    if (this.head === this.tail) return null;
    const val = this.storage[this.head];
    delete this.storage[this.head++];
    return val;
  }
}
```

## Stack이나 Queue를 프론트엔드에서 사용한 경험이 있나요?

- Stack은 undo/redo 기능 구현에 사용했고,
- Queue는 Snackbar 메시지 큐, 비동기 작업 순차 실행에서 사용했음

## JS에서 shift가 느린 이유는 뭔가요?

배열은 인덱스를 기준으로 요소가 정렬돼 있는데, `shift`를 사용하면 모든 요소가 한 칸씩 앞으로 이동해야 해서 O(n) 시간이 걸림
