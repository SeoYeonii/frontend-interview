# 일반

## React란 무엇이고 주요 특징은 무엇인가요?

React는 UI(User Interface)를 만들기 위한 JavaScript 라이브러리. 컴포넌트 기반 구조로 재사용성을 높이고, 선언형(Declarative) 방식으로 코드를 작성할 수 있어 유지보수가 쉬움. Facebook에서 개발했으며 가상 DOM(Virtual DOM) 을 통해 성능 최적화.

- JSX: JavaScript 안에서 HTML처럼 문법 작성
- 컴포넌트 기반 구조: 재사용성과 분리된 책임 부여
- Virtual DOM: 변경 사항만 업데이트해 렌더링 성능 향상
- 단방향 데이터 흐름: 예측 가능한 상태 관리
- Hooks: 함수형 컴포넌트에서도 상태와 생명주기 활용 가능

## React는 화면을 어떻게 업데이트하나요?

- state/props 변경
- Virtual DOM → diff → 최소 DOM 수정 → 효율적인 리렌더링 수행

## React는 어떤 브라우저를 지원하나요?

React는 대부분의 현대 브라우저를 지원함.
IE11은 더 이상 지원되지 않으며, React 18부터 공식적으로 IE 지원 종료.

## Element와 Component의 차이는 무엇인가요?

- Element: React 엘리먼트는 DOM 요소의 불변 객체로, UI의 스냅샷을 의미. JSX의 반환값이며 단순히 `React.createElement()`로 생성된 객체
- Component: UI를 만들기 위한 함수 또는 클래스. props와 state를 사용해 엘리먼트를 반환 (엘리먼트를 반환하는 함수)

## 브라우저는 JSX 코드를 이해하나요?

브라우저는 JSX를 직접 실행할 수 없음. Babel 등을 통해 React.createElement()로 변환되어야 동작함.

## JSX에서 여러 태그를 감싸야 하는 이유는?

JSX는 하나의 요소만 반환 가능하므로, 여러 요소는 <div> 또는 <>...</>로 감싸야 함. → Fragment로 불필요한 DOM 생성 없이 처리 가능

## JSX 없이 React를 사용할 수 있나요?

- 가능함. JSX는 syntactic sugar일 뿐이고, 실제로는 `React.createElement()` 호출로 변환됨

```tsx
React.createElement("div", null, "Hello");
```

- 하지만 JSX가 훨씬 가독성 좋고 생산성 높음

## JSX는 어떻게 XSS 같은 인젝션 공격을 방지하나요?

JSX는 내부적으로 값이 삽입될 때 HTML 이스케이프 처리를 하기 때문에 XSS 공격에 안전함.
단, dangerouslySetInnerHTML 사용 시는 직접 sanitize 필요.

## 컴포넌트 생명주기의 단계는 어떻게 되나요?

| 생명주기 단계    | 클래스형 메서드            | 함수형 대응 방식 (Hooks 기반)                 |
| ---------------- | -------------------------- | --------------------------------------------- |
| 마운트 전        | `constructor`              | `useState` / 초기값 설정                      |
| 마운트 직후      | `componentDidMount`        | `useEffect(() => { ... }, [])`                |
| 업데이트 시      | `componentDidUpdate`       | `useEffect(() => { ... }, [deps])`            |
| 언마운트 시      | `componentWillUnmount`     | `useEffect(() => { return () => {...} }, [])` |
| 상태 파생        | `getDerivedStateFromProps` | 자체 구현 or 상태 관리 방식 변경              |
| 렌더링 전 스냅샷 | `getSnapshotBeforeUpdate`  | 따로 제공되지 않음 (거의 사용 안 함)          |

- 클래스 컴포넌트는 라이프사이클 메서드가 명확하게 구분돼 있음
- 함수형 컴포넌트는 `useEffect` 하나로 다양한 시점을 커버하기 때문에, 오히려 더 유연

## React의 라이프사이클 메서드에는 어떤 것들이 있나요?

클래스형 기준으로 `componentDidMount`, `componentDidUpdate`, `componentWillUnmount` 등이 있고, 함수형에서는 `useEffect`, `useLayoutEffect`로 대체됨.

## 클래스 컴포넌트를 함수형 컴포넌트보다 언제 사용하나요?

