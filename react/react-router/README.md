# React Router

## React Router란 무엇인가요?

React Router는 React 기반 애플리케이션에서 클라이언트 사이드 라우팅을 가능하게 해주는 대표적인 라이브러리. SPA(Single Page Application) 구조에서 필수적인 기능들을 제공함

ex) 각 URL 경로에 따라 특정 컴포넌트를 렌더링할 수 있게 해 줌, 중첩 라우트, 동적 라우팅, 리디렉션, URL 파라미터 처리, 쿼리 스트링 관리, 라우트 보호 등 다양한 라우팅 전략을 지원

전통적인 멀티 페이지 앱(MPA)에서는 URL 변경 시 전체 페이지가 새로고침되며 서버로부터 새로운 HTML을 받아오지만, React Router를 사용하면 페이지 전체를 다시 로드하지 않고도 URL에 따라 뷰를 동적으로 바꿀 수 있어, 훨씬 빠르고 자연스러운 사용자 경험을 제공함.

특히 최신 버전인 React Router v6에서는 선언형 라우트 방식이 더욱 간결해졌고, useNavigate, useParams, useLocation 같은 훅 중심 API 덕분에 함수형 컴포넌트에서의 사용성이 크게 향상됐음. 또한 코드 스플리팅을 위한 lazy()와의 연계나, Outlet을 이용한 중첩 라우팅 구성도 매우 유연하게 구성할 수 있음.

## React Router는 `history` 라이브러리와 어떻게 다른가요?

`React Router`는 라우팅 기능을 제공하는 완전한 라이브러리.
`history`는 URL 변경을 다루는 저수준 라이브러리.
React Router 내부에서 history를 사용하지만, 자체적으로 라우트 매칭, 컴포넌트 렌더링 등을 처리.

## history의 `push`와 `replace` 메서드의 목적은 무엇인가요?

- `push`는 새로운 항목을 히스토리에 추가
- `replace`는 현재 항목을 대체.
  - 예: 로그인 후 이전 페이지로 돌아가지 않도록 하려면 `replace` 사용.

## useNavigate와 history 객체의 차이는 무엇인가요?

둘 다 React 앱에서 프로그래밍 방식으로 라우팅을 할 때 사용하는 도구. history 객체의 기능을 함수형 방식으로 간결하게 대체한 게 `useNavigate`API이며, React Router v6부터는 `history` 대신 `useNavigate()` 사용이 표준

- history 객체
  - React Router v5까지 사용되던 방식
  - `withRouter`, `useHistory()` 등을 통해 history 객체를 받아오고, `history.push('/path')`, `history.replace('/path')` 같은 메서드로 페이지를 이동
  - `history` 객체는 react-router가 내부적으로 사용하는 저수준의 라우팅 관리 도구였고, 외부에서 직접 다루는 방식
- useNavigate
  - React Router v6에서 도입된 방식으로, `useHistory()`는 더 이상 사용되지 않고 `useNavigate()`로 대체됨
  - `navigate('/about')`, `navigate(-1)` 등의 방식으로 라우팅을 처리하며, 보다 직관적이고 명확한 API를 제공

## history → useNavigate issue?

React Router v6 초창기 (2022~2023년) 즈음에 페이지 이탈 방지 기능 구현할 때 `useNavigate()` 기반의 라우팅에서 문제가 있었음. 기존에 쓰던 `history.block()`은 더 이상 지원되지 않고, `useNavigate()`는 아직 안정화되지 않아서 내부적으로 unstable API를 써야 했던 경험이 있음

- 이전 버전 (v5):
  - `history.block()` API로 페이지 이동을 막거나 confirm alert을 띄우는 기능을 안정적으로 구현할 수 있었음.
  - 예:
    ```jsx
    const unblock = history.block((tx) => {
      if (window.confirm("정말 나가시겠습니까?")) {
        unblock();
        tx.retry(); // 이동 재시도
      }
    });
    ```
