# Heap

## Heap이란 무엇인가요?

Heap은 완전 이진 트리 기반의 우선순위 큐 자료구조.

- Min Heap: 부모 노드 ≤ 자식 노드
- Max Heap: 부모 노드 ≥ 자식 노드

루트 노드에 항상 최소값/최대값이 위치.

## Heap은 어떤 상황에서 사용하나요?

- 우선순위 큐
- Top-K 문제 (K번째로 큰/작은 수)
- 실시간 정렬 (ex. 실시간 뉴스 피드, 순위 계산)
- Dijkstra 알고리즘등에서 경로 탐색 시

## JavaScript에는 Heap이 없는데 어떻게 구현하나요?

배열로 이진 트리 형태의 Heap을 만들 수 있음.

- 부모 인덱스: `Math.floor((i - 1) / 2)`
- 자식 인덱스: `i * 2 + 1`, `i * 2 + 2`

## 간단한 Min Heap 클래스 구조 구현

```jsx
var Heap = function () {
  var heap = {};

  heap.data = [null];

  heap.isEmpty = function () {
    return heap.data.length == 1;
  };

  heap.push = function (val) {
    // 리프 노드에 값을 넣고 히피파이.
    heap.data.push(val);
    var myIndx = heap.data.length - 1;
    var pIndx = Math.floor(myIndx / 2);
    console.log(pIndx);
    while (pIndx > 0) {
      if (heap.data[pIndx] < val) {
        heap.data[myIndx] = heap.data[pIndx];
        heap.data[pIndx] = val;
        myIndx = pIndx;
        pIndx = Math.floor(myIndx / 2);
        console.log(heap.data);
      } else break;
    }
  };

  heap.pop = function () {
    if (heap.isEmpty()) return false;
    // 최상단 값을 리턴하고
    var tmp = heap.data[1];
    // 리프 값을 최상단으로 올려서 다시 히피파이
    var n = heap.data.pop();
    heap.data[1] = n;

    var curIndx = 1;
    while (true) {
      var l = curIndx * 2;
      var r = curIndx * 2 + 1;

      var f = true;
      if (heap.data.length > l) {
        if (heap.data[curIndx] < heap.data[l]) {
          var t = heap.data[curIndx];
          heap.data[curIndx] = heap.data[l];
          heap.data[l] = t;
          curIndx = l;
          f = false;
        }
      }
      if (heap.data.length > r) {
        if (heap.data[curIndx] < heap.data[r]) {
          var t = heap.data[curIndx];
          heap.data[curIndx] = heap.data[r];
          heap.data[r] = t;
          curIndx = r;
          f = false;
        }
      } else break;
      if (f) break;
    }

    return tmp;
  };
};

Heap();
```

## Heap의 주요 연산 시간 복잡도는?

| 연산               | 시간복잡도 |
| ------------------ | ---------- |
| 삽입 (insert)      | O(logN)    |
| 삭제 (extract)     | O(logN)    |
| 최솟값/최댓값 조회 | O(1)       |