과거에는 상태관리나 생명주기 기능을 위해 클래스 컴포넌트를 사용했지만, 이제는 Hook을 통해 함수형 컴포넌트에서도 동일한 기능을 구현할 수 있으므로 특별한 이유가 없다면 함수형을 권장.

## constructor에서 `setState`를 호출하면 무슨 일이 일어나나요?

경고 없이 무시되며, 초기 state는 `this.state = {}`로만 설정해야 함. constructor에서는 setState 사용 금지.

- `constructor()`는 React lifecycle 전에 호출되는 JavaScript 클래스 초기화 단계. 이 시점엔 React가 컴포넌트의 상태 관리(setState 등)를 아직 연결하지 않았기 때문에, `setState()`를 호출해도 React가 그것을 감지하지 못하고 무시

## `super(props)`를 사용하는 이유는 무엇인가요?

클래스형 컴포넌트에서 `this.props`에 접근하기 위해 반드시 `super(props)` 호출 필요.

- React 컴포넌트는 `React.Component`를 상속(inheritance) 해서 만들기 때문에 자식 클래스에서 `constructor`를 정의하면, 반드시 `super()`를 먼저 호출해야 `this`를 사용할 수 있음.
- `super(props)`는 부모 클래스인 `React.Component`의 생성자를 호출하면서 props를 초기화해주는 역할을 함.

## React에서 state와 props

state는 컴포넌트의 내부 데이터로, 사용자 인터랙션 등에 따라 값이 변경되며 컴포넌트의 리렌더링을 유발

props는 부모 컴포넌트가 자식 컴포넌트에게 데이터를 전달할 때 사용하는 읽기 전용 객체

- props는 외부에서 주어지는 읽기 전용 데이터이고, state는 컴포넌트 내부에서 관리되는 변경 가능한 데이터

## 왜 state를 직접 수정하면 안 되나요?

React는 `setState`를 통해 상태 변경을 감지하고 리렌더링을 수행하기 때문에, 직접 state를 수정하면 변경이 감지되지 않고 UI가 동기화되지 않을 수 있음.

## 동적인 키 이름으로 state를 설정하려면 어떻게 하나요?

ES6의 computed property를 활용하여 `this.setState({ [key]: value })` 형태로 사용.

## `setState`의 콜백 함수는 왜 사용하나요?

상태 업데이트가 비동기이기 때문에, 상태 변경 후 로직이 필요할 경우 콜백을 통해 처리함.

## 이전 state를 기반으로 새 state를 계산할 때는 어떻게 하나요?

React의 상태 업데이트는 비동기적이고 batching 처리되기 때문에, 이전 상태를 기반으로 새로운 상태를 계산해야 할 때는 반드시 함수형 업데이트를 사용하는 것이 안전

## 초기 state를 설정할 때 props를 사용하면 어떤 일이 일어나나요?

가능하지만 비추천. props가 변경돼도 초기 state는 유지되므로 props와 state가 비동기화되는 문제가 발생할 수 있음.

## Prop Drilling이란?

부모 → 자식 → 손자 식으로 중간 컴포넌트가 필요 없는 props를 계속 전달하는 현상

→ Context나 상태 관리 라이브러리로 해결 가능

## defaultProps란 무엇인가요?

컴포넌트에 props가 전달되지 않았을 때 사용할 기본값을 지정하는 방법.
함수형에서는 defaultProps 대신 함수 파라미터의 기본값을 사용하는 것이 일반적.

## `ref`는 어떤 용도로 사용되나요?

DOM 요소에 직접 접근하거나 포커스, 스크롤, 서드파티 라이브러리 연동 시 사용.

## `ref`는 어떻게 생성하나요?

`useRef()` 또는 `createRef()` 사용. 함수형 컴포넌트는 `useRef`, 클래스형은 `createRef`.

## inline ref 함수는 왜 비추천되나요?

렌더링마다 새로운 함수가 생성되기 때문에, 불필요한 리렌더링이나 성능 저하 발생 가능성 있음.
가능하면 useRef를 활용하거나 함수 정의를 고정해서 사용.

## 컴포넌트 라이브러리에서 `forwardRef`를 사용할 때 추가 주의가 필요한 이유는?

