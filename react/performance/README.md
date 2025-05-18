# 성능

## Concurrent Rendering이란?

React가 UI 업데이트를 중단/재시도하면서 사용자 응답성을 높이는 기능
→ React 18부터 기본 탑재된 기능 (Transition, startTransition 등)

## Async Mode vs Concurrent Mode 차이점은?

과거 React에서 실험적으로 도입된 async mode는 중단됨.
현재는 Concurrent Mode로 통합되어, 업데이트를 병렬 처리하고 우선순위 제어 가능

## React Server Component란?

서버에서 렌더링되어 클라이언트 JS 없이 UI 일부를 구성하는 컴포넌트.

- 번들 사이즈 감소, 성능 향상
- Next.js App Router에서 사용됨

## React에서 hydration이란?

SSR로 전달된 HTML을 클라이언트가 React로 연결(sync)하는 과정. → 초기 렌더 속도 향상, SEO 개선

## 코드 스플리팅이란?

필요한 시점에 필요한 코드만 로딩하여 초기 로딩 속도를 개선하는 기법.
React에서는 React.lazy, Suspense, dynamic import를 통해 구현 가능

## React는 상태 업데이트를 어떻게 batching(묶음 처리)하나요?

React는 이벤트 핸들러, lifecycle 등에서 발생한 여러 setState 호출을 한 번에 처리함으로써 불필요한 렌더링을 방지

## 자동 batching을 막을 수 있나요?

React 18에서는 자동 batching이 기본이지만, `flushSync()`로 수동 처리 가능

```tsx
import { flushSync } from 'react-dom';
flushSync(() => setState(...));

```

## 컴포넌트 내부에 또 다른 함수형 컴포넌트를 정의하면?

렌더링될 때마다 새로 생성되므로 불필요한 리렌더링 발생 가능성 → 컴포넌트 외부로 분리하거나 useCallback으로 메모이제이션 고려

## windowing 기법이란?

리스트의 일부만 렌더링해서 성능을 높이는 기술.

- 예: react-window, react-virtualized
- 스크롤 위치에 따라 필요한 요소만 렌더링
