# Hooks

## 훅(Hooks)이란?

React 16.8부터 도입된 기능으로, 함수형 컴포넌트에서 상태 관리나 생명주기 처리를 가능하게 해주는 API들. (`useState`, `useEffect`, `useContext` 등)

## 훅을 사용할 때 지켜야 할 규칙은?

- 최상위에서만 호출 (조건문, 반복문 안 ❌)
- 함수형 컴포넌트나 커스텀 훅에서만 사용

## 훅(Hooks)이 클래스 컴포넌트의 모든 기능을 대체할 수 있나요?

거의 대부분 가능함. 생명주기, 상태, context, 에러 처리 등 모두 지원.
단, componentDidCatch는 아직 Hook으로 직접 대체 불가 → ErrorBoundary는 여전히 필요.

## 컴포넌트가 렌더링되지 않도록 하려면?

- 조건부 렌더링 사용: `return null`
- 또는 `React.memo`로 props 변경 없을 시 렌더 방지 가능
- `shouldComponentUpdate`는 클래스형 전용

## `useReducer` 훅이란 무엇이며, 어떻게 사용하는지 설명해주세요.

`useReducer`는 상태 관리 로직이 복잡하거나 상태 간 연관이 있을 때 사용하는 훅.`reducer` 함수와 `dispatch`를 사용해 상태를 업데이트하며, Redux의 reducer 방식과 유사.

## `useState`와 `useReducer`는 어떻게 비교할 수 있나요?

`useState`는 단순한 상태에 적합하고, `useReducer`는 복잡한 상태 업데이트나 조건 분기, 여러 상태를 함께 관리할 때 유리. 예: 폼 상태, 상태 트랜지션 등.

## state 변경을 감지하려면 어떻게 하나요?

함수형에서는 `useEffect(() => { ... }, [state])`로 감지 가능.

## Context란 무엇인가요?

전역적으로 값을 공유하기 위한 React의 내장 API. 여러 컴포넌트에서 prop 없이도 데이터를 전달할 수 있음.

## Consumer란?

- Context의 값을 읽기 위해 사용하는 컴포넌트.
- 함수형에서는 `useContext` 훅으로 대체됨.

## `useContext` 훅을 사용할 때 context는 어떻게 동작하나요?

`useContext`는 Context 객체를 인자로 받아 현재 컴포넌트에서 Context 값을 바로 사용할 수 있게 해줌. 상위 트리에서 `Provider`가 전달한 값을 가져옴.

## `useContext` 훅은 보통 어떤 상황에서 사용하나요?

전역적으로 접근이 필요한 상태(예: 로그인 정보, 테마, 언어 설정 등)를 전달할 때 사용. (props drilling을 피할 수 있어 코드가 깔끔해지기 때문)

## Context 사용 시 발생할 수 있는 성능 문제는 어떻게 해결하나요?

- Context value가 변경되면 하위 모든 컴포넌트가 리렌더됨.
- 해결 방법:
  - `value`는 memoization (`useMemo`) 처리
  - context 분리
  - 필요 시 `selector` 패턴 (예: `useContextSelector` 라이브러리) 도입
  - 일반적으로 상태관리 라이브러리 많이 사용

## useMemo와 useCallback의 차이점은? 언제 사용하는가?

useMemo는 값을 메모이제이션하고, useCallback은 함수를 메모이제이션.
공통점은 의존성 배열을 기반으로 연산 결과를 캐싱해 불필요한 재계산을 방지하는 데 있고, 차이점은 리턴 타입이 useMemo는 값, useCallback은 함수라는 것.
성능 최적화가 필요한 컴포넌트, 특히 불필요한 렌더링을 방지하거나 props로 콜백을 넘겨줄 때 유용

## 커스텀 훅(Custom Hook)은 언제 만들고 어떻게 구성하나요?

- 로직 재사용이 필요할 때
  - 예: 폼 처리, 로딩 상태 관리, 디바운싱 등.
- 일반적으로 `use`로 시작하는 함수 이름을 사용하고, 내부에서 다른 훅들을 조합하여 하나의 역할 단위로 추상화. 구조적으로는 훅 + 상태 + 반환값의 형태로 구성하는 것이 일반적

## useRef는 DOM 접근 외에 어떤 용도로 사용할 수 있나요?

렌더링 사이에서 유지되어야 하는 값을 저장할 때 사용 가능

- 예: 이전 값 저장, 타이머 ID 저장, 외부 라이브러리 인스턴스 참조, 마운트 여부 체크 등
- 특징은 값을 변경해도 컴포넌트를 리렌더링하지 않는다는 점

## useEffect cleanup 함수는 언제 호출되나요?

- 컴포넌트가 언마운트될 때
- 의존성 배열의 값이 바뀌어서 effect가 다시 실행되기 직전

# 비동기 작업 중 컴포넌트가 언마운트되었을 때 어떻게 처리하나요?

- 비동기 작업을 시작한 후 컴포넌트가 언마운트되면, 작업 완료 시점에 `setState()`를 호출할 수 없어 memory leak 경고가 발생할 수 있음.
- 이를 방지하기 위해 `useRef`로 isMounted 여부를 체크하거나, AbortController를 활용해 fetch를 취소.

## useLayoutEffect와 useEffect의 차이는?

- `useEffect`는 브라우저가 화면을 그린 후 실행됨
- `useLayoutEffect`는 DOM이 변경된 직후, 페인팅 전에 실행됨.
  - `useLayoutEffect`는 레이아웃 측정, 동기적인 DOM 조작이 필요한 경우에 사용해야 하며, 그렇지 않으면 깜빡임이 발생할 수 있음
  - 예시
    - 요소 위치를 측정해서 그에 따라 레이아웃을 조절할 때
    - 스크롤 위치 강제로 조정 (`useEffect`는 렌더 후 실행되므로, 이미 화면이 깜빡이고 난 후라 늦음)

기본적으로는 `useEffect`를 사용하고, 렌더 타이밍이 민감할 때만 `useLayoutEffect`를 사용.

## 동일한 상태를 여러 컴포넌트에서 공유할 때 어떤 방법을 사용하는가?

1. Context API + useContext: 글로벌한 상태 공유에 적합. 예: 로그인 정보, 테마 등.
2. 전역 상태 라이브러리: Redux, Zustand, Jotai 등에서 공유 상태 관리.
3. 상위 컴포넌트로 lifting 후 props로 전달: 구조가 단순할 때 효과적.

- 상황에 따라 성능, 구조, 유지보수성을 고려해 선택

## 컴포넌트를 1초마다 업데이트하려면 어떻게 하나요?

`setInterval`을 `useEffect` 안에서 설정하고, cleanup 함수로 `clearInterval` 해줘야 메모리 누수 방지 가능.

```tsx
useEffect(() => {
  const interval = setInterval(() => {
    setCount((c) => c + 1);
  }, 1000);
  return () => clearInterval(interval);
}, []);
```

## AJAX 호출은 어떻게 하고, 어느 시점에서 해야 하나요?

함수형 컴포넌트에선 `useEffect` 안에서 호출. 클래스형은 `componentDidMount`
개인적으로 보통 react-query 사용했기 때문에 컴포넌트와 분리해서 로직 설정 후, 컴포넌트 최상단에서 훅 호출하듯이 호출해서 사용.