- 라이브러리 사용자 입장에서 ref 사용 시 예상대로 동작하지 않을 수 있음 (예: 버튼 내부 span에 ref 연결됨)
- 내부 구조가 바뀌면 ref 타겟도 바뀔 수 있어 ref가 깨지기 쉬움
- 해결: 명확한 문서화 또는 필요한 DOM에만 ref 노출

## 캡처링 단계 이벤트란?

이벤트가 타깃 요소에 도달하기 전 상위 요소에서 먼저 감지되는 단계.
React에서는 onClickCapture와 같이 사용

## React에서 클릭 이벤트를 코드로 발생시키려면?

`ref`를 이용해서 DOM 요소에 접근 후 `ref.current.click()` 호출

## 이벤트 핸들러에는 왜 error boundary가 필요 없나요?

이벤트 핸들러 내부 오류는 React 렌더 트리 밖에서 발생하므로, try##catch로 직접 핸들링 가능.

Error Boundary는 렌더링 과정, lifecycle, constructor 내 오류만 잡음

## 함수가 여러 번 호출되는 걸 어떻게 막나요?

- 디바운싱 (`lodash.debounce`, `useDebounce`)
- 조건문으로 중복 호출 제어
- 클릭 중복 방지용 `disabled` 상태 처리 등

→ 상황에 따라 UX 기반 전략 필요

## try/catch와 error boundary는 어떻게 다른가요?

- `try/catch`: 동기 코드에서 사용하는 일반 JS 예외 처리
- `ErrorBoundary`: React 렌더링 중 발생하는 에러를 잡고 fallback UI를 보여줌

## `forwardRef`란 무엇인가요?

부모 컴포넌트가 자식 컴포넌트 내부 DOM에 접근할 수 있도록 `ref`를 전달하는 방식. 고급 컴포넌트 재사용 시 유용.

## `forwardRef`를 React DevTools에서 어떻게 디버깅하나요?

- React DevTools에서 `ForwardRef`라는 컴포넌트로 표시됨.
- 컴포넌트 이름을 명시적으로 설정하면 디버깅이 더 쉬움:

```tsx
const MyInput = React.forwardRef((props, ref) => <input ref={ref} />);
MyInput.displayName = "MyInput";
```

## string ref는 왜 레거시로 간주되나요?

문자열 ref는 성능 및 예측성 이슈로 비추천되며, 함수형 또는 `useRef` 방식이 권장됨.

## forwardref 안쓰고 그냥 ref 전달하면 왜 안되나요?

함수형 컴포넌트일 경우 React는 ref를 일반 props로 전달하지 않음.

단 ref말고 이름 바꿔서 props로 보내받아서 `ref`로 수동 연결은 가능

- React의 `ref` 시스템(예: `useRef`, `ref.current`)과 통합되려면 forwardRef가 필요
- 외부 라이브러리와 통합하거나, `ref`를 generic하게 다룰 땐 forwardRef를 안 쓰면 확장성 떨어짐

## HTML과 React의 이벤트 처리 방식 차이는?

HTML은 소문자 이벤트명(`onclick`)을 사용하고 문자열로 핸들러를 지정하지만, React는 `camelCase`(`onClick`)로 이벤트명을 지정하고 함수 레퍼런스를 넘김

- HTML
  - 값은 문자열로 지정 → 브라우저가 이 문자열을 함수처럼 평가(eval) 함
  - 보안/성능/유지보수 측면에서 불리함
- React
  - JavaScript에서 속성명을 camelCase로 쓰는 것이 관례이고, React는 JS 안에서 이벤트를 다루기 때문
  - 값은 함수 레퍼런스를 직접 넘김 → 안전하고 효율적
  - React는 내부적으로 `addEventListener`가 아닌 자체 Synthetic Event 시스템을 사용
    - 이벤트 버블링 처리, 이벤트 풀링, 크로스 브라우징 처리를 위해
    - 그래서 DOM과는 다르게 자체적으로 이벤트를 추상화함

## JSX에서 이벤트 핸들러를 바인딩하려면 어떻게 하나요?

`this.handleClick = this.handleClick.bind(this)` 또는 화살표 함수 사용. 클래스 컴포넌트에서 주로 필요함.

## React의 Synthetic Event란?

React가 자체적으로 만든 이벤트 래퍼 객체로, 브라우저 간의 이벤트 차이를 추상화해 일관된 API를 제공

