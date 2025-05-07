# CORS

## CORS란 무엇인가요?

CORS(Cross-Origin Resource Sharing)는 브라우저의 보안 정책인 '동일 출처 정책(SOP)Same-Origin-Policy'(요청을 보내기 위해서는 요청을 보내고자 하는 대상과 프로토콜도 같아야 하고, 포트도 같아야 함)을 우회하기 위한 메커니즘으로, 서로 다른 출처 간의 HTTP 요청을 허용할지 여부를 서버가 응답 헤더를 통해 명시하는 방식.

## 동일 출처 정책(Same Origin Policy)이란?

브라우저가 보안을 위해, 다른 출처(프로토콜/도메인/포트 중 하나라도 다르면)를 가진 리소스에 대해 자바스크립트에서 접근하거나 요청을 보내는 것을 제한하는 정책

## CORS 이슈가 발생하는 상황은?

프론트엔드가 API를 요청할 때 서버의 도메인이 다르면, 브라우저가 보안을 위해 요청을 차단

예: [`localhost:3000`](http://localhost:3000) → [`api.example.com`](http://api.example.com) 로 요청시

## 서버에서 CORS를 허용하려면 어떻게 해야 하나요?

서버는 HTTP 응답 헤더에 다음과 같은 항목을 포함해야 함:

```
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: GET, POST, ...
Access-Control-Allow-Headers: Content-Type
// 민감한 데이터나 인증 정보가 포함될 경우 Origin을 * 대신 명시적으로 설정해야함
```

## Preflight 요청이란?

HTTP 의 `OPTIONS` 메서드를 사용하며 `Access-Control-Request-*` 형태의 헤더로 전송하는 사전 요청으로, 브라우저가 실제 요청 전에 서버에 CORS 허용 여부를 확인하기 위해 자동으로 보냄.

브라우저가 강제하며 HTTP `OPTION` 요청 메서드를 이용해 서버로부터 지원 중인 메서드들을 내려 받은 뒤, 서버에서 `approval(승인)` 시에 실제 HTTP 요청 메서드를 이용해 실제 요청을 전송하는 것

주로 `Content-Type: application/json` , PUT, DELETE 등의 요청에서 발생

## CORS 문제는 백엔드에서 해결해야 하나요, 프론트에서 해결해야 하나요?

클라이언트가 조작할 수 없는 브라우저의 보안 정책이기 때문에 주로 서버에서 해결해야 함.

## CORS를 우회할 수 있는 방법은?

- 개발 중 프록시 서버 설정 (e.g. `vite.config.js`, `webpack-dev-server`)
- 서버에 CORS 허용 헤더 추가
- Nginx/Cloudflare와 같은 리버스 프록시 설정

## CORS는 무엇인가 왜 이러한 방법이 정의 되었으며, 본인이 코드를 작성하면서 CORS와 관련하여서 경험하였던 이슈는 무엇인가\*\*

CORS란 도메인 또는 포트가 다른 서버의 자원을 요청하면 발생 하는 문제.(예전에는 동일 출처 정책이 맞았음) 프론트엔드와 백엔드를 분리하고 처음 프론트엔드 프로젝트 결과물 클라이언트에서 백엔드에 접근했을 때 cors 발동. 나중에 image/다른 첨부파일들을 외부 서버에 저장한다고 했을 때 해당 서버로 자료 요청할 때 cors를 마주한 적이 있음. 웹 프론트 측에서 request header에 CORS 관련 옵션을 넣어주고, 서버에서는 해당 프론트 요청을 허용해서 해결.

## CORS가 `OPTIONS`로 요청이 가는 이유는?

브라우저는 보안상 교차 출처 요청(Cross-Origin Request) 중 일부를 사전 검사(preflight request) 하도록 설계되어 있음.

이때 "안전하지 않은 요청", 즉 Content-Type이 application/json, text/plain이 아닌 경우, 또는 Authorization 헤더 같은 커스텀 헤더를 포함한 요청은

먼저 서버에 OPTIONS 메서드로 사전 요청을 보내어, 실제 요청이 가능한지를 확인.

## `Access Control Allow Credentials`는 왜 쓰나요?

기본적으로 CORS 요청은 인증 정보(쿠키, 인증 헤더, 세션)를 포함하지 않음.
만약 클라이언트가 fetch(..., { credentials: 'include' })를 사용해
쿠키나 세션을 함께 보내고자 한다면, 서버에서 Access-Control-Allow-Credentials: true 명시적으로 허용해야 함. 이 헤더가 없으면, 브라우저는 보안상 이유로 인증 정보를 요청에 포함하지 않으며,
클라이언트와 서버 간 인증 기반 통신이 불가능함.
