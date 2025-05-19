# 병합 정렬, 퀵 정렬, 힙 정렬

## 병합 정렬이란 무엇인가요?

분할 정복(Divide & Conquer) 알고리즘으로,
배열을 반으로 나누고 재귀적으로 정렬한 뒤, 두 정렬된 배열을 병합.
안정 정렬이며, 항상 일정한 성능을 보장

- 시간 복잡도: O(n log n)
  - 분할 : n개 원소를 두 개로 분할 -> O(logn)
  - 병합 : 최대 n번의 비교 연산 -> O(n)
- 공간 복잡도: O(n) (추가 배열 필요)

특징:

- 데이터 크기가 크고 정렬이 안정적이어야 할 때 사용
- 병합 정렬은 순차적인 비교를 통해 정렬하므로, LinkedList의 정렬에 효율적
- JavaScript 내장 정렬의 기반으로도 사용된 적 있음
- 추가 메모리를 사용해야 하므로 메모리 효율은 떨어짐

## 병합 정렬을 어떻게 JS로 구현하나요?

```js
function mergeSort(arr) {
  if (arr.length <= 1) return arr;
  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));
  return merge(left, right);
}

function merge(left, right) {
  const result = [];
  while (left.length && right.length) {
    result.push(left[0] < right[0] ? left.shift() : right.shift());
  }
  return result.concat(left, right);
}
```

## 퀵 정렬이란 무엇인가요?

배열에서 기준 값(pivot)을 선택해, 그보다 작은 값과 큰 값을 나눠 재귀적으로 정렬하는 분할 정복 알고리즘. 일반적으로 제일 빠른 정렬방식으로 알려져 있음.

- 평균 O(n log n)
- 최악 O(n²) (pivot이 나쁘게 선택된 경우)
- 공간복잡도 O(log n) (재귀 깊이)

특징:

- 불안정 정렬 → 같은 값을 가진 요소들의 순서가 유지되지 않음
- 피봇을 사용할 때 배열 내부에서 참조를 하기 때문에 가장 빠름, 같은 메모리 주소를 참조하기 때문에 아이템을 바꾸기 때문에 캐시에다 그 데이터를 저장을 함.램에있는 데이터보다 캐시에 있는 데이터에 참조하는 속도가 훨씬 빠르기 때문에 그래서 일반적으로 가장 빠르다고 함
- 평균적으로 O(N log N) 정렬 → 대부분의 경우 빠름
- 메모리 추가 사용이 적음 (in-place 정렬 가능)
- 최악의 경우 O(N²) 가능 → 해결책: 랜덤 피벗 선택

시간복잡도:

- 최선의 경우
  - 피봇에 의한 원소들의 부분집합이 정확히 n/2개씩 2등분 되는 경우가 반복되는 경우
  - 시간 복잡도 : O(nlogn)
- 최악의 경우
  - 피봇에 의한 원소들의 부분집합이 1개과 n-1개로 분할되는 경우가 반복되는 경우
  - 시간 복잡도 : O(n2)
    공간 복잡도:
- 주어진 배열 내에서 교환을 하며 수행하므로 O(n)

## 퀵 정렬 JS 구현

```js
function quickSort(arr) {
  if (arr.length <= 1) return arr;
  const pivot = arr[0];
  const left = arr.slice(1).filter((el) => el <= pivot);
  const right = arr.slice(1).filter((el) => el > pivot);
  return [...quickSort(left), pivot, ...quickSort(right)];
}
```

## 힙 정렬이란 무엇인가요?

힙(Heap) 자료구조를 기반으로 한 정렬 알고리즘. 최대 힙을 구성해 루트(최댓값)를 꺼내 정렬. 이 과정을 반복해 전체 정렬.

특징:

- 가장 크거나 가장 작은 값을 구할 때 → 한번의 heapify로 구할 수 있으므로 유용
- 최대 k 만큼 떨어진 요소들 정렬 → 삽입 정렬보다 더욱 개선된 결과를 얻어낼 수 있음
- 동일한 값에 대해 기존의 순서가 유지되지 않는 불안정 정렬
- 항상 O(N log N) 보장 → 퀵 정렬과 다르게 최악 O(N²)이 없음
- 추가 메모리 필요 없음 (in-place 정렬 가능)
- 힙 구성 과정이 비교적 느림 → 퀵 정렬보다 일반적으로 느림

시간 복잡도:

- 정렬된 원소 구하기(히프 재구성) : 완전 이진 트리를 히프로 구성하는 평균 시간 O(logn)
- n개 노드에 대해 삭제 연산한 히프 재구성 시간 : O(nlogn)
- 따라서 시간 복잡도는 O(nlogn)

## JS로 힙 정렬을 구현할 수 있나요?

```js
function heapSort(arr) {
  const n = arr.length;

  const heapify = (i, len) => {
    let largest = i;
    const left = 2 * i + 1;
    const right = 2 * i + 2;

    if (left < len && arr[left] > arr[largest]) largest = left;
    if (right < len && arr[right] > arr[largest]) largest = right;

    if (largest !== i) {
      [arr[i], arr[largest]] = [arr[largest], arr[i]];
      heapify(largest, len);
    }
  };

  for (let i = Math.floor(n / 2) - 1; i >= 0; i--) heapify(i, n);
  for (let i = n - 1; i > 0; i--) {
    [arr[0], arr[i]] = [arr[i], arr[0]];
    heapify(0, i);
  }

  return arr;
}
```

## 병합 정렬 vs 퀵 정렬 vs 힙 정렬

| 알고리즘  | 평균 성능  | 최악 성능  | 공간복잡도 | 안정 정렬 |
| --------- | ---------- | ---------- | ---------- | --------- |
| 병합 정렬 | O(n log n) | O(n log n) | O(n)       | ✅        |
| 퀵 정렬   | O(n log n) | O(n²)      | O(log n)   | ❌        |
| 힙 정렬   | O(n log n) | O(n log n) | O(1)       | ❌        |