- 이벤트 버블링 처리, 이벤트 풀링, 크로스 브라우징 처리를 위해
- 그래서 DOM과는 다르게 자체적으로 이벤트를 추상화함

## JSX에 함수를 괄호 열고 호출하는 형태로 작성했을 때 일어나는 일은?

예: `onClick={handleClick()}` → 이러면 즉시 실행됨

handleClick() → 함수 실행 결과를 onClick에 전달

즉, 렌더링 시점에 함수가 바로 호출되고, 반환된 값이 이벤트 핸들러로 등록됨. 근데 대부분의 경우 `handleClick()` 함수는 아무것도 반환하지 않거나 `undefined`를 반환하니까, 클릭해도 아무 일도 안 일어나거나 예상과 다르게 동작

## key prop은 무엇이고, 배열 렌더링 시 사용하는 이유는?

key는 각 엘리먼트가 고유함을 식별하는 값으로, 리스트를 렌더링할 때 성능 최적화와 정확한 UI 업데이트를 위해 사용.
key는 React가 어떤 요소가 변경/추가/삭제되었는지 식별할 수 있도록 도와주는 고유값. → virtual DOM diffing 알고리즘에서 중요한 힌트 역할

## key로 index를 안전하게 사용할 수 있는 조건은?

보통 안 사용하는 이유:

- 항목의 순서나 내용이 바뀌었을 때 오작동
  - index는 순서 기반이라서 항목의 삽입/삭제/정렬이 생기면 key가 바뀜
  - React는 key가 같으면 같은 컴포넌트라고 판단해서 재사용하는데, 그게 달라지면 렌더링 결과가 잘못될 수 있음

안전하게 사용될 수 있는 조건:

- 리스트가 정적이고 순서가 바뀌지 않을 때
- 고유 id가 없고, 리스트 항목이 재정렬/추가/삭제되지 않을 때만

## Virtual DOM이란 무엇이고 어떻게 동작하나요?

React에서 사용하는 가상의 DOM 트리로, 실제 DOM 변경 전 메모리 상에서 UI를 계산하여 효율적인 변경만 반영(실제 변경된 것만 반영). 변경 사항을 최소화하여 브라우저 성능을 최적화

컴포넌트가 업데이트되면 새로운 Virtual DOM을 만들고, 이전 Virtual DOM과 비교(Diffing). 변화가 감지된 최소 단위만 실제 DOM에 반영.

## Shadow DOM과 Virtual DOM의 차이는?

- Virtual DOM은 React에서 사용하는 개념으로 성능 최적화를 위해 실제 DOM과 별도로 관리되는 가상의 DOM
- Shadow DOM은 웹 컴포넌트의 캡슐화를 위한 브라우저 기술로, 스타일과 DOM을 외부로부터 격리

## React Fiber와 주요 목적은?

React의 새로운 렌더링 엔진.

기존 React(React 15 이하)는 재귀 호출 방식으로 렌더 트리를 동기적으로 처리함.

- 컴포넌트가 많거나 복잡한 트리가 있으면 브라우저를 블로킹하는 일이 생김

그래서 파이버 아키텍쳐를 이용해 동기적으로 처리되던 작업을 잘게 쪼개서 비동기적으로 실행할 수 있도록 설계되어 렌더링 성능과 유연성이 향상됨.

- 우선순위 기반의 작업 스케줄링
  - 특히 긴 작업을 나눠서 브라우저가 더 빠르게 사용자 인터랙션을 처리할 수 있도록 함(모니터 주사율에 맞춰서)
- 중단 가능한 렌더링
- UI 응답성 향상.

Fiber의 처리과정

1. Reconciliation (재조정)(비동기 가능) → 어떤 노드가 변경됐는지 비교
2. Work Loop → 작업 단위를 하나씩 꺼내서 처리 (중간에 yield 가능)
3. Commit Phase (반드시 동기)→ 변경 사항을 DOM에 실제로 반영

## Controlled Component, Uncontrolled Component

- Controlled Component: 폼 요소의 값이 state에 의해 제어되는 컴포넌트. value와 onChange를 state와 연결하여 사용자의 입력을 직접 제어할 수 있음. (입력값 체크 필요할 때 등)