- v6 초기 (특히 6.3~6.4까지):
  - `useNavigate()` 기반에서는 이런 식의 navigation blocking 기능이 제공되지 않았거나, 실험적인 future flag로만 구현 가능했었음
  - 그래서 history 기반 라우팅에서는 가능했던 로직이, `useNavigate`에서는 잘 동작하지 않아서 고생 엄청함 ㅠㅠ
  - 이 시기에는 RouterProvider + createBrowserRouter 조합에서도 blocking 관련 API는 `unstable_` 접두어가 붙은 실험적 상태였음. 중요하지 않은 페이지였고, 보안상 문제 없었고 테스트에서 문제를 발견하지 않았기떄문에 이 api 사용했음.
- v6.4 이후로 점점 개선됨:
  - 현재는 `unstable_useBlocker` → `useBlocker` 또는 `navigation.block()` 같은 방식으로 대체 가능하지만, 여전히 완벽히 v5 수준의 유연함은 아니라고 평가됨

## React Router v6의 `<Router>` 컴포넌트 종류는 무엇인가요?

- `BrowserRouter`: 브라우저 환경용
- `HashRouter`: 해시 기반 라우팅
- `MemoryRouter`: 메모리 기반 라우팅
- `StaticRouter` SSR용

## React Router v6에서 중첩 라우트를 어떻게 구성하나요?

중첩 라우트를 구성하기 위해 <Route>의 children으로 다른 <Route>를 배치하고, 부모 컴포넌트 안에서 <Outlet /> 컴포넌트를 사용하여 자식 컴포넌트를 렌더링함.

- 이 방식은 다단계 페이지 구조(예: /dashboard/settings, /dashboard/profile)를 깔끔하게 표현할 수 있게 해주며, 부모-자식 관계의 뷰 계층 구조를 자연스럽게 구성할 수 있음
- 또 중첩 라우트를 쓰면 각 뷰의 loader, errorElement, lazy() 같은 기능을 라우트 단위로 분리 적용할 수 있어서, React Router v6.4 이상에서는 데이터 로딩 최적화까지 할 수 있음
  개인적으로 참여한 프로젝트에서는 관리자 페이지의 공통 레이아웃을 하나로 구성하고, 각 서브 메뉴를 중첩 라우팅으로 처리했음. (레이아웃 재사용성, 코드분리 → 유지 보수성)

## Outlet이란 무엇인가요?

Outlet은 React Router v6에서 중첩 라우트를 구성할 때 사용되는 컴포넌트. 부모 라우트가 자식 라우트를 렌더링할 위치를 지정하기 위해 사용하며, 일종의 라우팅용 슬롯(Slot) 역할을 함.

- 예를 들어 /dashboard 경로에 대한 공통 레이아웃이 있고, 그 하위 경로로 /dashboard/profile, /dashboard/settings 같은 페이지가 있다면, 부모 컴포넌트인 `Dashboard` 안에 `<Outlet />`을 넣어두면 해당 위치에 자식 라우트 컴포넌트가 렌더링됨
- 보통 관리자 페이지나 마이페이지처럼 레이아웃은 공통이고, 콘텐츠만 바뀌는 구조를 자주 사용. 이때 `<Outlet />`을 사용하면 레이아웃을 하나로 재사용하면서, 라우트 별 콘텐츠만 유동적으로 렌더링할 수 있어 유지보수성과 구조적인 효율성이 높아짐

## 프로젝트에서 주로 어떤 방식으로 라우트를 구성했나요?

개인적으로 주로 `createBrowserRouter` 로 라우트 구성하고 이를 `RouterProvider` 에 제공 하는 방식 사용. 라우트 중심으로 loader/action/error 등을 선언적으로 구성하면 컴포넌트를 단순하게 분리할 수 있어서 협업 시에도 구조가 명확해지고 유지보수가 쉬웠음.

