# 최적화

## 웹 최적화 기법이 뭐고, 어떠한 것들이 있나요?

웹 최적화는 궁극적으로 페이지 로드 속도와 사용자 경험을 개선하기 위한 작업임. 초기 로딩 속도를 줄이고, 불필요한 리소스 요청을 최소화하며, 효율적인 렌더링과 전송 전략을 통해 성능을 향상시키는 것이 핵심.

- 코드 스플리팅: 필요한 코드만 로딩 → 초기 페이지 가볍게
- Lazy Loading: 이미지/컴포넌트 지연 로딩 → 렌더링 부담 분산
- Tree Shaking: 사용하지 않는 코드 제거 → 번들 사이즈 ↓
- 이미지 최적화(WebP 등): 이미지 용량 ↓ → 전송 속도 ↑
- Gzip/Brotli 압축: 텍스트 리소스 전송 크기 ↓
- CDN 활용: 리소스를 사용자와 가까운 서버에서 제공 → latency ↓
- Preload/Prefetch: 리소스를 미리 가져와 사용 체감 속도 ↑
- 캐싱 전략: 재요청 방지 → 페이지 재방문 속도 향상

## 당신은 어떤 웹사이트의 assets/resources를 어떻게 최적화 할것인가요?

1. 이미지 최적화

- WebP, AVIF 등 최신 포맷으로 변환하고
- 필요 시 `srcset`이나 `responsive image`를 활용해 해상도에 따라 이미지 크기 조절

2. 정적 리소스 압축

- HTML, CSS, JS 파일은 Gzip 또는 Brotli 압축
- JS 코드에 대해서는 Tree Shaking 및 Minify 처리

3. **코드 스플리팅 및 Lazy Loading**

- 초기 렌더링에 필요하지 않은 JS/컴포넌트는 지연 로딩
- React/Vue 등의 라우트 기반 코드 스플리팅 적용

4. **CDN 활용**

- 이미지, JS, CSS 등 정적 리소스를 CDN으로 서빙하여 전송 거리 최소화 및 응답 속도 향상

5. **HTTP 캐싱 전략 적용**

- 리소스에 `Cache-Control`, `ETag` 등의 헤더를 설정해 중복 요청 방지
- 자주 바뀌지 않는 리소스는 long-term 캐싱

6. **Preload/Prefetch 전략**

- 사용자가 곧바로 필요로 할 리소스는 `<link rel="preload">`
- 추후 탐색 예상 경로는 `<link rel="prefetch">`

: 이미지는 WebP 최적화, 정적 리소스는 압축 및 캐싱, 필요한 리소스만 지연 로딩하고 CDN으로 빠르게 서빙하며, 사용자 행동을 예측한 preload/prefetch까지 종합적으로 적용.

## 브라우저가 주어진 도메인에 대해 자원들을 한번에 얼마나 다운로드 하나요? 그리고 예외는?

브라우저는 한 도메인에 대해 기본적으로 6개의 자원을 동시에 다운로드할 수 있도록 제한함. 이는 네트워크 효율성과 공정성 때문이며, HTTP/2를 사용할 경우 다중 스트림으로 동시 처리되어 이 제한이 사실상 사라짐. 실무에서는 서브도메인을 활용하거나 CDN, HTTP/2를 통해 이를 우회.

- Chrome, Edge, Firefox: 6개
- Safari: 6~8개
- IE 10 이상: 6개
- (과거 IE 6~7): 2개 (HTTP 1.1 기준)

우회방법:

- 도메인을 다르게 하면 병렬 다운로드 가능
  - 대표적 전략: CDN을 여러 서브도메인으로 나누기 (e.g., `img1.domain.com`, `img2.domain.com`)
- HTTP/2 사용 시
  - 동시 연결 수 제한이 사실상 무의미해짐
  - 하나의 TCP 연결 내에서 다중 스트림 처리 가능
    → 여러 자원을 병렬 처리 가능
- 브라우저 설정/확장으로 변경 가능하지만, 실무에서는 기본값을 가정하고 개발

## 웹 성능과 관련된 이슈

1. 네트워크 요청에 빠르게 응답

- `3.xx` 리다이렉트를 피할 것
- `meta-refresh` 사용금지
- `CDN(content delivery network)`을 사용할 것
- 동시 커넥션 수를 최소화 할 것
- 커넥션을 재활용할 것

2. 자원을 최소한의 크기로 내려받기

- 777K
- `gzip` 압축을 사용할 것
- `HTML5 App cache`를 활용할 것
- 자원을 캐시 가능하게 할 것
- 조건 요청을 보낼 것

3. 효율적인 마크업 구조를 구축

- 레거시 IE 모드는 http 헤더를 사용할 것
- @import 의 사용을 피할 것
- inline 스타일과 embedded 스타일은 피할 것
- 사용하는 스타일만 CSS 에 포함할 것
- 중복되는 코드를 최소화 할 것
- 단일 프레임워크를 사용할 것
- Third Party 스크립트를 삽입하지 말 것

4. 미디어 사용을 개선

- CSS3 를 활용할 것
- 하나의 작은 크기의 이미지는 DataURL 을 사용할 것
- 비디오의 미리보기 이미지를 만들 것

5. 빠른 자바스크립트 코드를 작성

- 코드를 최소화할 것
- 필요할 때만 스크립트를 가져올 것 : flag 사용
- DOM 에 대한 접근을 최소화 할 것 : Dom manipulate 는 느리기 때문
- 다수의 엘리먼트를 찾을 때는 selector api 를 사용할 것.
- 마크업의 변경은 한번에 할 것 : temp 변수를 활용
- DOM 의 크기를 작게 유지할 것.
- 내장 JSON 메서드를 사용할 것.

6. 애플리케이션의 작동원리를 알고 사용

- Timer 사용에 유의할 것.
- `requestAnimationFrame` 을 사용할 것 권장
- 활성화될 때를 알고 있을 것

## TTI (Time to Interactive), FCP 등의 렌더링 지표

웹 렌더링 성능을 측정할 때 자주 사용하는 지표로는 FCP(First Contentful Paint), TTI(Time to Interactive), LCP(Largest Contentful Paint) 등이 있음

FCP는 사용자가 페이지에서 첫 번째 콘텐츠(텍스트, 이미지 등)를 볼 수 있게 되는 시점을 의미

TTI는 사용자가 페이지를 완전히 사용할 수 있는 시점으로, 주요 인터랙션이 지연 없이 가능한 순간을 의미

LCP는 가장 큰 콘텐츠 요소가 렌더링 완료되는 시점으로, 실제 사용자 체감 속도와 가장 밀접

## SPA 성능 병목은 어디서 발생할까요?

SPA(Single Page Application)의 경우, 최초 로딩 시 번들 크기가 크기 때문에 TTI가 지연되는 경향이 있음.

- JS 번들 크기 과다 → 불필요한 코드 포함, 라이브러리 의존도 과다한 경우 발생

- 초기 렌더링 시 blocking script → 리소스 로딩 차단

- Lazy loading 미적용 → 모든 컴포넌트를 한 번에 불러옴

- 복잡한 연산을 main thread에서 처리 → 인터랙션 응답 지연

- 비효율적인 렌더링 구조 → 불필요한 리렌더링

따라서, SPA에서는 코드 스플리팅, Lazy loading, Critical CSS 적용, 캐싱 전략 등을 통해 TTI와 FCP를 줄이는 것이 중요