- Uncontrolled Component: 폼 요소의 값을 DOM이 직접 관리하는 방식으로, React state가 아닌 ref 등을 통해 값을 읽고 설정. (성능: 매 입력마다 상태 변경 (`setState`)가 없으므로 리렌더링이 발생하지 않음)

## Lifting State Up이란?

여러 컴포넌트가 공통 데이터를 사용할 때, 그 상태(state)를 공통 부모 컴포넌트로 끌어올리는 패턴. 하위 컴포넌트는 props를 통해 상태를 공유

## props proxy란?

HOC에서 전달받은 props를 하위 컴포넌트에 그대로 전달하거나 가공해서 WrappedComponent에 넘기는 패턴. 이때 props를 프록시(proxy)처럼 중간에서 가로채서 필요한 작업을 할 수 있음.

- 사용하는 이유
  - 공통 로직을 재사용할 수 있음
  - 컴포넌트를 수정하지 않고 동작을 확장 가능
  - 원래 컴포넌트를 건드리지 않고, HOC에서 props를 가로채 필요한 데이터를 추가하거나 변경 가능
  - 조건부 렌더링이나 래핑 가능

## React에서 데코레이터를 어떻게 사용하나요?

Babel 플러그인을 통해 지원 가능하며, 보통 HOC를 간단하게 표현할 때 사용함. ex: `@connect(...)`

## render hijacking이란?

HOC 등에서 렌더 결과를 가로채거나 수정하는 패턴.

- 예전에는 많이 썼지만 지금은 주로 Hook이나 Composition으로 대체.

## `displayName` 속성의 목적은?

React DevTools에서 컴포넌트 이름을 명확하게 표시하기 위한 설정.
HOC 사용 시 원래 컴포넌트 이름 유지에 유용함.

## 고차 컴포넌트(Higher-Order Component)란?

컴포넌트를 인자로 받아 새로운 컴포넌트를 반환하는 함수입니다. 공통 로직을 재사용하는 데 활용됨

## 고차 컴포넌트(HOC)에서 props proxy는 어떻게 구성하나요?

HOC 내부에서 받은 props를 하위 컴포넌트에 그대로 전달하거나, 일부 수정해서 넘기는 방식. `return <WrappedComponent {...props} />`

## HOC(고차 컴포넌트)의 한계는 무엇인가요?

- Wrapper hell: 중첩이 깊어지면 디버깅이 어려움
- ref 전달 어려움: 일반적으로 ref는 전달되지 않음 → `forwardRef` 필요
- props 충돌 위험: 내부 HOC가 사용하는 prop과 이름이 겹칠 수 있음

  - 요즘은 HOC보다 Hooks나 Composition 방식 선호

## Reconciliation이란?

React가 Virtual DOM을 통해 변경된 부분을 찾아 실제 DOM에 반영하는 과정. 효율적인 업데이트를 위해 최소 변경만 수행.

## diffing 알고리즘이란?

가상 DOM에서 이전과 이후의 트리를 비교(diff)하여 변경된 최소 DOM 조작만 수행하는 알고리즘. React는 이 과정을 통해 성능 최적화함.

## React의 diffing 알고리즘이 따르는 규칙은?

- DOM 노드는 같은 타입일 때만 비교
- key가 다른 리스트 항목은 새로운 것으로 간주
- 재귀적으로 하위 노드를 비교
  - 최소 DOM 변경으로 최적화

## React는 왜 class 대신 className을 사용하나요?

`class`는 JavaScript의 예약어이기 때문에, JSX에서는 HTML 클래스 속성을 `className`으로 대체

## Fragments란?

여러 요소를 감싸되 DOM에 별도의 노드를 추가하지 않는 컴포넌트. `<></>` 또는 `<React.Fragment>`로 사용. 키가 필요할 땐 후자쓰고 키 필요없으면 간단히 전자 사용.

DOM 구조를 불필요하게 복잡하게 만들지 않으므로 렌더링 성능과 시멘틱 구조를 개선. 스타일이나 레이아웃에도 영향을 덜 줌

## Stateless components, Stateful components

- Stateless components: 자신의 state를 가지지 않고 props만 받아서 렌더링하는 컴포넌트.

