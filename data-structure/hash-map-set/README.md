# Hash (Set/Map)

## Hash Table이란 무엇인가요?

키-값 쌍을 저장하는 자료구조. 해시 함수를 통해 키를 해시값으로 변환해 빠르게 접근, 저장, 삭제가 가능. 평균적으로 O(1) 시간 복잡도를 가짐.

## 로드팩터란 무엇인가요?

- `(데이터의 개수)/(저장공간)`
- 데이터의 개수가 증가해서 로드팩터의 값이 원래 로드팩터의 값보다 커지게 되면 `저장 공간의 크기는 증가되고 해시 재정리 작업(refresh)`을 해야 함(JS는 알아서 처리해줌). 로드팩터라는 값이 클수록 공간은 넉넉해지지만, 데이터를 찾는 시간은 증가.

## 해시 함수?

1. Division Method: 나눗셈을 이용하는 방법으로 입력값을 테이블의 크기로 나누어 계산한다.( 주소 = 입력값 % 테이블의 크기) 테이블의 크기를 소수로 정하고 2의 제곱수와 먼 값을 사용해야 효과가 좋다고 알려져 있음
2. Digit Folding: 각 Key의 문자열을 ASCII 코드로 바꾸고 값을 합한 데이터를 테이블 내의 주소로 사용하는 방법.
3. Multiplication Method: 숫자로 된 Key값 K와 0과 1사이의 실수 A, 보통 2의 제곱수인 m을 사용하여 다음과 같은 계산을 해줌. h(k)=(kAmod1) × m
4. Univeral Hashing: 다수의 해시함수를 만들어 집합 H에 넣어두고, 무작위로 해시함수를 선택해 해시값을 만드는 기법.

## 충돌 해결방법?

- 분리 연결법(Separate Chaining) (메모리 상에 제한이 없으면)
  - 동일한 버킷의 데이터에 대해 자료구조를 활용해 추가 메모리를 사용하여 다음 데이터의 주소를 저장. 동일한 버킷으로 접근을 한다면 데이터들을 연결을 해서 관리. (실제로 Java8의 Hash테이블은 Self-Balancing Binary Search Tree 자료구조를 사용해 Chaining 방식을 구현했다고 함.)
- 개방 주소법(Open Addressing)
  - 추가적인 메모리를 사용하는 Chaining 방식과 다르게 비어있는 해시 테이블의 공간을 활용하는 방법.
    1. Linear Probing: 현재의 버킷 index로부터 고정폭 만큼씩 이동하여 차례대로 검색해 비어 있는 버킷에 데이터를 저장.
    2. Quadratic Probing: 해시의 저장순서 폭을 제곱으로 저장하는 방식.
    3. Double Hashing Probing: 해시된 값을 한번 더 해싱하여 해시의 규칙성을 없애버리는 방식. 해시된 값을 한번 더 해싱하여 새로운 주소를 할당하기 때문에 다른 방법들보다 많은 연산을 하게 됨.

## JS에서 Hash Table을 사용할 수 있는 객체는 무엇인가요?

- `Object`: 문자열/심볼 키만 허용, prototype
- `Map`: 모든 타입을 키로 허용, 순서 보장, 성능 안정
- `Set`: 유일한 값의 집합. 중복 제거에 유용

## Map과 Object의 차이점은 무엇인가요?

| 항목      | Object                 | Map                   |
| --------- | ---------------------- | --------------------- |
| 키 타입   | 문자열/심볼            | 모든 타입             |
| 키 순서   | 보장 안 됨             | 삽입 순서 유지        |
| 크기 확인 | `Object.keys().length` | `map.size`            |
| 성능      | 중간                   | 빠름 (대용량 시 우수) |

## 배열에서 중복을 제거하는 방법은?

`const unique = [...new Set(arr)];`

## 두 배열의 교집합을 구하는 법은?

```jsx
function intersection(a, b) {
  const setA = new Set(a);
  return b.filter((item) => setA.has(item));
}
```

## Map을 사용했을 때 장점은?

- 객체보다 명확하게 key-value 역할을 하고, 순회 시 순서가 유지돼서 UI 처리에 유리할 수 있음
- 키로 숫자나 객체도 쓸 수 있어서, React 상태값 캐싱처럼 복잡한 구조를 관리하기 좋을 수 있음

## Map/Set을 사용할 때 시간 복잡도는 어떻게 되나요?

O(1). 단, 해시 충돌이 많으면 최악의 경우 O(n). JS의 `Map`과 `Set`은 내부적으로 해시와 리스트를 적절히 조합해서 성능을 보장
