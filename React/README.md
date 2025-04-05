## 카테고리

- React 기본 개념
- React Router
- Hook
- 성능

## 질문지

### React 기본 개념

| 질문                                                                        |  중요도  |
| :-------------------------------------------------------------------------- | :------: |
| React란 무엇이고 주요 특징은 무엇인가요?                                    | ⭐️ 필수 |
| React는 화면을 어떻게 업데이트하나요?                                       | ✅ 중요  |
| React는 어떤 브라우저를 지원하나요?                                         | 🔍 참고  |
| Element와 Component의 차이는 무엇인가요?                                    | ⭐️ 필수 |
| 브라우저는 JSX 코드를 이해하나요?                                           | 🔍 참고  |
| JSX에서 여러 태그를 감싸야 하는 이유는?                                     | ✅ 중요  |
| JSX 없이 React를 사용할 수 있나요?                                          | 🔍 참고  |
| JSX는 어떻게 XSS 같은 인젝션 공격을 방지하나요?                             | ✅ 중요  |
| 컴포넌트 생명주기의 단계는 어떻게 되나요?                                   | 🔍 참고  |
| React의 라이프사이클 메서드에는 어떤 것들이 있나요?                         | 🔍 참고  |
| 클래스 컴포넌트를 함수형 컴포넌트보다 언제 사용하나요?                      | ✅ 중요  |
| constructor에서 `setState`를 호출하면 무슨 일이 일어나나요?                 | ✅ 중요  |
| `super(props)`를 사용하는 이유는 무엇인가요?                                | ✅ 중요  |
| React에서 state와 props                                                     | ⭐️ 필수 |
| 왜 state를 직접 수정하면 안 되나요?                                         | ⭐️ 필수 |
| 동적인 키 이름으로 state를 설정하려면 어떻게 하나요?                        | ✅ 중요  |
| `setState`의 콜백 함수는 왜 사용하나요?                                     | ✅ 중요  |
| 이전 state를 기반으로 새 state를 계산할 때는 어떻게 하나요?                 | ⭐️ 필수 |
| 초기 state를 설정할 때 props를 사용하면 어떤 일이 일어나나요?               | 🔍 참고  |
| Prop Drilling이란?                                                          | ✅ 중요  |
| defaultProps란 무엇인가요?                                                  | ✅ 중요  |
| `ref`는 어떤 용도로 사용되나요?                                             | ✅ 중요  |
| `ref`는 어떻게 생성하나요?                                                  | ✅ 중요  |
| inline ref 함수는 왜 비추천되나요?                                          | ✅ 중요  |
| 컴포넌트 라이브러리에서 `forwardRef`를 사용할 때 추가 주의가 필요한 이유는? | ✅ 중요  |
| 캡처링 단계 이벤트란?                                                       | 🔍 참고  |
| React에서 클릭 이벤트를 코드로 발생시키려면?                                | 🔍 참고  |
| 이벤트 핸들러에는 왜 error boundary가 필요 없나요?                          | 🔍 참고  |
| 함수가 여러 번 호출되는 걸 어떻게 막나요?                                   | ✅ 중요  |
| try/catch와 error boundary는 어떻게 다른가요?                               | ✅ 중요  |
| `forwardRef`란 무엇인가요?                                                  | ✅ 중요  |
| `forwardRef`를 React DevTools에서 어떻게 디버깅하나요?                      | 🔍 참고  |
| forwardref 안쓰고 그냥 ref 전달하면 왜 안되나요?                            | ✅ 중요  |
| string ref는 왜 레거시로 간주되나요?                                        | 🔍 참고  |
| HTML과 React의 이벤트 처리 방식 차이는?                                     | ✅ 중요  |
| JSX에서 이벤트 핸들러를 바인딩하려면 어떻게 하나요?                         | ✅ 중요  |
| React의 Synthetic Event란?                                                  | ✅ 중요  |
| JSX에 함수를 괄호 열고 호출하는 형태로 작성했을 때 일어나는 일은?           | ✅ 중요  |
| key prop은 무엇이고, 배열 렌더링 시 사용하는 이유는?                        | ⭐️ 필수 |
| key로 index를 안전하게 사용할 수 있는 조건은?                               | ✅ 중요  |
| Virtual DOM이란 무엇이고 어떻게 동작하나요?                                 | ⭐️ 필수 |
| Shadow DOM과 Virtual DOM의 차이는?                                          | 🔍 참고  |
| React Fiber와 주요 목적은?                                                  | ✅ 중요  |
| Controlled Component, Uncontrolled Component                                | ✅ 중요  |
| Lifting State Up이란?                                                       | ✅ 중요  |
| props proxy란?                                                              | 🔍 참고  |
| React에서 데코레이터를 어떻게 사용하나요?                                   | 🔍 참고  |
| render hijacking이란?                                                       | 🔍 참고  |
| `displayName` 속성의 목적은?                                                | 🔍 참고  |
| 고차 컴포넌트(Higher-Order Component)란?                                    | ✅ 중요  |
| 고차 컴포넌트(HOC)에서 props proxy는 어떻게 구성하나요?                     | 🔍 참고  |
| HOC(고차 컴포넌트)의 한계는 무엇인가요?                                     | ✅ 중요  |
| Reconciliation이란?                                                         | ✅ 중요  |
| diffing 알고리즘이란?                                                       | ✅ 중요  |
| React의 diffing 알고리즘이 따르는 규칙은?                                   | ✅ 중요  |
| React는 왜 class 대신 className을 사용하나요?                               | ✅ 중요  |
| Fragments란?                                                                | ✅ 중요  |
| Stateless components, Stateful components                                   | ✅ 중요  |
| React의 장점, 단점                                                          | ✅ 중요  |
| Real DOM vs Virtual DOM 차이?                                               | ✅ 중요  |
| react-dom 패키지의 용도는?                                                  | ✅ 중요  |
| ReactDOMServer란?                                                           | 🔍 참고  |
| React에서 dangerouslySetInnerHTML을 사용하는 방법은?                        | 🔍 참고  |
| React에서 스타일을 적용하는 방법은?                                         | ✅ 중요  |
| React에서 이벤트 처리 방식은 HTML과 어떻게 다른가요?                        | ✅ 중요  |
| 배열 렌더링 시 key로 index를 사용하는 것의 영향은?                          | ✅ 중요  |
| windowing 기법이란?                                                         | 🔍 참고  |
| props를 DOM 요소에 spread할 때 주의해야 하는 이유는?                        | ✅ 중요  |
| React에서 컴포넌트를 메모이제이션(memoization)하려면 어떻게 하나요?         | ✅ 중요  |
| 서버 사이드 렌더링(SSR)을 어떻게 구현하나요?                                | ✅ 중요  |
| React의 production 모드는 어떻게 활성화하나요?                              | 🔍 참고  |
| Hooks는 render props나 고차 컴포넌트를 대체하나요?                          | ✅ 중요  |
| 컴포넌트 이름이 대문자로 시작해야 하는 이유는 무엇인가요?                   | 🔍 참고  |
| React v16에서 커스텀 DOM 속성을 지원하나요?                                 | 🔍 참고  |
| React와 ReactDOM의 차이는 무엇인가요?                                       | ✅ 중요  |
| ReactDOM이 React에서 분리된 이유는 무엇인가요?                              | ✅ 중요  |
| `react-dom`의 `render()` 메서드 목적은?                                     | 🔍 참고  |
| 브라우저 크기 조정 시 뷰를 다시 렌더링하려면 어떻게 하나요?                 | 🔍 참고  |
| React에서 props는 왜 직접 수정할 수 없나요?                                 | ⭐️ 필수 |
| react-router에서 Google Analytics를 추가하려면 어떻게 하나요?               | 🔍 참고  |
| 기본 React에서도 async/await를 사용할 수 있나요?                            | ✅ 중요  |
| 스타일 모듈(styles module)의 장점은 무엇인가요?                             | ✅ 중요  |
| React에서 인기 있는 린터(Linter) 도구에는 어떤 것들이 있나요?               | 🔍 참고  |
| `React.lazy()`란?                                                           | ✅ 중요  |
| Suspense 컴포넌트란?                                                        | ✅ 중요  |
| React v16에서의 에러 바운더리란?                                            | ✅ 중요  |
| Error Boundary는 어디에 배치하는 것이 적절한가요?                           | ✅ 중요  |
| React 16에서 잡히지 않은 오류의 동작은?                                     | 🔍 참고  |
| React v15에서는 에러 바운더리를 어떻게 처리했나요?                          | 🔍 참고  |
| 어떤 경우에 Error Boundary가 오류를 잡지 못하나요?                          | ✅ 중요  |
| React Strict Mode란?                                                        | ✅ 중요  |
| CRA(Create React App)는 무엇이며, 장점은?                                   | ✅ 중요  |
| CRA 프로젝트에서 폴리필(polyfill)을 추가하는 방법은?                        | 🔍 참고  |
| CRA에서 http 대신 https를 사용하려면?                                       | 🔍 참고  |
| CRA에서 상대 경로(`../../components/...`) import를 피하려면?                | ✅ 중요  |
| `renderToNodeStream()`의 목적은?                                            | 🔍 참고  |
| Next.js란? 주요 기능은?                                                     | ✅ 중요  |
| 좋아하는 react stack?                                                       | 🔍 참고  |

