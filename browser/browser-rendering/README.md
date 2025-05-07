# 브라우저 구조 및 렌더링 엔진

## 브라우저 정의 & 구성요소

브라우저는 사용자가 선택한 자원을 서버에 요청하고, 브라우저에 표시하는 일을 함. 자원은 html 문서, pdf, image등 다양한 형태이며 자원의 주소는 uri에 의해 정해짐

구성 요소

- 사용자 인터페이스 (UI): 주소창, 뒤로가기 버튼 등
- 브라우저 엔진: 렌더링 엔진과 JS 엔진 사이에서 조정자 역할 (각 구성 요소들이 올바른 타이밍에 실행되도록 조정)
- 렌더링 엔진: HTML, CSS 해석하고 이를 시각적으로 페이지에 출력
- 통신: HTTP 요청, 응답 처리
- UI 백엔드: 폰트 렌더링, 창 그리기 등 OS 추상화 역할
- JS 엔진: 자바스크립트 실행하는 역할
- 자료저장소: localStorage, IndexedDB등

## 웹 브라우져에서 사이트를 렌더링 하는 과정이 어떻게 되나요?

1. 주소 입력 → 리소스 요청(HTTP)
   사용자가 URL을 입력하면 브라우저는 DNS를 통해 해당 주소에 대한 IP를 얻음

   - **DNS 조회**: 도메인 이름을 IP 주소로 변환
     - 로컬 DNS 캐시 → DNS 서버 → 루트/상위 서버로 재귀 탐색하며 IP 획득
   - **TCP 연결**: 대상 서버와 3-way handshake로 연결을 설정
   - **HTTPS 보안 연결(TLS handshake)**: HTTPS라면 TLS 핸드셰이크도 수행
   - **HTTP 요청 전송**: 브라우저는 요청 헤더와 함께 HTML 파일을 요청

2. 서버 응답 → HTML 문서 수신

3. 렌더링 엔진 작동 (HTML → 화면)

   1. HTML 파싱 → DOM Tree 생성

   2. CSS 파싱 → CSSOM(CSS Object Model) 생성

   3. DOM + CSSOM → Render Tree 생성 (화면에 보이지 않는 요소(ex. `display: none`)는 제외)

   4. Render Tree 기반 Layout 계산

   5. 각 노드 위치/크기 배정 (Reflow)
      렌더링 엔진 + UI 백엔드

   6. Painting → 실제 픽셀로 그리기
      렌더링 엔진 + GPU (→ 컴포지터 스레드)

   7. 컴포지팅 (레이어 합성)

이러한 과정이 점진적으로 진행되며, 렌더링 엔진은 좀 더 빠르게 사용자에게 제공하기 위해 모든 html을 파싱할 때 까지 기다리지 않고 배치와 그리기 과정을 시작함. 즉 전송을 받고 기다리는 동시에 받은 내용을 먼저 화면에 보여줌. (웹페이지에 접속할 때 한꺼번에 뜨지 않고 점점 화면이 나오는 이유)

**파싱 중간에 `<script>` 태그를 만나면,**
→ 렌더링을 중단하고 JS 실행 (제어권한을 자바스크립트 엔젠에게 넘김)
→ 필요 시 DOM/CSSOM을 수정하여 렌더링 결과에 영향

## 렌더링 엔진은 멀티스레드로 동작하는가?

YES. 렌더링 엔진은 멀티스레드 환경에서 동작함.
브라우저는 단일 스레드로 동작하는 자바스크립트 엔진과는 별도로, 렌더링을 담당하는 프로세스 내에서 여러 스레드를 운영
ex) HTML 파싱, CSS 파싱, 자바스크립트 실행, 레이아웃 계산, 페인팅 등의 작업은 각각의 전용 스레드가 비동기적으로 처리되며, 특히 레이아웃/페인팅과 같은 작업은 컴포지터 스레드에서 처리됨
ex) Web Worker나 fetch, timer 등 비동기 API는 브라우저의 백그라운드 스레드에서 실행됨
이런 구조 덕분에 메인 스레드가 차단되지 않도록 하면서도 사용자 경험을 향상시킬 수 있음

## JavaScript가 Layout에 어떤 영향을 미치나?