- (데이터 중심 라우팅(data-driven routing) 방식을 구현할 수 있도록 설계된 API) 이 조합의 가장 큰 장점은 라우트 정의와 함께 데이터 로딩, 오류 처리, 권한 체크 등 UI 외의 로직을 함께 선언적으로 구성할 수 있음.

1. 라우트 단위로 데이터 로딩을 분리할 수 있음
   - `loader`, `action`, `errorElement` 같은 옵션을 통해 각 라우트마다 서버 요청이나 상태 변경 로직을 분리할 수 있음.
2. 에러 및 로딩 처리의 표준화
   - 각 라우트마다 `errorElement`, `pendingElement` 등을 명시해놓으면 라우트 단위에서의 에러 핸들링이 매우 명확해짐
3. 라우트 계층 구조가 명확
   - createBrowserRouter는 객체 기반으로 라우트를 정의하므로, 중첩 관계가 눈에 잘 보이고 유지보수성이 좋음.
4. 라우트 중심 개발 방식
   - URL 중심으로 앱의 구조를 먼저 설계하고, 각 라우트에 필요한 데이터/행동을 선언하는 구조는 프레임워크 설계 철학과 맞닿아 있음.
5. SSR 및 코드 스플리팅과도 궁합이 좋음
   - `lazy()`와 함께 쓰면 라우트 단위 코드 스플리팅이 매우 쉽게 적용됨.
   - loader 내부에서 데이터를 미리 패치하면, SSR 환경에서도 데이터를 함께 전달할 수 있는 구조가 만들어짐.

## "Router는 하나의 자식 요소만 가질 수 있습니다" 경고가 뜨는 이유는?

`<Router>` 컴포넌트는 반드시 하나의 자식 요소만 렌더링해야 하므로, 여러 요소를 렌더링할 경우 `<Routes>` 또는 `<div>`로 감싸야 함.

## 기본 페이지 또는 NotFound 페이지를 구현하려면 어떻게 하나요?

`<Route path="*">`를 사용해 정의되지 않은 모든 경로를 처리할 수 있음. 아님 `createBrowserRouter` + `RouterProvider` 조합 사용했으면 errorElement 직접 명시 할 수 있음.

## 로그인 후 자동 리디렉션을 구현하려면 어떻게 하나요?

로그인 성공 시 `navigate('/home')` 또는 `history.push('/home')` 호출. 토큰 검증 상태를 `useEffect`로 감지하여 리디렉션하는 패턴도 일반적.

## URL 파라미터(`params`)와 쿼리 파라미터(`search`)의 차이는 무엇이며, 각각 어떻게 다루나요?

둘 다 라우팅 시 값을 전달하는 방법이지만

- URL 파라미터 (params)
  - 경로 자체에 포함되는 값(필수 값)
  - 보통 리소스 식별자처럼 의미 있는 데이터를 전달할 때 사용됨 (예: `/user/123` → `123`은 특정 유저의 ID)
  - React Router에서는 `<Route path="/user/:id" />`처럼 선언하고, `useParams()` 훅으로 값을 가져옴
- 쿼리 파라미터 (search)
  - URL 경로 뒤에 `?key=value` 형식으로 붙는 값(선택적 필터나 옵션 값)
  - 필터, 정렬, 검색어 등 옵션성 데이터를 전달할 때 주로 사용 (예: `/products?category=shoes&page=2`)
  - React Router에서는 `useLocation()` 훅을 사용해서 `search` 값을 읽고, `URLSearchParams`로 파싱

## 동적 경로(`:id` 등)를 사용할 때 발생할 수 있는 실수와 주의점은?

- useParams()로 받은 값이 문자열이라는 점을 간과하고 숫자로 비교하거나 연산하는 경우
- 또한, 존재하지 않는 id로 접근했을 때의 예외 처리를 하지 않으면 404 화면이 뜨지 않거나, 빈 화면이 렌더링되는 경우
- 이 외에도 경로에 중복된 패턴이 있을 경우, 라우팅 충돌이나 예상치 않은 매칭 순서가 발생할 수 있어 주의 필요.