### React Router

| 질문                                                                                      |  중요도  |
| :---------------------------------------------------------------------------------------- | :------: |
| React Router란 무엇인가요?                                                                | ⭐️ 필수 |
| React Router는 `history` 라이브러리와 어떻게 다른가요?                                    | ✅ 중요  |
| history의 `push`와 `replace` 메서드의 목적은 무엇인가요?                                  | ✅ 중요  |
| useNavigate와 history 객체의 차이는 무엇인가요?                                           | ✅ 중요  |
| history → useNavigate issue?                                                              | 🔍 참고  |
| React Router v6의 `<Router>` 컴포넌트 종류는 무엇인가요?                                  | ✅ 중요  |
| React Router v6에서 중첩 라우트를 어떻게 구성하나요?                                      | ⭐️ 필수 |
| Outlet이란 무엇인가요?                                                                    | ✅ 중요  |
| 프로젝트에서 주로 어떤 방식으로 라우트를 구성했나요?                                      | ✅ 중요  |
| "Router는 하나의 자식 요소만 가질 수 있습니다" 경고가 뜨는 이유는?                        | 🔍 참고  |
| 기본 페이지 또는 NotFound 페이지를 구현하려면 어떻게 하나요?                              | ⭐️ 필수 |
| 로그인 후 자동 리디렉션을 구현하려면 어떻게 하나요?                                       | ⭐️ 필수 |
| URL 파라미터(`params`)와 쿼리 파라미터(`search`)의 차이는 무엇이며, 각각 어떻게 다루나요? | ⭐️ 필수 |
| 동적 경로(`:id` 등)를 사용할 때 발생할 수 있는 실수와 주의점은?                           | ✅ 중요  |
| 라우팅 상태(state)와 URL 상태를 분리해서 관리하는 이유는 무엇인가요?                      | ✅ 중요  |
| 라우트 보호(Protected Route)를 어떻게 구현하나요?                                         | ⭐️ 필수 |
| 라우팅 시 발생할 수 있는 성능 이슈와 최적화 방법은?                                       | ✅ 중요  |
| React Router에서 Link vs NavLink 차이는 무엇인가요?                                       | ✅ 중요  |
| SPA에서 서버 배포 시 발생할 수 있는 404 이슈는 어떻게 해결하나요?                         | ⭐️ 필수 |
| React Router v6와 v7의 주요 차이점은 무엇인가요?                                          | ✅ 중요  |
| React Router v7로 업그레이드할 때 고려해야 할 사항은 무엇인가요?                          | ✅ 중요  |