- Stateful components: 내부에 state를 가지고 있으며 상태 변화에 따라 렌더링 결과가 달라지는 컴포넌트. 주로 클래스 컴포넌트 또는 Hook이 사용된 함수형 컴포넌트가 해당됨

## React의 장점, 단점

- 장점: 컴포넌트 기반 구조, Virtual DOM으로 인한 빠른 렌더링, 재사용성, 대규모 커뮤니티 및 생태계, JSX

- 단점: 초기 설정 복잡성, 학습 곡선, 상태 관리 라이브러리 필요성, 빠른 생태계 변화로 인한 유지보수 부담

## Real DOM vs Virtual DOM 차이?

- Real DOM: 실제 브라우저에 그려지는 DOM
- Virtual DOM: React가 메모리 상에 유지하는 가상 DOM
  - 변경 사항만 Real DOM에 반영하여 성능 최적화

## react-dom 패키지의 용도는?

React 컴포넌트를 실제 DOM에 마운트하거나 업데이트하는 기능을 제공. 예: `ReactDOM.render(<App />, document.getElementById('root'))`

## ReactDOMServer란?

서버 사이드 렌더링(SSR)을 지원하는 React의 기능으로, 컴포넌트를 HTML 문자열로 변환하여 서버에서 클라이언트로 전송할 수 있게 해줌

## React에서 dangerouslySetInnerHTML을 사용하는 방법은?

XSS 위험이 있지만 HTML 문자열을 직접 삽입하고 싶을 때 사용

예: `<div dangerouslySetInnerHTML={{ __html: '<p>Hello</p>' }} />`

## React에서 스타일을 적용하는 방법은?

- 인라인 스타일 객체 (`style={{ color: 'red' }}`)
- CSS 클래스 (`className="my-class"`)
- CSS Modules
- Styled-components 등 CSS-in-JS

## React에서 이벤트 처리 방식은 HTML과 어떻게 다른가요?

React는 camelCase(`onClick`)를 사용하며, 이벤트 핸들러는 문자열이 아닌 함수로 전달. 이벤트는 SyntheticEvent로 추상화되어 cross-browser 호환성을 보장

## 배열 렌더링 시 key로 index를 사용하는 것의 영향은?

리스트의 순서가 변경될 경우 성능 저하 및 불필요한 리렌더링이 발생할 수 있음. 고유하고 안정적인 값이 key로 사용되어야 함.(배열의 index를 키로 쓰면 warning도 뜸)

## props를 DOM 요소에 spread할 때 주의해야 하는 이유는?

불필요한 props가 HTML 속성으로 전달되면 경고가 발생하거나 렌더링 오류가 생길 수 있으므로, 필요한 props만 명시적으로 전달하는 것이 좋음

## React에서 컴포넌트를 메모이제이션(memoization)하려면 어떻게 하나요?

`React.memo(Component)`로 감싸거나, `useMemo`를 사용하여 컴포넌트 또는 계산 값을 캐시하여 리렌더링을 방지할 수 있음

## 서버 사이드 렌더링(SSR)을 어떻게 구현하나요?

`ReactDOMServer.renderToString()`으로 컴포넌트를 문자열로 변환 후 HTML에 삽입하여 클라이언트에 전달.
개인적으로 사용해보지는 않음. Next.js와 같은 프레임워크를 사용하면 SSR을 쉽게 구현할 수 있음.

## React의 production 모드는 어떻게 활성화하나요?

빌드 시 `NODE_ENV=production` 설정을 통해 활성화됨. `create-react-app` 등에서는 `npm run build`로 자동 설정

## Hooks는 render props나 고차 컴포넌트를 대체하나요?

✅. `useState`, `useEffect`, `useContext` 등의 Hook은 로직 재사용을 위해 render props나 HOC보다 간결한 대안으로 사용됨

## 컴포넌트 이름이 대문자로 시작해야 하는 이유는 무엇인가요?

React는 소문자로 시작하는 태그를 HTML 태그로 간주하므로, 사용자 정의 컴포넌트를 구분하려면 반드시 대문자로 시작해야 함

## React v16에서 커스텀 DOM 속성을 지원하나요?

✅. React v16부터는 `data-*`, `aria-*` 외에도 알려지지 않은 커스텀 속성도 DOM에 그대로 전달됨.

## React와 ReactDOM의 차이는 무엇인가요?

