# 이분 탐색

## 이분 탐색이란 무엇인가요?

정렬된 배열에서 원하는 값을 찾기 위해 중간 값을 기준으로 탐색 범위를 절반씩 줄여가는 탐색 알고리즘. 반복 또는 재귀로 구현할 수 있고, 탐색 대상이 크면 성능이 매우 뛰어남.

## 이분탐색의 시간복잡도는?

O(log n)→ 탐색 범위를 매번 절반으로 줄이기 때문.

## JS로 이분 탐색을 어떻게 구현하나요?

```js
function binarySearch(arr, target) {
  let left = 0,
    right = arr.length - 1;
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (arr[mid] === target) return mid;
    if (arr[mid] < target) left = mid + 1;
    else right = mid - 1;
  }
  return -1;
}
```

## 이분 탐색이 가능한 조건은 무엇인가요?

반드시 데이터가 정렬되어 있어야 함. 정렬되어 있지 않으면 탐색 결과가 보장되지 않음

## while (left <= right) vs while (left < right)의 차이는?

- left <= right는 정확한 인덱스 탐색에 사용
- left < right는 최소/최대 경계값 탐색에 사용
  (ex. 이분 탐색으로 최소값을 찾는 문제)

## 이분 탐색에서 무한 루프에 빠지는 이유는?

- mid 계산 시 오버플로우
- left와 right 업데이트 조건이 잘못되어 탐색 범위가 줄지 않을 때
  → 항상 left = mid + 1, right = mid - 1 조건을 잘 확인해야 함
