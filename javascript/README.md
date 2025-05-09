## 카테고리

- [JavaScript 기본 개념](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics)
- [실행 컨텍스트 / 스코프 / 클로저](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure)
- 객체 & 프로토타입 & 클래스
- 함수와 this
- 이벤트 & DOM
- 비동기 & 동시성
- ECMAScript
- 가비지컬랙터
- 함수형 프로그래밍
- 프로젝트

## 질문지

### JavaScript 기본 개념

| 질문                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |  중요도  |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------: |
| [JS 타입에는 어떠한 것들이 있나요? (primitive / reference)](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#js-%ED%83%80%EC%9E%85%EC%97%90%EB%8A%94-%EC%96%B4%EB%96%A0%ED%95%9C-%EA%B2%83%EB%93%A4%EC%9D%B4-%EC%9E%88%EB%82%98%EC%9A%94-primitive--reference)                                                                                                                                                                                                                                                                                                                                   | ⭐️ 필수 |
| [Symbol이란?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#symbol%EC%9D%B4%EB%9E%80)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | ✅ 중요  |
| [null과 undefined, undeclared의 차이는 무엇이고 이 상태는 어떻게 확인할 수 있나요?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#null%EA%B3%BC-undefined-undeclared%EC%9D%98-%EC%B0%A8%EC%9D%B4%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%B4%EA%B3%A0-%EC%9D%B4-%EC%83%81%ED%83%9C%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%ED%99%95%EC%9D%B8%ED%95%A0-%EC%88%98-%EC%9E%88%EB%82%98%EC%9A%94)                                                                                                                                                                                                           | ⭐️ 필수 |
| [`typeof`, `instanceof`의 차이](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#typeof-instanceof%EC%9D%98-%EC%B0%A8%EC%9D%B4)                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | ✅ 중요  |
| [`Object.is()`와 `===` 차이](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#objectis%EC%99%80--%EC%B0%A8%EC%9D%B4)                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | 🔍 참고  |
| [객체의 얕은 복사와 깊은 복사란?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#%EA%B0%9D%EC%B2%B4%EC%9D%98-%EC%96%95%EC%9D%80-%EB%B3%B5%EC%82%AC%EC%99%80-%EA%B9%8A%EC%9D%80-%EB%B3%B5%EC%82%AC%EB%9E%80)                                                                                                                                                                                                                                                                                                                                                                                    | ⭐️ 필수 |
| [깊은 복사 방법](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#%EA%B9%8A%EC%9D%80-%EB%B3%B5%EC%82%AC-%EB%B0%A9%EB%B2%95)                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | ✅ 중요  |
| [`Object.assign()`과 스프레드 연산자(`...`)의 얕은 복사 차이점?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#objectassign%EA%B3%BC-%EC%8A%A4%ED%94%84%EB%A0%88%EB%93%9C-%EC%97%B0%EC%82%B0%EC%9E%90%EC%9D%98-%EC%96%95%EC%9D%80-%EB%B3%B5%EC%82%AC-%EC%B0%A8%EC%9D%B4%EC%A0%90)                                                                                                                                                                                                                                                                                                             | 🔍 참고  |
| [깊은 복사 시 성능 이슈는 어떻게 해결할 수 있을까?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#%EA%B9%8A%EC%9D%80-%EB%B3%B5%EC%82%AC-%EC%8B%9C-%EC%84%B1%EB%8A%A5-%EC%9D%B4%EC%8A%88%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%ED%95%B4%EA%B2%B0%ED%95%A0-%EC%88%98-%EC%9E%88%EC%9D%84%EA%B9%8C)                                                                                                                                                                                                                                                                                               | 🔍 참고  |
| [구조 분해 할당은 얕은 복사일까 깊은 복사일까?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#%EA%B5%AC%EC%A1%B0-%EB%B6%84%ED%95%B4-%ED%95%A0%EB%8B%B9%EC%9D%80-%EC%96%95%EC%9D%80-%EB%B3%B5%EC%82%AC%EC%9D%BC%EA%B9%8C-%EA%B9%8A%EC%9D%80-%EB%B3%B5%EC%82%AC%EC%9D%BC%EA%B9%8C)                                                                                                                                                                                                                                                                                                              | 🔍 참고  |
| [primitive type에서 빌트인 메소드를 사용할 수 있는 이유는?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#primitive-type%EC%97%90%EC%84%9C-%EB%B9%8C%ED%8A%B8%EC%9D%B8-%EB%A9%94%EC%86%8C%EB%93%9C%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%A0-%EC%88%98-%EC%9E%88%EB%8A%94-%EC%9D%B4%EC%9C%A0%EB%8A%94)                                                                                                                                                                                                                                                                                             | ✅ 중요  |
| [`==`와 `===`의 차이점은 무엇인가요?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#%EC%99%80-%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80%EC%9A%94)                                                                                                                                                                                                                                                                                                                                                                                                   | ⭐️ 필수 |
| [명시적 형변환과 묵시적 형변환의 차이점은?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#%EB%AA%85%EC%8B%9C%EC%A0%81-%ED%98%95%EB%B3%80%ED%99%98%EA%B3%BC-%EB%AC%B5%EC%8B%9C%EC%A0%81-%ED%98%95%EB%B3%80%ED%99%98%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%80)                                                                                                                                                                                                                                                                                                                             | ✅ 중요  |
| [타입 강제 변환이란 무엇인가요? JavaScript에서 타입 강제 변환을 신뢰해서 생기는 흔한 문제점은 어떤 것들이 있나요?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#%ED%83%80%EC%9E%85-%EA%B0%95%EC%A0%9C-%EB%B3%80%ED%99%98%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80%EC%9A%94-javascript%EC%97%90%EC%84%9C-%ED%83%80%EC%9E%85-%EA%B0%95%EC%A0%9C-%EB%B3%80%ED%99%98%EC%9D%84-%EC%8B%A0%EB%A2%B0%ED%95%B4%EC%84%9C-%EC%83%9D%EA%B8%B0%EB%8A%94-%ED%9D%94%ED%95%9C-%EB%AC%B8%EC%A0%9C%EC%A0%90%EC%9D%80-%EC%96%B4%EB%96%A4-%EA%B2%83%EB%93%A4%EC%9D%B4-%EC%9E%88%EB%82%98%EC%9A%94) | ✅ 중요  |
| [JS에서 배열이란?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#js%EC%97%90%EC%84%9C-%EB%B0%B0%EC%97%B4%EC%9D%B4%EB%9E%80)                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | ✅ 중요  |
| [자바스크립트의 배열이 실제 자료구조 배열이 아닌데 그 이유는?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-%EB%B0%B0%EC%97%B4%EC%9D%B4-%EC%8B%A4%EC%A0%9C-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EB%B0%B0%EC%97%B4%EC%9D%B4-%EC%95%84%EB%8B%8C%EB%8D%B0-%EA%B7%B8-%EC%9D%B4%EC%9C%A0%EB%8A%94)                                                                                                                                                                                                                               | 🔍 참고  |
| [객체의 속성이나 배열의 요소를 순회할 때 어떤 언어 구문을 사용하시나요?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#%EA%B0%9D%EC%B2%B4%EC%9D%98-%EC%86%8D%EC%84%B1%EC%9D%B4%EB%82%98-%EB%B0%B0%EC%97%B4%EC%9D%98-%EC%9A%94%EC%86%8C%EB%A5%BC-%EC%88%9C%ED%9A%8C%ED%95%A0-%EB%95%8C-%EC%96%B4%EB%96%A4-%EC%96%B8%EC%96%B4-%EA%B5%AC%EB%AC%B8%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%98%EC%8B%9C%EB%82%98%EC%9A%94)                                                                                                                                                                               | ✅ 중요  |
| [`Array.forEach()` 루프와 `Array.map()` 메서드의 주요 차이점은 무엇이며, 상황에 따라 어떤 것을 선택하나요?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#arrayforeach-%EB%A3%A8%ED%94%84%EC%99%80-arraymap-%EB%A9%94%EC%84%9C%EB%93%9C%EC%9D%98-%EC%A3%BC%EC%9A%94-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EB%A9%B0-%EC%83%81%ED%99%A9%EC%97%90-%EB%94%B0%EB%9D%BC-%EC%96%B4%EB%96%A4-%EA%B2%83%EC%9D%84-%EC%84%A0%ED%83%9D%ED%95%98%EB%82%98%EC%9A%94)                                                                                                             | ✅ 중요  |
| [배열을 순회할 수 있는 다른 주요 메서드들에는 어떤 것들이 있나요?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#%EB%B0%B0%EC%97%B4%EC%9D%84-%EC%88%9C%ED%9A%8C%ED%95%A0-%EC%88%98-%EC%9E%88%EB%8A%94-%EB%8B%A4%EB%A5%B8-%EC%A3%BC%EC%9A%94-%EB%A9%94%EC%84%9C%EB%93%9C%EB%93%A4%EC%97%90%EB%8A%94-%EC%96%B4%EB%96%A4-%EA%B2%83%EB%93%A4%EC%9D%B4-%EC%9E%88%EB%82%98%EC%9A%94)                                                                                                                                                                                                                | 🔍 참고  |
| [삼항 연산자에 대해 설명해주세요.](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#%EC%82%BC%ED%95%AD-%EC%97%B0%EC%82%B0%EC%9E%90%EC%97%90-%EB%8C%80%ED%95%B4-%EC%84%A4%EB%AA%85%ED%95%B4%EC%A3%BC%EC%84%B8%EC%9A%94)                                                                                                                                                                                                                                                                                                                                                                           | 🔍 참고  |
| [JavaScript에서 `while` 루프와 `do-while` 루프의 차이점은 무엇인가요?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#javascript%EC%97%90%EC%84%9C-while-%EB%A3%A8%ED%94%84%EC%99%80-do-while-%EB%A3%A8%ED%94%84%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80%EC%9A%94)                                                                                                                                                                                                                                                                                  | 🔍 참고  |
| [JavaScript 메모리 구조](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/javascript-basics#%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B5%AC%EC%A1%B0)                                                                                                                                                                                                                                                                                                                                                                                                                 | 🔍 참고  |

### 실행 컨텍스트 / 스코프 / 클로저

| 질문                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |  중요도  |
| :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------: |
| [var 와 let, const의 차이점은 무엇인가 (function scope와 block scope의 개념에서)](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#var-%EC%99%80-let-const%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-function-scope%EC%99%80-block-scope%EC%9D%98-%EA%B0%9C%EB%85%90%EC%97%90%EC%84%9C)                                                                                                   | ⭐️ 필수 |
| [`const`로 선언된 객체의 속성은 변경할 수 있나요? 가능하다면 어떻게 하나요?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#const%EB%A1%9C-%EC%84%A0%EC%96%B8%EB%90%9C-%EA%B0%9D%EC%B2%B4%EC%9D%98-%EC%86%8D%EC%84%B1%EC%9D%80-%EB%B3%80%EA%B2%BD%ED%95%A0-%EC%88%98-%EC%9E%88%EB%82%98%EC%9A%94-%EA%B0%80%EB%8A%A5%ED%95%98%EB%8B%A4%EB%A9%B4-%EC%96%B4%EB%96%BB%EA%B2%8C-%ED%95%98%EB%82%98%EC%9A%94)                          | ✅ 중요  |
| [객체 자체를 불변하게 만들고 싶다면?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#%EA%B0%9D%EC%B2%B4-%EC%9E%90%EC%B2%B4%EB%A5%BC-%EB%B6%88%EB%B3%80%ED%95%98%EA%B2%8C-%EB%A7%8C%EB%93%A4%EA%B3%A0-%EC%8B%B6%EB%8B%A4%EB%A9%B4)                                                                                                                                                                                                | ✅ 중요  |
| [TDZ란 무엇인가](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#tdz%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)                                                                                                                                                                                                                                                                                                               | ⭐️ 필수 |
| [호이스팅](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85)                                                                                                                                                                                                                                                                                                                                  | ⭐️ 필수 |
| [호이스팅의 종류](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85%EC%9D%98-%EC%A2%85%EB%A5%98)                                                                                                                                                                                                                                                                                               | ✅ 중요  |
| [자바스크립트 엔진의 해석 순서](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%97%94%EC%A7%84%EC%9D%98-%ED%95%B4%EC%84%9D-%EC%88%9C%EC%84%9C)                                                                                                                                                                                                                         | 🔍 참고  |
| [실행컨텍스트란 무엇이고 실행 컨텍스트 안에는 어떤 것들이 있나요?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#%EC%8B%A4%ED%96%89%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EA%B3%A0-%EC%8B%A4%ED%96%89-%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8-%EC%95%88%EC%97%90%EB%8A%94-%EC%96%B4%EB%96%A4-%EA%B2%83%EB%93%A4%EC%9D%B4-%EC%9E%88%EB%82%98%EC%9A%94)                                           | ⭐️ 필수 |
| [렉시컬 환경이란?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#%EB%A0%89%EC%8B%9C%EC%BB%AC-%ED%99%98%EA%B2%BD%EC%9D%B4%EB%9E%80)                                                                                                                                                                                                                                                                                              | ✅ 중요  |
| [Scope는 무엇인가?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#scope%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)                                                                                                                                                                                                                                                                                                          | ⭐️ 필수 |
| [ES5와 ES6의 스코프 차이는?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#es5%EC%99%80-es6%EC%9D%98-%EC%8A%A4%EC%BD%94%ED%94%84-%EC%B0%A8%EC%9D%B4%EB%8A%94)                                                                                                                                                                                                                                                                   | ✅ 중요  |
| [스코프 체인이란?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#%EC%8A%A4%EC%BD%94%ED%94%84-%EC%B2%B4%EC%9D%B8%EC%9D%B4%EB%9E%80)                                                                                                                                                                                                                                                                                              | ⭐️ 필수 |
| [식별자 해결이란?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#%EC%8B%9D%EB%B3%84%EC%9E%90-%ED%95%B4%EA%B2%B0%EC%9D%B4%EB%9E%80)                                                                                                                                                                                                                                                                                              | ✅ 중요  |
| [스코프 체인을 통해 식별자 해결을 하는 과정 & 프로토타입과의 관계 ](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#%EC%8A%A4%EC%BD%94%ED%94%84-%EC%B2%B4%EC%9D%B8%EC%9D%84-%ED%86%B5%ED%95%B4-%EC%8B%9D%EB%B3%84%EC%9E%90-%ED%95%B4%EA%B2%B0%EC%9D%84-%ED%95%98%EB%8A%94-%EA%B3%BC%EC%A0%95--%ED%94%84%EB%A1%9C%ED%86%A0%ED%83%80%EC%9E%85%EA%B3%BC%EC%9D%98-%EA%B4%80%EA%B3%84)                                                 | 🔍 참고  |
| [Lexical Scope / 렉시컬 스코프 / 정적 스코프란?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#lexical-scope--%EB%A0%89%EC%8B%9C%EC%BB%AC-%EC%8A%A4%EC%BD%94%ED%94%84--%EC%A0%95%EC%A0%81-%EC%8A%A4%EC%BD%94%ED%94%84%EB%9E%80)                                                                                                                                                                                                 | ✅ 중요  |
| [Scope binding](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#scope-binding)                                                                                                                                                                                                                                                                                                                                                    | 🔍 참고  |
| [스코프를 속일 수 있는 방법은? 혹은 동적으로 스코프를 생성할 수 있는 방법은?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#%EC%8A%A4%EC%BD%94%ED%94%84%EB%A5%BC-%EC%86%8D%EC%9D%BC-%EC%88%98-%EC%9E%88%EB%8A%94-%EB%B0%A9%EB%B2%95%EC%9D%80-%ED%98%B9%EC%9D%80-%EB%8F%99%EC%A0%81%EC%9C%BC%EB%A1%9C-%EC%8A%A4%EC%BD%94%ED%94%84%EB%A5%BC-%EC%83%9D%EC%84%B1%ED%95%A0-%EC%88%98-%EC%9E%88%EB%8A%94-%EB%B0%A9%EB%B2%95%EC%9D%80) | 🔍 참고  |
| [클로저란?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#%ED%81%B4%EB%A1%9C%EC%A0%80%EB%9E%80)                                                                                                                                                                                                                                                                                                                                 | ⭐️ 필수 |
| [클로저 메모리 누수 예시](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#%ED%81%B4%EB%A1%9C%EC%A0%80-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%88%84%EC%88%98-%EC%98%88%EC%8B%9C)                                                                                                                                                                                                                                                          | ✅ 중요  |
| [IIFE 사용 이유와 클로저와의 관계](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#iife-%EC%82%AC%EC%9A%A9-%EC%9D%B4%EC%9C%A0%EC%99%80-%ED%81%B4%EB%A1%9C%EC%A0%80%EC%99%80%EC%9D%98-%EA%B4%80%EA%B3%84)                                                                                                                                                                                                                          | ✅ 중요  |
| [Global Object 란?](https://github.com/SeoYeonii/frontend-interview/tree/main/javascript/context-scope-closure#global-object-%EB%9E%80)                                                                                                                                                                                                                                                                                                                                      | ✅ 중요  |

### 객체 & 프로토타입 & 클래스

| 질문                                                                           |  중요도  |
| :----------------------------------------------------------------------------- | :------: |
| 프로토타입이란?                                                                | ⭐️ 필수 |
| 프로토타입 체이닝이란?                                                         | ⭐️ 필수 |
| 프로토타입의 상속이란?                                                         | ✅ 중요  |
| Object의 프로토타입은?                                                         | ✅ 중요  |
| Class의 최상단 프로토 타입은 무엇인가?                                         | 🔍 참고  |
| JavaScript의 프로토타입 기반 상속(prototypal inheritance)은 어떻게 동작하나요? | ⭐️ 필수 |
| 호스트 객체(Host Object)와 네이티브 객체(Native Object)의 차이는 무엇인가요?   | ✅ 중요  |
| 내장 객체(Built-in Object)를 확장하는 것의 장단점은 무엇인가요?                | ✅ 중요  |
| 클래스 vs 함수 생성자                                                          | ⭐️ 필수 |
| 생성자 함수와 new 키워드                                                       | ✅ 중요  |
| 정적(static) 클래스 멤버를 정의하는 이유는 무엇인가요?                         | ✅ 중요  |
| 싱글톤 패턴이란?                                                               | ✅ 중요  |
| Object.create(), Object.assign() 차이                                          | 🔍 참고  |
| ES6 클래스와 ES5 함수 생성자의 차이는 무엇인가요?                              | ✅ 중요  |

### 함수와 this

| 질문                                                                                              |  중요도  |
| :------------------------------------------------------------------------------------------------ | :------: |
| 함수의 정의 방식 (4가지)                                                                          | ✅ 중요  |
| `function Person() {}`, `var person = Person()`, `var person = new Person()`의 차이는 무엇인가요? | ✅ 중요  |
| `function foo() {}`와 `var foo = function() {}`는 어떤 차이가 있나요?                             | ✅ 중요  |
| this란 무엇인가?                                                                                  | ⭐️ 필수 |
| this안에는 뭐가 있는가?                                                                           | 🔍 참고  |
| this랑 같은 위치에 있는 객체 여러가지가 있는데 그것이 무엇인가?                                   | 🔍 참고  |
| this는 언제 결정되는가?                                                                           | ⭐️ 필수 |
| 참조하는 this를 바꿀 수 있는 방법                                                                 | ✅ 중요  |
| Call, Apply, Bind 함수에 대해 설명해주세요.                                                       | ⭐️ 필수 |
| `Function.call()`과 `Function.apply()`는 무엇을 하는 함수이며, 둘의 차이는 무엇인가요?            | ⭐️ 필수 |
| `Function.prototype.bind()`는 무엇인가요?                                                         | ⭐️ 필수 |
| 화살표 함수 vs 일반 함수의 this                                                                   | ⭐️ 필수 |
| class에서의 this 특징                                                                             | ✅ 중요  |
| class와 function에서 this의 차이                                                                  | ✅ 중요  |
| button에 eventlistener에서 callback에서 this는 뭘 가리키나요?                                     | ✅ 중요  |
| 화살표 함수란?                                                                                    | ✅ 중요  |
| 화살표 함수(`=>`)를 사용하는 이유는 무엇이며, 기존 함수와 어떤 차이가 있나요?                     | ⭐️ 필수 |
| Arrow function의 this 바인딩 특징을 설명해주세요.                                                 | ⭐️ 필수 |
| 생성자 내부 메서드에 화살표 함수를 사용하는 이점은 무엇인가요?                                    | ✅ 중요  |
| 일반 함수와 arrow 함수의 hoisting 차이는?                                                         | 🔍 참고  |
| function을 arrow function으로 리팩토링할때 주의할 점                                              | ✅ 중요  |
| 익명 함수(Anonymous function)의 대표적인 사용 예는 무엇인가요?                                    | ✅ 중요  |
| 선언적 함수랑 익명 함수의 차이점이 뭔가? / 익명함수와 아닌 함수의 차이점?                         | ✅ 중요  |
| 즉시실행함수 (IIFE)란? 왜 쓰는지 설명하시오                                                       | ✅ 중요  |
| 입급객체란?                                                                                       | 🔍 참고  |
| 고차 함수(Higher-order function)란 무엇인가요?                                                    | ✅ 중요  |
| ES5의 고차함수 7개                                                                                | 🔍 참고  |
| 자바스크립트 Argument 처리 구                                                                     | 🔍 참고  |
| Function Object를 생성할 때, 일어나는 일은? (function a(){})                                      | 🔍 참고  |
| new 키워드로 함수를 생성할 때, 일어나는 일 vs 그냥 함수를 만들면?                                 | ✅ 중요  |
| ES5의 map, forEach의 인자에 대해서 설명하시요                                                     | ✅ 중요  |

### 이벤트 & DOM

| 질문                                                           |  중요도  |
| :------------------------------------------------------------- | :------: |
| 이벤트 위임(Event Delegation)이란 무엇인가요?                  | ✅ 중요  |
| 이벤트 버블링(Event Bubbling)이란?                             | ⭐️ 필수 |
| 이벤트 캡처링(Event Capturing)이란?                            | ✅ 중요  |
| 실제 브라우저가 이벤트를 감지하는 방법                         | ✅ 중요  |
| 캡쳐링 단계에서 이벤트를 감지하는 방법                         | ✅ 중요  |
| 버블링/캡쳐링을 중단하는 방법                                  | ✅ 중요  |
| HTML 속성(attribute)과 DOM 속성(property)의 차이는?            | ✅ 중요  |
| `event.target`과 `event.currentTarget`의 차이는?               | ⭐️ 필수 |
| `event.preventDefault()`와 `event.stopPropagation()`의 차이는? | ⭐️ 필수 |
| 이벤트 위임은 언제 유리한가요?                                 | ✅ 중요  |
| addEventListener의 third 인자 options는 어떤 옵션이 있나요?    | 🔍 참고  |

### 비동기 & 동시성

| 질문                                                                     |  중요도  |
| :----------------------------------------------------------------------- | :------: |
| Node js는 싱글스레드인가요? 멀티 쓰레드 인가요?                          | ✅ 중요  |
| 이벤트 루프에 대해서 설명, 동시성 모델에 대해서 설명                     | ⭐️ 필수 |
| 콜 스택(Call Stack)과 태스크 큐(Task Queue)의 차이는 무엇인가요?         | ⭐️ 필수 |
| 동기/비동기 프로그래밍                                                   | ⭐️ 필수 |
| 동기(synchronous) 함수와 비동기(asynchronous) 함수의 차이는?             | ⭐️ 필수 |
| SetTimeout SetInterval                                                   | ✅ 중요  |
| 콜백 함수에 대해 설명해주세요.                                           | ✅ 중요  |
| 프로미스(Promise)란 무엇이며, 언제 어떻게 사용하나요?                    | ⭐️ 필수 |
| Promise chaining 에서 에러는 어떻게 핸들링하나요?                        | ✅ 중요  |
| async await에 대해 설명                                                  | ⭐️ 필수 |
| Microtask와 Macrotask 차이는?                                            | ✅ 중요  |
| AJAX란 무엇인가요?                                                       | ⭐️ 필수 |
| AJAX 요청이 완료되기 전에 DOM을 조작하려면 어떻게 해야 하나요?           | 🔍 참고  |
| fetch와 XMLHttpRequest의 주요 차이는 무엇인가요?                         | ✅ 중요  |
| AJAX는 항상 비동기인가요? 동기로 쓸 수 있나요?                           | 🔍 참고  |
| AJAX 요청에서 CORS 에러가 발생한 적이 있나요? 어떻게 해결했나요?         | ✅ 중요  |
| AJAX 요청 중 중복 요청이 생기는 경우 어떻게 처리하시나요?                | ✅ 중요  |
| AJAX 요청이 실패했을 때 사용자에게 어떻게 피드백을 주시나요?             | ✅ 중요  |
| fetch와 axios의 차이점은 무엇이며, 어떤 상황에서 어떤 것을 선호하시나요? | ✅ 중요  |
| WebWorker                                                                | 🔍 참고  |

### ECMAScript

| 질문                                                                       |  중요도  |
| :------------------------------------------------------------------------- | :------: |
| ECMA Script                                                                | 🔍 참고  |
| ES3 vs ES5                                                                 | 🔍 참고  |
| JavaScript로 컴파일되는 언어(TypeScript, Elm 등)를 사용하는 것의 장단점은? | ✅ 중요  |
| 객체나 배열 구조 분해 할당(Destructuring)의 예시를 들어주세요.             | ✅ 중요  |
| 템플릿 리터럴(Template Literal)로 문자열을 생성하는 예를 보여주세요.       | ✅ 중요  |
| 전개 연산자(spread)와 나머지 인자(rest)의 차이와 장점은?                   | ⭐️ 필수 |
| 옵셔널 체이닝, 널 병합 연산자 사용법 설명                                  | ⭐️ 필수 |
| `'use strict'` (strict mode)는 무엇이며, 장단점은 무엇인가요?              | ✅ 중요  |

### 가비지컬랙터

| 질문                                                              |  중요도  |
| :---------------------------------------------------------------- | :------: |
| 자바스크립트 가비지컬렉터                                         | ⭐️ 필수 |
| 가비지 컬렉터의 역할은? 어떻게 작동하는가?                        | ⭐️ 필수 |
| GC가 발생했는지 어떻게 알 수 있나요?                              | 🔍 참고  |
| JS 메모리 누수 원인 4가지                                         | ✅ 중요  |
| 클로저와 메모리 누수 관계 설명                                    | ✅ 중요  |
| 클로저를 사용하는 상황에서 메모리 누수를 어떻게 방지할 수 있나요? | ✅ 중요  |
| 브라우저에서의 메모리 최적화 방법은?                              | ✅ 중요  |
| WeakMap, WeakSet은 왜 사용하나요?                                 | ✅ 중요  |

### 함수형 프로그래밍

| 질문                                                                        |  중요도  |
| :-------------------------------------------------------------------------- | :------: |
| 함수형 프로그래밍                                                           | ✅ 중요  |
| 순수함수는 무엇인가요? 순수함수의 장점은?                                   | ⭐️ 필수 |
| 커링 함수(Curry Function)의 예와 이 문법이 주는 장점은 무엇인가요?          | ✅ 중요  |
| 메소드 체이닝이란 무엇이며, 이것의 장단점은 무엇인가?                       | ✅ 중요  |
| JavaScript로 객체지향 프로그래밍(OOP)을 적용할 때 어떤 식으로 접근하시나요? | ✅ 중요  |
| 싱글톤 패턴에 대해..                                                        | 🔍 참고  |
| 가변(Mutable) 객체와 불변(Immutable) 객체의 차이는?                         | ✅ 중요  |
| JavaScript에서 불변 객체의 예는?                                            | 🔍 참고  |
| 불변 객체를 사용할 때의 장단점은?                                           | ✅ 중요  |
| 코드에서 불변성을 어떻게 구현하나요?                                        | ✅ 중요  |
| Compose, Pipe는 무엇인가요?                                                 | 🔍 참고  |
| Ramda, Lodash 등 함수형 라이브러리 써본 경험 있나요?                        | 🔍 참고  |

### 프로젝트

| 질문                                                                |  중요도  |
| :------------------------------------------------------------------ | :------: |
| input에 딜레이를 걸려면 어떻게 할까요?                              | ✅ 중요  |
| 디바운스, 쓰로틀에 대해 설명해주세요. 코드를 직접 작성할 수 있는지? | ⭐️ 필수 |
| JavaScript 코드를 디버깅할 때 사용하는 도구나 기법은 무엇인가요?    | ⭐️ 필수 |
| 여러 파일 간 코드를 공유하는 방법에는 어떤 것들이 있나요?           | ✅ 중요  |
| 코드 스플리팅이 필요한 이유는?                                      | ✅ 중요  |
| 웹팩/번들러 없이 JS 프로젝트 구조를 어떻게 관리하나요?              | 🔍 참고  |
| Webpack과 Vite의 차이는?                                            | ✅ 중요  |
| 번들링과 트리 쉐이킹(Tree-shaking)이란?                             | ⭐️ 필수 |
| Dynamic Import란?                                                   | ✅ 중요  |
| SPA에서 초기 로딩을 최적화하려면?                                   | ✅ 중요  |
| JS 프로젝트 디렉토리 구조를 어떻게 구성하나요?                      | 🔍 참고  |