`react`는 컴포넌트 선언과 렌더링 로직을 제공하고, `react-dom`은 실제로 브라우저 DOM에 마운트하거나 조작하는 기능을 제공.

## ReactDOM이 React에서 분리된 이유는 무엇인가요?

플랫폼 독립성과 재사용성을 높이기 위해 UI 렌더링 로직(`react-dom`)과 핵심 로직(`react`)을 분리. 이로 인해 React Native 등 다른 플랫폼과의 통합도 용이해졌음

## `react-dom`의 `render()` 메서드 목적은?

React 요소를 실제 DOM에 마운트하는 역할. `ReactDOM.render(<App />, document.getElementById('root'))`

## 브라우저 크기 조정 시 뷰를 다시 렌더링하려면 어떻게 하나요?

`resize` 이벤트를 `useEffect`로 감지하고 상태를 변경하여 리렌더링을 유도. `useState`와 `useEffect` 조합을 주로 사용.

## React에서 props는 왜 직접 수정할 수 없나요?

React의 단방향 데이터 흐름 원칙에 따라 부모 컴포넌트에서 내려준 props는 자식에서 변경할 수 없음. 상태는 state로 관리해야 함.

## react-router에서 Google Analytics를 추가하려면 어떻게 하나요?

라우터 변경 시 GA 이벤트를 전송하도록 `useEffect`와 `useLocation()`을 함께 사용. 예: `ReactGA.pageview(location.pathname + location.search)`.

## 기본 React에서도 async/await를 사용할 수 있나요?

✅. Babel 등의 트랜스파일러가 있는 환경에서는 async/await를 사용할 수 있습니다. 다만 비동기 호출을 직접 `useEffect`에 넣을 땐 함수 내부에서 async 선언이 필요함.

## 스타일 모듈(styles module)의 장점은 무엇인가요?

CSS 클래스명이 컴포넌트 단위로 자동으로 유일하게 생성되므로, 전역 네이밍 충돌을 방지할 수 있음.
또한, 컴포넌트 단위로 스타일을 캡슐화하여 재사용성과 유지보수가 용이해짐

## React에서 인기 있는 린터(Linter) 도구에는 어떤 것들이 있나요?

- ESLint: JS/TS 코드 전반을 분석하여 문제를 사전에 방지
- eslint-plugin-react: JSX 문법과 React best practice 검사
- eslint-plugin-jsx-a11y: 웹 접근성 규칙 검사를 위한 플러그인
- Prettier: 코드 포맷 정리를 위한 포매터, ESLint와 함께 자주 사용

## React.lazy() 란?

React.lazy()는 동적으로 import한 컴포넌트를 Lazy Loading 할 수 있도록 도와주는 함수. 즉, 해당 컴포넌트가 실제로 렌더링되기 전까지 번들에 포함되지 않고, 필요할 때 로드됨.

- React 16.6 이상부터 사용할 수 있음

## Suspense 컴포넌트란?

비동기 컴포넌트 로딩 중 fallback UI를 보여주는 React 컴포넌트.
React.lazy와 함께 사용하거나, 서버 컴포넌트와도 사용됨.

## React v16에서의 에러 바운더리란?

컴포넌트 트리에서 JavaScript 오류를 잡아내고, UI를 대체하여 앱 전체가 crash 되는 걸 방지함. `componentDidCatch`, `getDerivedStateFromError` 사용

## Error Boundary는 어디에 배치하는 것이 적절한가요?

- 페이지 단위나 주요 UI 컴포넌트(위젯, 폼 등) 단위로 감싸는 것이 일반적
- 너무 넓게 또는 너무 세부적으로 나누면 실효성 떨어짐

## React 16에서 잡히지 않은 오류의 동작은?

Error Boundary가 없는 경우, 전체 컴포넌트 트리가 언마운트됨
사용자에게는 흰 화면(Blank Screen)만 보이게 됨

## React v15에서는 에러 바운더리를 어떻게 처리했나요?

공식적인 error boundary 기능이 없어서 try-catch로 처리하거나 외부 도구에 의존해야 했음.

## 어떤 경우에 Error Boundary가 오류를 잡지 못하나요?

- 이벤트 핸들러 내부
- 비동기 코드 (ex. setTimeout, fetch)
- 서버 사이드 렌더링 중
- Error Boundary 자체 내부에서 발생한 오류