JS는 DOM 조작을 통해 Layout울 직접 유발할 수 있음

```jsx
const el = document.getElementById("box");
el.style.width = "500px"; // 스타일 변경 → Layout 필요
console.log(el.offsetWidth); // 읽기 → 즉시 강제 Reflow 발생
```

**JS로 인해 발생하는 렌더링 비용 3종**

- `Reflow (Layout)`: DOM의 구조/크기/위치가 바뀌어 → 전체 또는 일부 레이아웃 재계산
- `Repaint (Paint)`: 스타일(색상, 그림자 등)만 바뀐 경우 → 다시 그림
- `Compositing`: 레이어 조합만 새로 함 (애니메이션 등)
  ```bash
  CSS 변경 속성
   └── top, width, height → Layout → Reflow → Repaint → CPU
   └── background-color   → Repaint만 필요 → CPU
   └── transform, opacity → Compositing만 필요 → GPU
  ```

JS는 메인 스레드에서 실행되고, 그 결과로 **DOM과 CSSOM이 바뀌면** → **레이아웃(Layout) → 페인트(Paint)** 까지 영향을 미침. 따라서 **JS는 렌더링 파이프라인 전체에 영향을 줄 수 있는 가장 핵심적인 요소**임

- JS로 많은 DOM 조작이 필요할 때: 변화들을 모아서 한 번에 처리 (Batch update)
- 성능 향상: `will-change`, `transform`, `opacity`로 GPU 이용 유도
- Reflow 방지: DOM 크기 읽기 전에 스타일 바꾸지 않기

## Dom

JavaScript는 BOM(Browser Object Model) 와 DOM(Document Object Model)라는 2개의 모델로 이루어져 있음

**BOM: Browser Object Model 브라우저 객체 모델**

웹페이지의 내용을 제외한 브라우저창에 포함된 모든 객체 요소들, window제어

- location: url 주소에 대한 정보 제공
- history 방문기록 정보 제공

**DOM: Document Object Model : 문서객체 모델 ⇒ document: 현재 눈에 보이는 웹문서에 대한 제어와 변경**

- 태그: Javascript가 활용할 수 있는 객체로 문서객체
  HTML 문서의 객체 표현.(W3C에 명세가 정해져있음)
  웹 브라우저가 html 페이지를 인식하는 방식.

돔객체는 html과 javascript를 연결해주는 통역사 같은 역할. 브라우저들은 사용자가 띄운 웹문서를 그 구성과 내용에 맞게 객체화하여 각요소별로 구조화함. 이 요소들은 병렬구조로 체계화되는데 이 document에 대한 모든 내용을 담고있는 객체를 DOM이라고 함.

## `Reflow` vs `Repaint` 차이

브라우저 렌더링 과정에서 Reflow와 Repaint는 모두 화면을 다시 그리는 작업이지만, 그 대상과 비용에서 차이가 있음.

Reflow는 요소의 위치나 크기 같은 레이아웃 정보가 변경될 때 발생하며, 브라우저는 전체 또는 일부 DOM 트리를 다시 계산해야 함. 이 작업은 비용이 크고 성능에 직접적인 영향을 줌

반면에 Repaint는 요소의 레이아웃은 그대로지만, 색상, 배경, 테두리 같은 시각적인 스타일이 바뀔 때 발생. 레이아웃 재계산은 필요 없고, 시각 요소만 다시 그리므로 상대적으로 비용이 낮음

## JS 실행 중 DOM 업데이트는 언제 적용되나요?

JavaScript 실행 중 DOM 조작이 일어나더라도, DOM 변경은 즉시 화면에 반영되지는 않음.
브라우저는 JS 실행이 완료된 후, 이벤트 루프가 빈 상태가 되면 렌더링을 한 번에 수행함.

-> DOM 변경은 메모리 상에는 반영되지만, 화면에 실제로 보이는 렌더링은 JS 실행이 끝나고 다음 프레임에서 이루어짐. 이 때문에 연속된 DOM 업데이트는 브라우저가 최적화해 묶어서 처리하며, 예를 들어 requestAnimationFrame을 사용하면 렌더링 타이밍을 조절할 수 있음.
