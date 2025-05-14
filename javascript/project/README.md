# 프로젝트

## input에 딜레이를 걸려면 어떻게 할까요?

이벤트 디바운스를 걸면 됨. (디바운스는 사용자가 입력을 멈춘 뒤 일정 시간 후에 함수가 실행되도록 함)

```jsx
function debounce(func, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => func.apply(this, args), delay);
  };
}
```

## 디바운스, 쓰로틀에 대해 설명해주세요. 코드를 직접 작성할 수 있는지?

- 디바운스: 입력이 멈춘 후 일정 시간 뒤에 함수 실행. 연속 호출 방지.
  ```jsx
  const debounce = (fn, delay) => {
    let timer;
    return (...args) => {
      clearTimeout(timer);
      timer = setTimeout(() => fn(...args), delay);
    };
  };
  ```
- 쓰로틀: 일정 시간 간격으로 함수 실행. 과도한 호출 제한.
  ```jsx
  const throttle = (fn, limit) => {
    let waiting = false;
    return (...args) => {
      if (!waiting) {
        fn(...args);
        waiting = true;
        setTimeout(() => (waiting = false), limit);
      }
    };
  };
  ```

## JavaScript 코드를 디버깅할 때 사용하는 도구나 기법은 무엇인가요?

- 브라우저 DevTools의 Console, Sources, Network, Performance 탭 활용
- `console.log`, `debugger` 사용
- Breakpoints, Call Stack, Scope 보기
- Linter (ESLint) 및 타입 검사기 (TypeScript) 사용
- React DevTools 사용

## 여러 파일 간 코드를 공유하는 방법에는 어떤 것들이 있나요?

- ESM(ES Modules)의 `import` / `export` 문법 사용
- CommonJS (require/module.exports) - Node.js 환경
- 번들러 없이 `<script type="module">` 사용 가능 (모듈 스코프 적용됨)
- 공유 모듈을 별도 파일로 작성한 후 여러 파일에서 `import`해서 사용

## 코드 스플리팅이 필요한 이유는?

- 초기 로딩 시 한 번에 많은 JS 파일을 다운로드하면 렌더링이 느려지기 때문
- 코드 스플리팅을 통해 필요한 순간에 필요한 코드만 로드하여 성능 향상
- 주로 라우트 단위, 컴포넌트 단위, 조건 분기에 따라 분리
- Webpack, Rollup, Vite 등의 번들러에서 지원

## 웹팩/번들러 없이 JS 프로젝트 구조를 어떻게 관리하나요?

- `type="module"`을 사용하면 브라우저가 모듈 스코프를 인식함
- 기능 단위로 JS 파일 분리 후 `import/export`로 관리
- 브라우저가 HTTP 요청으로 각각의 모듈을 요청하기 때문에 의존성이 많을수록 요청 수 증가 → 느려질 수 있음
- 따라서 정적 자산 관리, 의존성 순서 등을 명확히 해줘야 하며, 실제 프로젝트에서는 번들러 도입이 권장됨 (나도 웹팩/번들러 없이 프로젝트 구성해본적은 없음)

# Webpack과 Vite의 차이는?

Webpack은 전통적인 번들러로, 모든 자원을 모아서 번들링 후 실행.
Vite는 개발 시 ESM 기반의 모듈 핫 리로드(HMR)를 지원하며, 번들링 없이도 빠른 개발 서버를 실행할 수 있어 DX(개발 경험)가 뛰어남. 빌드 시에는 Rollup 기반으로 최적화된 번들을 생성. Vite는 브라우저에서 ESM을 직접 이용해서 파일을 불러옴. 즉, 개발 중엔 브라우저가 필요한 모듈만 바로바로 가져와서 실행하기 때문에, 전체 앱을 미리 묶는(번들링) 시간이 필요 없음.

- HMR: "수정한 파일만 즉시 반영하는 기능". 개발 중에 파일을 수정하면 전체 앱을 새로고침하지 않고, 바뀐 모듈(파일)만 바로 교체해서 페이지에 반영. 그래서 빠르고 상태 유지도 됨.
- 개발할 때는 ESM으로 모듈을 개별적으로 불러오지만, 배포할 땐 모든 파일을 하나로 묶는 "번들링" 작업이 필요함. 이 작업을 Rollup 사용해서 처리. (최적화의 특화)
  - 사용하지 않는 코드 제거 (Tree-shaking)
  - 코드 압축
  - 중복 모듈 제거

## 번들링과 트리 쉐이킹(Tree-shaking)이란?

- 번들링은 여러 JS/TS/리소스 파일을 하나의 파일로 묶는 과정
- 트리 쉐이킹은 사용되지 않는 코드를 제거하여 최종 번들 크기를 줄이는 최적화 기법
  예시:

```jsx
// utils.js
export const used = () => {};
export const unused = () => {};
// 만약 used()만 사용된다면, 트리 쉐이킹을 통해 unused()는 최종 번들에 포함되지 않음
```

## Dynamic Import란?

동적 import는 특정 시점에 필요한 모듈만 비동기로 로드하는 문법

```jsx
button.addEventListener("click", async () => {
  const module = await import("./Chart.js");
  module.render();
});
```

- 초기 로딩 속도 향상
- 코드 스플리팅에 활용 가능
- 라우트 기반 코드 분할에도 자주 사용

## SPA에서 초기 로딩을 최적화하려면?

SPA는 모든 자바스크립트를 한 번에 로딩하기 때문에 초기 로딩 속도가 느릴 수 있어서

- 코드 스플리팅 (라우트, 컴포넌트 단위)
- Lazy Loading (React.lazy, dynamic import)
- Critical CSS 추출 및 비동기 CSS 로딩
- 이미지 지연 로딩(Lazy Load)
- Preload, Prefetch, CDN 캐싱

## JS 프로젝트 디렉토리 구조를 어떻게 구성하나요?

프로젝트 규모와 팀에 따라 다르지만, 일반적으로 다음과 같은 방식으로 구성

```bash
src/
├── components/    # 재사용 가능한 UI 컴포넌트
├── pages/         # 라우트 단위 페이지
├── hooks/         # 커스텀 훅
├── utils/         # 유틸 함수
├── apis/          # API 호출 함수
├── store/         # 상태 관리
├── assets/        # 이미지, 폰트, 스타일 등 정적 리소스
├── constants/     # 상수 정의
├── types/         # 타입 정의 (TS 사용 시)

```