## React Strict Mode란?

개발 중 문제를 조기에 감지하기 위한 개발용 툴

- 두 번 렌더링(React는 side effect를 감지하기 위해 일부 생명주기 함수, `useEffect` 등을 의도적으로 두 번 호출함 (개발 환경 한정)), 경고 표시 등 통해 side effect 확인 가능

- 안전하지 않은 코드 감지
- 향후 비동기 렌더링 지원을 위한 준비
- 사용 중인 라이브러리의 안정성 검토에 도움

## CRA(Create React App)는 무엇이며, 장점은?

React 공식 CLI 툴로, 빠르게 설정 없이 개발 환경을 구성할 수 있음. Webpack, Babel, Lint 등이 내장되어 있음. 설정 커스터마이징이 필요없거나 작은 프로젝트에서 설정을 빨리 하고 싶을 때 많이 사용.

- 설정 없는 개발 환경 제공
- 핫 리로딩, 코드 스플리팅, 환경 변수 지원
- `react-scripts`로 실행/빌드/테스트 통합

## CRA 프로젝트에서 폴리필(polyfill)을 추가하는 방법은?

CRA는 Babel과 core-js를 기본 포함하지만, 필요한 경우 core-js, whatwg-fetch, es6-promise 등의 폴리필 패키지를 직접 설치하고 import 해야 함.
또는 react-app-polyfill을 사용하여 주요 브라우저 호환성을 확보할 수 있음.

## CRA에서 http 대신 https를 사용하려면?

`.env` 파일에 `HTTPS=true` 설정하면 개발 서버가 HTTPS로 실행됨

단, 브라우저에서 보안 경고가 뜨지 않게 하려면 로컬 인증서를 추가로 구성해야 할 수 있음.

## CRA에서 상대 경로(`../../components/...`) import를 피하려면?

CRA 3.0 이상에서는 `jsconfig.json` 또는 `tsconfig.json`에서 `baseUrl`을 `src`로 설정하면 절대 경로 import가 가능함. alias 설정 해서 @/~~ 도 가능

```json
{
  "compilerOptions": {
    "baseUrl": "src"
  }
}
```

## `renderToNodeStream()`의 목적은?

- 서버 사이드 렌더링(SSR) 시 HTML을 스트리밍으로 전송할 수 있게 함
- 초기 페이지 로드 성능을 향상시킬 수 있음
- React 18 이후에는 `renderToPipeableStream()`으로 대체됨

## Next.js란? 주요 기능은?

React 기반의 프레임워크로, SSR, SSG, API Routes, File-based Routing, Image 최적화, App Router 등 다양한 기능을 제공함.

- SEO와 성능 모두 고려한 React 개발 가능

## 좋아하는 react stack?

react + typescript + MobX + React Query + StyledComponent + Vite 등등

- typescript: 타입 지정해서 백엔드 개발자와 일할때도 타입 명확하게 인터페이스 제공할 수 있고, 에러도 런타임 이전에 잡아줘서 굉장히 편리.

  - 컴파일 타임 타입 체크
  - 자동완성, 리팩토링 편의성
  - 협업 시 명세 역할

    - 코드 안정성과 유지보수성 향상

- MobX: 관찰 가능한 상태를 기반으로 자동으로 UI를 업데이트해주는 상태 관리 라이브러리. 선언적이면서도 매우 간단하고 직관적. 개인적으로 쉽다고 소문난 zustand등등 보다 더 직관적으로 느낌.
- react query: api 호출할때 관리를 간단한 설정으로 해줌. 게다가 호출 로직을 컴포넌트랑 분리시켜서 컴포넌트도 더 깔끔해짐.
- styledComponent: ``안에 css 그대로 입력해서 컴포넌트 만들기때문에 예를들어 figma 쓴다고 하면 css 바로 가져와서 컴포넌트를 만들 수 있기 때문에 굉장히 편리.
  - CSS-in-JS 은 소규모 프로젝트에 권장되는 방식이나 스타일 적용된 공통 컴포넌트 분리해서 사용하면 크게 저해하지 않아 보임.
- vite: 빌드할 때 빠르기 때문에 배포할 때 조금이라도 더 단축되서 편리
