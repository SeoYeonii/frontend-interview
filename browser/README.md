## 카테고리

- 브라우저 구조 및 렌더링 엔진
- 브라우저 저장소
- 최적화
- CORS
- Web Server / WAS
- 크로스브라우징

## 질문지

### 브라우저 구조 및 렌더링 엔진

| 질문                                                                                                                                                                                                                                                                                                                                                                                      |  중요도  |
| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------: |
| [브라우저 정의 & 구성요소](https://github.com/SeoYeonii/frontend-interview/tree/main/browser/browser-rendering#%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EC%A0%95%EC%9D%98--%EA%B5%AC%EC%84%B1%EC%9A%94%EC%86%8C)                                                                                                                                                                             | ✅ 중요  |
| [웹 브라우저에서 사이트를 렌더링 하는 과정이 어떻게 되나요](https://github.com/SeoYeonii/frontend-interview/tree/main/browser/browser-rendering#%EC%9B%B9-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%B8%EC%97%90%EC%84%9C-%EC%82%AC%EC%9D%B4%ED%8A%B8%EB%A5%BC-%EB%A0%8C%EB%8D%94%EB%A7%81-%ED%95%98%EB%8A%94-%EA%B3%BC%EC%A0%95%EC%9D%B4-%EC%96%B4%EB%96%BB%EA%B2%8C-%EB%90%98%EB%82%98%EC%9A%94) | ⭐️ 필수 |
| [렌더링 엔진은 멀티스레드로 동작하는가?](https://github.com/SeoYeonii/frontend-interview/tree/main/browser/browser-rendering#%EB%A0%8C%EB%8D%94%EB%A7%81-%EC%97%94%EC%A7%84%EC%9D%80-%EB%A9%80%ED%8B%B0%EC%8A%A4%EB%A0%88%EB%93%9C%EB%A1%9C-%EB%8F%99%EC%9E%91%ED%95%98%EB%8A%94%EA%B0%80)                                                                                                | 🔍 참고  |
| [JavaScript가 Layout에 어떤 영향을 미치나?](https://github.com/SeoYeonii/frontend-interview/tree/main/browser/browser-rendering#javascript%EA%B0%80-layout%EC%97%90-%EC%96%B4%EB%96%A4-%EC%98%81%ED%96%A5%EC%9D%84-%EB%AF%B8%EC%B9%98%EB%82%98)                                                                                                                                           | ✅ 중요  |
| [DOM](https://github.com/SeoYeonii/frontend-interview/tree/main/browser/browser-rendering#dom)                                                                                                                                                                                                                                                                                            | ⭐️ 필수 |
| [Reflow vs Repaint 차이](https://github.com/SeoYeonii/frontend-interview/tree/main/browser/browser-rendering#reflow-vs-repaint-%EC%B0%A8%EC%9D%B4)                                                                                                                                                                                                                                        | ✅ 중요  |
| DOMContentLoaded vs load 이벤트 차이                                                                                                                                                                                                                                                                                                                                                      | 🔍 참고  |
| 렌더링 차단 리소스 예시                                                                                                                                                                                                                                                                                                                                                                   | 🔍 참고  |
| [JS 실행 중 DOM 업데이트는 언제 적용되나요?](https://github.com/SeoYeonii/frontend-interview/tree/main/browser/browser-rendering#js-%EC%8B%A4%ED%96%89-%EC%A4%91-dom-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8%EB%8A%94-%EC%96%B8%EC%A0%9C-%EC%A0%81%EC%9A%A9%EB%90%98%EB%82%98%EC%9A%94)                                                                                                      | 🔍 참고  |

### 브라우저 저장소

| 질문                                              |  중요도  |
| :------------------------------------------------ | :------: |
| 쿠키(Cookie)와 세션(Session)의 차이는 무엇인가요? | ⭐️ 필수 |
| 쿠키, localStorage, sessionStorage의 차이         | ⭐️ 필수 |
| localStorage에 JWT 토큰을 저장해도 괜찮을까요?    | ⭐️ 필수 |
| HTTP-only 쿠키란?                                 | ✅ 중요  |
| 브라우저 저장소는 언제 어떤 걸 써야 하나요?       | ✅ 중요  |
| 브라우저가 쿠키를 어떻게 전송하나요?              | ✅ 중요  |
| XSS (Cross-Site Scripting) 공격                   | ⭐️ 필수 |
| CSRF (Cross-Site Request Forgery)                 | ⭐️ 필수 |
| XSS vs CSRF                                       | ✅ 중요  |
| SSR + 로그인 인증 시 토큰 어디에 저장하세요?      | ⭐️ 필수 |
| SameSite 쿠키 속성에 대해 설명해주세요            | ✅ 중요  |
| Secure, HttpOnly 쿠키 속성은 왜 필요한가요?       | ✅ 중요  |
| 쿠키에 저장 가능한 용량은 얼마나 되나요?          | 🔍 참고  |
| localStorage는 브라우저 간 공유되나요?            | 🔍 참고  |

### 최적화

| 질문                                                                                   |  중요도  |
| :------------------------------------------------------------------------------------- | :------: |
| 웹 최적화 기법이 뭐고, 어떠한 것들이 있나요?                                           | ⭐️ 필수 |
| 당신은 어떤 웹사이트의 assets/resources를 어떻게 최적화 할것인가요?                    | ⭐️ 필수 |
| 브라우저가 주어진 도메인에 대해 자원들을 한번에 얼마나 다운로드 하나요? 그리고 예외는? | ✅ 중요  |
| 웹 성능과 관련된 이슈                                                                  | ✅ 중요  |
| TTI, FCP 등의 렌더링 지표                                                              | 🔍 참고  |
| SPA 성능 병목은 어디서 발생할까요?                                                     | 🔍 참고  |

### CORS

| 질문                                                                |  중요도  |
| :------------------------------------------------------------------ | :------: |
| CORS란 무엇인가요?                                                  | ⭐️ 필수 |
| 동일 출처 정책(Same-Origin Policy)이란?                             | ⭐️ 필수 |
| CORS 이슈가 발생하는 상황은?                                        | ✅ 중요  |
| 서버에서 CORS를 허용하려면 어떻게 해야 하나요?                      | ✅ 중요  |
| Preflight 요청이란?                                                 | ✅ 중요  |
| CORS 문제는 백엔드에서 해결해야 하나요, 프론트에서 해결해야 하나요? | 🔍 참고  |
| CORS를 우회할 수 있는 방법은?                                       | 🔍 참고  |
| CORS란 무엇이고 실무 경험 공유                                      | ⭐️ 필수 |
| CORS가 OPTIONS로 요청이 가는 이유는?                                | ✅ 중요  |
| Access-Control-Allow-Credentials는 왜 쓰나요?                       | ✅ 중요  |

### Web Server / WAS

| 질문                                            |  중요도  |
| :---------------------------------------------- | :------: |
| Web Server VS WAS                               | ⭐️ 필수 |
| 웹서버와 WAS를 분리한 이유는?                   | ✅ 중요  |
| Static pages vs Dynamic Pages                   | ✅ 중요  |
| WAS가 웹 서버 역할까지 다 하지 않는 이유?       | ✅ 중요  |
| Nginx와 Express의 역할 차이                     | ⭐️ 필수 |
| 정적 파일은 어디에서 서빙하는 게 좋은가요?      | ✅ 중요  |
| WAS 과부하를 줄이기 위한 방법은?                | ✅ 중요  |
| React 앱 배포 시 웹 서버와 WAS 역할             | ✅ 중요  |
| 웹 서버 없이 WAS만 사용할 수 있나요?            | 🔍 참고  |
| Reverse Proxy란?                                | ⭐️ 필수 |
| React 앱에서 Nginx의 역할은?                    | ✅ 중요  |
| nginx.conf에서 정적 파일 라우팅 방식 설명 가능? | 🔍 참고  |

### 크로스브라우징

| 질문                                      |  중요도  |
| :---------------------------------------- | :------: |
| 크로스 브라우징이란?                      | ⭐️ 필수 |
| 웹 표준과 표준 제정 기관이 왜 중요한가요? | ✅ 중요  |
| 크로스 브라우징 대응 전략은?              | ✅ 중요  |
| canIuse, autoprefixer 등 도구 활용 여부?  | 🔍 참고  |
