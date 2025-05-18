# 트라이

## Trie란 무엇인가요?

Trie는 문자열을 저장하고 검색하는 데 최적화된 트리 구조.
각 노드는 문자의 집합으로 구성되고, 문자열의 접두사를 공유함으로써 공간을 절약.

## Trie에서 “apple”과 “app”을 모두 삽입하면 어떻게 되나요?

"app"까지는 노드가 공유되고, "apple"은 그 뒤에 새로운 분기('l', 'e')가 추가됨.
"app" 노드에는 isEnd: true, "apple"의 마지막 'e'에도 isEnd: true가 설정됨.

## Trie의 주요 사용 사례는?

- 문자열 자동완성 / 추천
- 접두사 기반 검색
- 사전(dictionary) 저장
- 대량의 문자열 검색 최적화

## JavaScript로 간단한 Trie를 어떻게 구현하나요?

```js
class TrieNode {
  constructor() {
    this.children = {};
    this.isEnd = false;
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  insert(word) {
    let node = this.root;
    for (const char of word) {
      if (!node.children[char]) {
        node.children[char] = new TrieNode();
      }
      node = node.children[char];
    }
    node.isEnd = true;
  }

  search(word) {
    let node = this.root;
    for (const char of word) {
      if (!node.children[char]) return false;
      node = node.children[char];
    }
    return node.isEnd;
  }

  startsWith(prefix) {
    let node = this.root;
    for (const char of prefix) {
      if (!node.children[char]) return false;
      node = node.children[char];
    }
    return true;
  }
}
```

## Trie의 시간복잡도는 어떻게 되나요?

| 연산                     | 시간 복잡도 (n: 단어 길이) |
| ------------------------ | -------------------------- |
| 삽입 (insert)            | O(n)                       |
| 검색 (search)            | O(n)                       |
| 접두사 확인 (startsWith) | O(n)                       |

문자열 길이에 비례하며, 많은 문자열이 접두사를 공유할수록 더 효율적.

## Trie와 Hash Map의 차이는?

| 항목        | Trie               | Hash Map                         |
| ----------- | ------------------ | -------------------------------- |
| 검색 대상   | 문자열의 구조      | 단일 키 (전체 문자열)            |
| 접두사 검색 | 매우 효율적        | 비효율적                         |
| 메모리      | 더 많이 사용       | 상대적으로 적음                  |
| 속도        | 길이에 비례 (O(n)) | O(1) (평균), but 접두사엔 부적합 |
