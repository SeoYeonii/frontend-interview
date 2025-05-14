# 함수형 프로그래밍

## 함수형 프로그래밍

함수형 프로그래밍은 순수 함수(pure function) 와 불변성(immutability) 을 기반으로, 함수 단위의 조합과 재사용을 강조하는 프로그래밍 패러다임.
JavaScript에서는 고차 함수, 클로저, 일급 객체 등을 통해 함수형 프로그래밍 기법을 많이 활용할 수 있음. 예를 들어 map, filter, reduce 같은 함수는 상태 변경 없이 데이터를 처리할 수 있어 함수형 프로그래밍의 핵심.
함수형 프로그래밍에서는 일반적인 함수의 조합이 아니라, 순수함수의 조합이 포인트.

순수함수

- 동일한 입력에는 항상 같은 값을 반환해야 함.
- 함수의 출력(return)은 오로지 그 함수에 입력된 값(input)에만 의존함.
- 함수의 실행은 프로그램의 실행에 영향을 미치지 않아야 함.(Self-contained되어야 한다, 즉, side effect가 없다.)
  - Side effect가 없다는 의미는 오로지 출력(return) 만 수행한다는 의미.

고차원 함수(Higher-Order Functions)

- 함수를 인자(argument)로 받음.
- 함수를 결과로 반환함.

## 순수함수는 무엇인가요? 순수함수의 장점은?

순수 함수란 부수효과가 없는 함수 즉, 동일한 입력에 대해 항상 동일한 결과를 반환하고, 외부 상태를 변경하지 않는 함수

```jsx
// 순수 함수 예시
function add(a, b) {
  return a + b;
}
```

장점

- 예측 가능성: 테스트와 디버깅이 쉬움
- 재사용성: 사이드 이펙트가 없으므로 다양한 곳에서 안전하게 재사용 가능
- 병렬 처리에 유리: 상태 공유가 없기 때문에 동시성 프로그래밍에 적합

## 커링 함수(Curry Function)의 예와 이 문법이 주는 장점은 무엇인가요?

커링(Currying) 은 여러 개의 인자를 받는 함수를 하나의 인자를 받는 함수들로 변환하는 기법

```jsx
const multiply = (a) => (b) => a * b;
const double = multiply(2);
console.log(double(5)); // 10
```

장점

- 재사용성이 뛰어나고, 고차 함수와 함께 쓰기에 적합
- 부분 적용(Partial Application)을 통해 코드 간결성 확보
- DI(Dependency Injection) 방식으로 로직 분리 가능

## 메소드 체이닝이란 무엇이며, 이것의 장단점은 무엇인가?

여러 메서드를 연속적으로 호출하여 데이터를 처리하는 방식
메소드 체이닝의 장점은 코드가 짧아진다는 장점이 있고, 단점은 에러가 났을때 어느 부분의 메소드에서 오류가 났는지 확인이 어려움

장점

- 코드가 간결하고 가독성 향상
- 불변성 유지와 함수형 프로그래밍 스타일에 적합

단점

- 디버깅이 어려움: 어디서 에러가 발생했는지 추적이 힘듦
- 모든 메서드가 `this` 또는 체이닝을 반환하도록 구현되어야 함

## JavaScript로 객체지향 프로그래밍(OOP)을 적용할 때 어떤 식으로 접근하시나요?

- 클래스 기반 구성: ES6 이후의 `class` 문법을 활용해 캡슐화, 상속, 다형성 등을 구현
- 컴포지션 기반 설계: 상속보다 구성(composition)을 통해 유연한 구조 설계
- SOLID 원칙 고려: 특히 단일 책임 원칙(SRP), 개방-폐쇄 원칙(OCP)을 자주 적용
- 유지보수와 확장성을 고려하여, 상태와 동작을 명확히 나누는 방식으로 설계
- 개인적으로 특히 단일 책임 원칙을 많이 사용해서 이들을 잘 조합해서 컴포넌트화 하여 사용

## 싱글톤 패턴에 대해..

전역 변수를 사용하지 않고 객체를 하나만 생성 하도록 하며, 생성된 객체를 어디에서든지 참조할 수 있도록 하는 패턴
[[Design Pattern] 싱글턴 패턴이란 - Heee's Development Blog](https://gmlwjd9405.github.io/2018/07/06/singleton-pattern.html)
애플리케이션에서 단 하나의 인스턴스만 생성되도록 보장하는 디자인 패턴.

```jsx
class Singleton {
  constructor() {
    if (!Singleton.instance) {
      Singleton.instance = this;
    }
    return Singleton.instance;
  }
}
```

사용 이유

- 설정값, 전역 상태, 캐시 등 공통된 자원에 접근할 때 유용
- 한 번만 초기화되어 리소스 낭비를 줄임

## 가변(Mutable) 객체와 불변(Immutable) 객체의 차이는?

- 가변 객체: 값이 직접 수정됨 (예: `arr.push(4)`)
- 불변 객체: 수정 시 새로운 객체를 반환함 (예: `concat`, spread)

## JavaScript에서 불변 객체의 예는?

- `String`, `Number`, `Boolean`, `BigInt`, `Symbol` 등 기본형(primitive type)은 불변성 유지
- 배열/객체는 기본적으로 가변형이므로, 불변 구조를 직접 구현하거나 라이브러리(Redux 등)를 통해 관리해야 함

## 불변 객체를 사용할 때의 장단점은?

장점

- 사이드 이펙트 방지
- 예측 가능한 코드 흐름
- 변경 감지(리액트의 상태 관리 등)에 유리

단점

- 성능 이슈: 대량의 객체 복사 발생
- 문법적으로 불편할 수 있음 → Immutable.js, Immer 같은 라이브러리 활용

## 코드에서 불변성을 어떻게 구현하나요?

- 전개 연산자(`...`) 사용
  - `const newObj = { ...oldObj, key: 'value' };`
- `Object.freeze()` 로 동결
- Immer, Immutable.js 등 라이브러리 사용

## Compose, Pipe는 무엇인가요?

- Compose: 함수들을 오른쪽 → 왼쪽으로 실행 (함수 조합)
- Pipe: 함수들을 왼쪽 → 오른쪽으로 실행

```jsx
// 예시 (Ramda)
const add = (x) => x + 1;
const multiply = (x) => x * 2;

const composed = R.compose(multiply, add); // multiply(add(x))
const piped = R.pipe(add, multiply); // multiply(add(x))
```

## Ramda, Lodash 등 함수형 라이브러리 써본 경험 있나요?

- Ramda의 `compose`, `pipe`, `curry` 등 순수 함수 조합 기능을 상태 변경 없는 데이터 흐름 처리에 사용
- Lodash의 `cloneDeep`, `debounce`, `throttle`, `get` 등을 자주 사용
- 개인적으로 주로 불변성 유지를 위해 Lodash는 많이 활용했었음.
