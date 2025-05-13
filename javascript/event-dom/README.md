# 이벤트 & DOM

## 이벤트 위임(Event Delegation)이란 무엇인가요?

이벤트 위임은 부모 요소에 이벤트 핸들러를 등록하고, 실제 이벤트 대상은 이벤트 버블링을 통해 처리하는 방식

- 이유: 많은 자식 요소에 각각 이벤트를 붙이지 않고, 하나의 상위 요소에서 처리하여 성능 최적화와 동적 요소 대응이 가능

## 이벤트 버블링(Event Bubbling)이란?

이벤트가 가장 깊은 요소에서 시작해서, 부모 요소로 전파되는 현상
즉, 이벤트가 하위 → 상위 방향으로 전파

## 이벤트 캡처링(Event Capturing)이란?

이벤트가 루트 요소에서 시작해, 타깃 요소까지 내려오는 단계
상위 → 하위 방향으로 먼저 이벤트가 전파

일반적으로 JS에서는 버블링 단계가 기본이며, addEventListener(..., ..., { capture: true }) 설정 시 캡처링 단계에서 처리할 수 있음

## 실제 브라우저가 이벤트를 감지하는 방법

- 기본(default)으로는 버블링 단계에서 이벤트를 감지. 그래서 일반적으로 `addEventListener('click', handler)` 하면 → 자식 → 부모 방향으로 이벤트가 전파될 때 핸들러가 호출됨

## 캡쳐링 단계에서 이벤트를 감지하는 방법

`addEventListener`의 세 번째 인자인 옵션을 `{ capture: true }`로 주면 됌

## 버블링/캡쳐링을 중단하는 방법

`stopPropagation()`

- 현재 이벤트가 더 이상 부모 요소로 버블링(capturing/bubbling)되지 않게 중단시킴.
- 현재 엘리먼트에서 등록된 다른 핸들러는 실행됨

`stopImmediatePropagation()`

- 현재 엘리먼트의 나머지 이벤트 핸들러 실행 자체도 막는다. (같은 엘리먼트에 여러 핸들러 등록해도 중단)
- 버블링도 막음.
- 예시: 버튼 하나에 여러 핸들러 등록되어 있고, 특정 조건에서 이후 핸들러 실행을 아예 막고 싶을 때

`preventDefault()`

- 브라우저의 기본 동작을 막음

## HTML 속성(attribute)과 DOM 속성(property)의 차이는?

| 항목      | HTML 속성 (attribute)    | DOM 속성 (property)    |
| --------- | ------------------------ | ---------------------- |
| 정의 시점 | HTML 태그 내 작성        | JS에서 접근            |
| 접근 방법 | `element.getAttribute()` | `element.value`        |
| 예        | `<input value="test">`   | `input.value = 'new';` |

즉, HTML 작성 시 초기 상태는 attribute, JS 실행 중 상태는 property가 더 정확

## `event.target`과 `event.currentTarget`의 차이는?

- event.target: 실제 이벤트가 발생한 하위 요소
- event.currentTarget: 이벤트 핸들러가 등록된 요소 (this 역할)
  예를 들어 리스트가 있고 ul에 클릭 이벤트 위임해 놨고 li를 클릭했을 때 event.target은 li고 event.currentTarget은 ul임

## `event.preventDefault()`와 `event.stopPropagation()`의 차이는?

preventDefault(): 기본 동작 차단 (예: 링크 이동, 폼 전송 등)
stopPropagation(): 이벤트 버블링(전파) 중단
둘은 용도가 다름

- `preventDefault`: 행동 차단 <a>링크 이동 막고 싶을 때
- `stopPropagation`: 이벤트 흐름 차단 <a><b></b></a> 에서 b에 이벤트 걸면 a로 전파되는데 이를 막고싶을 때.

## 이벤트 위임은 언제 유리한가요?

- 수많은 자식 요소가 있을 때
- 동적으로 자식 요소가 추가/삭제될 수 있을 때
- 이벤트를 하나로 관리하고 싶을 때
- 이벤트 리스너를 적게 등록해 성능 향상이 필요할 때 사용

## addEventListener의 third 인자 options는 어떤 옵션이 있나요?

`element.addEventListener(type, listener, options);`

- `capture`: true면 캡처링 단계에서 실행 (기본값 false)
- `once`: true면 이벤트 한 번만 실행 후 자동 제거
- `passive`: true면 `preventDefault()`를 사용하지 않겠다는 힌트 → 스크롤 이벤트 성능 개선