## 라우팅 상태(state)와 URL 상태를 분리해서 관리하는 이유는 무엇인가요?

URL 상태는 공유와 복원에 유리한 상태, 라우팅 state는 일시적이고 내부 흐름에서만 필요한 상태로, 목적과 생명주기가 다르기 때문에 분리해서 관리하는 것이 설계적으로 바람직함

- URL 상태
  - 브라우저 주소창에 노출되는 상태
  - 페이지를 새로고침하거나 URL을 공유해도 일관된 결과를 보여줘야 하는 상태에 적합
  - 예: 검색어, 필터 조건, 페이지 번호 등
    → /products?category=shoes&page=2
- 라우팅 상태
  - React Router의 navigate('/path', { state: { ... } })로 전달되는 상태
  - URL에는 노출되지 않으며, 페이지 전환 간 임시 데이터 전달에 주로 사용됨
  - 예: 로그인 성공 후 이동할 경로, 이전 페이지의 origin 정보 등
- 분리 이유
  - 공유 가능 여부
    - URL 상태는 링크 공유가 가능하지만, 라우팅 state는 그렇지 않음 → 검색 조건, 결과 페이지 등은 URL에 보존 필요
  - 데이터 보존
    - 페이지 새로고침 시 state는 사라지므로, 중요한 데이터는 URL 또는 전역 상태에 저장하는 게 안전함
  - 보안 및 UX 고려
    - 민감한 정보(예: 토큰)는 URL에 포함시키지 않아야 하고, 이런 데이터는 state나 context로 관리해야 함
  - 컴포넌트 재사용성
    - 라우팅 state에 의존하면 컴포넌트가 특정 라우팅 흐름에 종속되므로, 테스트나 재사용이 어려워질 수 있음

## 라우트 보호(Protected Route)를 어떻게 구현하나요?

라우트 보호는 로그인 상태나 권한에 따라 특정 라우트에 대한 접근을 제한하는 기능. 보통 인증 여부를 확인한 뒤, 조건에 따라 리디렉션하거나 해당 페이지를 보여주는 방식으로 구현
보통 RequireAuth 같은 보호용 래퍼 컴포넌트를 만들고, 그 안에서 토큰이나 로그인 상태를 검사. 로그인 여부 외에도 권한(role)에 따른 분기, SSO 연동, 토큰 만료 처리, 이전 경로 기억 후 복귀 같은 로직도 함께 고려.

## 라우팅 시 발생할 수 있는 성능 이슈와 최적화 방법은?

라우팅 시에는 페이지 단위의 JS 번들 크기 증가, 필요 없는 컴포넌트 렌더링, 초기 렌더 지연 같은 이슈가 발생할 수 있음

- 코드 스플리팅(Code Splitting)
  - React의 lazy()와 Suspense를 활용해 라우트 단위로 컴포넌트를 지연 로딩할 수 있음
  - 라우트 전환 시 무거운 상태를 초기화하거나, 리렌더링 최적화를 위해 memo나 useMemo를 함께 사용

## React Router에서 Link vs NavLink 차이는 무엇인가요?

Link와 NavLink는 모두 React Router에서 라우팅을 위한 컴포넌트이지만, NavLink는 현재 경로와 일치 여부를 판단해서 자동으로 활성화 상태를 부여할 수 있음
`<NavLink to="/home" className={({ isActive }) => isActive ? 'active' : ''} />`
예를 들어 네비게이션 메뉴처럼 현재 위치를 시각적으로 강조할 때 NavLink가 유용.
Link는 단순히 페이지 이동만 처리하고, 경로 비교나 스타일 적용은 직접 처리해야 함

## SPA에서 서버 배포 시 발생할 수 있는 404 이슈는 어떻게 해결하나요?

