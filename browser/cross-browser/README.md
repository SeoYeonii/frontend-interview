# 크로스브라우징

## 크로스 브라우징이란?

웹 표준에 따라 개발을 하여 서로 다른 OS 또는 플랫폼에 대응하는 것을 말함. 즉, 브라우저의 렌더링 엔진이 다른 경우에 인터넷이 이상없이 구현되도록 하는 기술. 웹 사이트를 서로 비슷하게 만들어 어떤 환경에서도 이상없이 작동되게 하는 것이 목적. 즉, 어느 한쪽에 최적화되어 치우치지 않도록 공통요소를 사용하여 웹 페이지를 제작하는 방법을 말함.

## 웹 표준과 표준 제정 기관이 왜 중요한가요?

웹 표준은 다양한 브라우저와 기기에서 웹이 일관되게 동작 하도록 보장해줌. W3C, WHATWG 같은 표준 기구는 개발자, 브라우저 벤더들이 공통 규칙을 기반으로 개발할 수 있게 도와줌. 이를 통해 호환성 문제를 줄이고 유지보수성을 높일 수 있음.

## 크로스 브라우징 대응 전략은?

크로스 브라우징은 다양한 브라우저(Chrome, Safari, Firefox, Edge 등)에서 기능과 UI가 동일하게 동작하도록 보장하는 작업

- 표준 기술 사용
  - W3C 표준에 맞는 HTML/CSS/JS 문법을 사용하여 예측 가능한 동작 유도
  - autoprefixer, babel 등을 통해 브라우저별 차이 자동 처리
- 호환성 체크 도구 사용
  - caniuse.com으로 브라우저 지원 여부 확인
  - ESLint + eslint-plugin-compat 등으로 호환성 린팅
- Polyfill / Transpiler 적용
  - core-js, regenerator-runtime, babel 등으로 JS 최신 문법을 구버전에서도 사용 가능하게 변환
  - postcss, autoprefixer로 CSS 자동 벤더 프리픽스 처리
- 반응형 및 유연한 레이아웃
  - 고정 너비 대신 flex, grid, vw/vh, rem 단위를 활용해 다양한 환경 대응
  - @media 쿼리로 해상도/OS/브라우저 기반 분기 처리
- Graceful Degradation & Progressive Enhancement
  - 핵심 기능만 먼저 제공하고, 고급 기능은 점진적으로 추가
  - 구버전 브라우저에서도 치명적인 오류 없이 기본 사용 가능하게 설계
- 실제 테스트
  - 브라우저별 실제 QA 확인 (Chrome, Safari, Firefox, Edge, 모바일 WebView 등)
- 필요 시 BrowserStack, Sauce Labs 등 도구 활용

## `canIuse`, `autoprefixer` 등 도구 활용 여부?
