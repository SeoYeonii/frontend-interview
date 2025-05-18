# Linked List

## Linked List란 무엇인가요? Array와 어떤 차이가 있나요?

Array는 인덱스 기반이고 메모리상 연속된 공간을 사용.

- 인덱싱: O(1)
- 삽입 삭제: O(n)
- 메모리: 연속적

Linked List는 노드가 포인터로 연결된 선형 자료구조

- 인덱싱: O(n)
- 삽입 삭제: O(1)
- 메모리: 비연속적

배열은 제한 사항이 있음:

1. 배열의 크기가 고정되어 있어 미리 요소의 수에 대해 할당을 받아야 함. (JS는 아니긴 함)
2. 새로운 요소를 삽입하는 것은 비용이 많이 듬(공간을 만들고, 기존 요소 전부 이동)
3. Array는 한 아이템을 삭제하려고 하면 삭제 후 삭제된 아이템의 길이만큼 나머지 데이터가 이동을 해줘야한다. Array에 있는 모든 값은 index를 가지고 있고 index가 value 없이는 존재 할 수 없기 때문.

단점:

1. 임의로 엑세스를 허용할 수 없음. 즉 첫 번쨰 노드부터 순차적으로 요소에 엑세스 해야함 (이진 검색 수행 불가능)
2. 포인터의 여분의 메모리 공간이 목록의 각 요소에 필요

## JS에는 기본 Linked List가 없는데, 왜 그럴까요?

JS는 일반적으로 배열로도 충분한 대부분의 기능을 제공하고, 메모리 제어나 포인터 개념이 필요 없기 때문. 하지만 성능이나 구조적 이유로 직접 구현하는 경우도 있긴함.

## 단일 연결 리스트를 JS로 구현해보세요.

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
  }

  append(value) {
    const node = new Node(value);
    if (!this.head) {
      this.head = node;
      return;
    }
    let curr = this.head;
    while (curr.next) curr = curr.next;
    curr.next = node;
  }
}
```

## 중간 노드를 삭제하는 함수는 어떻게 만들 수 있을까요?

노드의 이전 포인터가 없는 단일 연결 리스트에서는 직전 노드를 순회로 찾고, 만약 양방향 연결 리스트라면 바로 prev. 이렇게 찾은 이전 노드와 다음 노드를 연결.

## 연결 리스트에서 사이클이 존재하는지 어떻게 확인할 수 있을까요?

Floyd의 토끼와 거북이 알고리즘(투 포인터)을 사용. 두 개의 포인터를 서로 다른 속도로 움직이다 보면 사이클이 있을 경우 언젠가 만나는 원리 사용.

## 배열과 연결 리스트 중 어떤 상황에서 Linked List를 선택하시겠어요?

- 삽입/삭제가 빈번하게 일어나는 경우
- 메모리 재배치를 피하고 싶은 경우
- 순차 접근만 필요한 경우

반대로 인덱스 접근이나 정렬이 필요하면 Array가 더 유리.

## 두 개의 정렬된 연결 리스트를 하나로 병합하는 로직은 어떻게 짜나요?

merge sort 할 때 처럼 포인터 두 개로 순차 비교하면서 새로운 리스트에 삽입

## 연결 리스트를 역순으로 바꾸는 알고리즘은?

```js
function reverseList(head) {
  let prev = null,
    curr = head;
  while (curr) {
    let next = curr.next;
    curr.next = prev;
    prev = curr;
    curr = next;
  }
  return prev;
}
```