→ ex) Nginx에서 `try_files` 설정 or Netlify 설정 등.
SPA에서는 라우팅을 클라이언트에서 처리하기 때문에, 사용자가 잘못된 URL로 직접 접근하면 서버는 해당 파일을 찾지 못해 404를 반환할 수 있음. 이 문제를 해결하려면, 서버에서 모든 요청을 index.html로 리디렉션하도록 설정해야 함.
이는 웹 서버(Nginx, Apache)나 호스팅 환경(Netlify, Vercel 등)에 따라 설정 방식이 다름

- 예: Nginx
  ```bash
  location / {
  try_files $uri /index.html;
  }
  ```
- Netlify \_redirects 파일 `/*    /index.html   200`

이렇게 설정하면 서버는 라우트를 찾지 못해도 항상 index.html을 반환하고, 그 후 React 앱이 클라이언트에서 URL을 해석해 적절한 페이지를 렌더링함

## React Router v6와 v7의 주요 차이점은 무엇인가요?

v7:

1. 프레임워크 모드 도입:

   Next.js나 Remix와 유사한 풀스택 애플리케이션을 구축할 수 있음. 프레임워크 모드는 서버 사이드 렌더링, 번들 최적화, 향상된 타입 안전성 등의 기능을 제공. [Remix - Build Better Websites](https://remix.run/blog/react-router-v7?utm_source=chatgpt.com)

2. 라우트 정의 방식의 변화:

   v6.4에서는 객체 기반의 라우트 정의 방식이 도입되었지만, v7에서는 다시 컴포넌트 기반의 라우트 정의 방식이 권장됨. 이는 개발자들에게 더 익숙한 패턴을 제공하며, 기존 코드와의 호환성을 높임. [Medium](https://medium.com/front-end-world/react-router-v7-8719488842a6?utm_source=chatgpt.com)

3. 업그레이드의 용이성:

   v6에서 v7로의 업그레이드는 대부분의 경우 비파괴적(non-breaking)이라고 함. 특히, 미래 플래그(future flags)를 활성화한 경우, 단계적으로 업그레이드를 진행할 수 있어 기존 코드베이스에 큰 변경 없이 새로운 기능을 도입할 수 있음. [React Router](https://reactrouter.com/upgrading/v6?utm_source=chatgpt.com)

4. 타입 안전성 강화:

   v7에서는 라우트 매개변수, 로더 데이터, 액션 등에 대한 타입 안전성이 향상되었다고 함. 이를 통해 개발자는 컴파일 타임에 오류를 보다 쉽게 감지하고, 안정적인 코드를 작성할 수 있음.

## React Router v7로 업그레이드할 때 고려해야 할 사항은 무엇인가요?

1. 미래 플래그 활성화:

   업그레이드 전에 v6의 최신 버전으로 업데이트하고, 미래 플래그를 활성화하여 단계적으로 변경 사항을 적용하는 것이 권장함. 이를 통해 코드베이스에 미치는 영향을 최소화할 수 있습니다. [React Router](https://reactrouter.com/upgrading/v6?utm_source=chatgpt.com)

2. 라우트 정의 방식 검토:

   v7에서는 컴포넌트 기반의 라우트 정의 방식이 다시 권장되므로, 기존에 객체 기반으로 라우트를 정의했다면 이를 재검토하고 필요 시 수정 필요. [Medium](https://medium.com/front-end-world/react-router-v7-8719488842a6?utm_source=chatgpt.com)

3. 타입스크립트 지원 확인:

   v7에서는 타입 안전성이 강화되었으므로, 타입스크립트를 사용하는 프로젝트라면 해당 기능을 활용하여 코드의 안정성을 높일 수 있음. [React Router](https://reactrouter.com/?utm_source=chatgpt.com)

4. 의존성 버전 확인:

   v7은 `react@18` 및 `react-dom@18` 이상의 버전을 필요로 하므로, 프로젝트의 React 버전을 확인하고 필요 시 업데이트해야 함. [React Router](https://reactrouter.com/upgrading/v6?utm_source=chatgpt.com)