### Hook

| 질문                                                              |  중요도  |
| :---------------------------------------------------------------- | :------: |
| 훅(Hooks)이란?                                                    | ⭐️ 필수 |
| 훅을 사용할 때 지켜야 할 규칙은?                                  | ⭐️ 필수 |
| 훅(Hooks)이 클래스 컴포넌트의 모든 기능을 대체할 수 있나요?       | ✅ 중요  |
| 컴포넌트가 렌더링되지 않도록 하려면?                              | ✅ 중요  |
| `useReducer` 훅이란 무엇이며, 어떻게 사용하는지 설명해주세요.     | ⭐️ 필수 |
| `useState`와 `useReducer`는 어떻게 비교할 수 있나요?              | ✅ 중요  |
| state 변경을 감지하려면 어떻게 하나요?                            | ✅ 중요  |
| Context란 무엇인가요?                                             | ✅ 중요  |
| Consumer란?                                                       | 🔍 참고  |
| `useContext` 훅을 사용할 때 context는 어떻게 동작하나요?          | ⭐️ 필수 |
| `useContext` 훅은 보통 어떤 상황에서 사용하나요?                  | ✅ 중요  |
| Context 사용 시 발생할 수 있는 성능 문제는 어떻게 해결하나요?     | ✅ 중요  |
| useMemo와 useCallback의 차이점은? 언제 사용하는가?                | ⭐️ 필수 |
| 커스텀 훅(Custom Hook)은 언제 만들고 어떻게 구성하나요?           | ✅ 중요  |
| useRef는 DOM 접근 외에 어떤 용도로 사용할 수 있나요?              | ✅ 중요  |
| useEffect cleanup 함수는 언제 호출되나요?                         | ⭐️ 필수 |
| 비동기 작업 중 컴포넌트가 언마운트되었을 때 어떻게 처리하나요?    | ✅ 중요  |
| useLayoutEffect와 useEffect의 차이는?                             | ✅ 중요  |
| 동일한 상태를 여러 컴포넌트에서 공유할 때 어떤 방법을 사용하는가? | ✅ 중요  |
| 컴포넌트를 1초마다 업데이트하려면 어떻게 하나요?                  | 🔍 참고  |
| AJAX 호출은 어떻게 하고, 어느 시점에서 해야 하나요?               | ✅ 중요  |

### 성능

| 질문                                                      | 중요도  |
| :-------------------------------------------------------- | :-----: |
| Concurrent Rendering이란?                                 | ✅ 중요 |
| Async Mode vs Concurrent Mode 차이점은?                   | ✅ 중요 |
| React Server Component란?                                 | ✅ 중요 |
| React에서 hydration이란?                                  | ✅ 중요 |
| 코드 스플리팅이란?                                        | ✅ 중요 |
| React는 상태 업데이트를 어떻게 batching(묶음 처리)하나요? | ✅ 중요 |
| 자동 batching을 막을 수 있나요?                           | 🔍 참고 |
| 컴포넌트 내부에 또 다른 함수형 컴포넌트를 정의하면?       | ✅ 중요 |
| windowing 기법이란?                                       | 🔍 참고 |
