# ECMAScript

## ECMA Script

ECMAScript(ECMA)는 자바스크립트의 표준 명세. 브라우저에서 동작하는 JavaScript는 ECMAScript 표준을 기반으로 구현되어 있으며, ES6 이후 매년 새로운 기능이 추가되는 중

Javascript는 1995년 넷스케이프(현재 파이어폭스) 웹페이지에 동적인 요소를 구현하기 위해 발명. 다양한 웹 브라우저들에서 JS가 잘 작동하기 위해서는 표준 규격이 필요해짐. 그래서 ECMA 국제 기구에서 ECMAScript standard 표준을 만듬

- 언어 구문(키워드, 객체 리터럴 초기화 등)
- 오류 처리 방법
- 자료형 등등
- `ES6(ES2015)`
  ECMA라는 국제 기구에서 만든 표준문서인 ECMAScript(ES)의 6번째 개정판 문서에 있는 표준 스펙. 6번째 버전은 2015에 나왔기 때문에 ES2015라고도 함. ES7은 2016에 나와 ES2016이라고도 함.

  - `const, let`
    var: 함수 단위 스코프, const, let: 블록 단위 스코프
    - 블록스코프: if, while, for, function 등에서 사용하는 중괄호에 속하는 범위를 뜻함. 따라서 const와 let을 이 중괄호 안에서 사용하게 된다면, 그 스코프 범위 안에서만 접근이 가능. 이를 통해 호이스팅에 관련된 문제는 자연스럽게 해결가능!
  - `템플릿 문자열`
    백틱(₩)을 이용해 새로운 문자열을 만들 수 있음.

    ```jsx
    var str = num1 + " + " + num2 + " = " + num3;

    const str2 = `${num1} + ${num2} = ${num3}`;
    ```

  - `객체 리터럴`

    ```jsx
    // Old Object
    var sayNode = function () {
      console.log("Node");
    };

    var es = "ES";
    var oldObject = {
      sayJS: function () {
        console.log("JS");
      },
      sayNode: sayNode,
    };

    oldObject[es + 6] = "Fantastic";

    oldObject.sayNode();
    oldObject.sayJS();
    console.log(oldObject.ES6);
    ```

    ```jsx
    // New Object
    var sayNode = function () {
      console.log("Node");
    };

    var es = "ES";

    const newObject = {
      sayJS() {
        console.log("JS");
      },
      sayNode,
      [es + 6]: "Fantastic",
    };

    newObject.sayNode();
    newObject.sayJS();
    console.log(newObject.ES6);
    ```

    객체의 메서드에 함수를 연결할 때, 이제 : 와같은 콜론과 function을 붙이지 않아도 가능해졌음.
    또한 `sayNode : sayNode` 같이 중복되는 이름의 변수는 그냥 간단히 sayNode 하나만 작성하면 됨.
    또한 객체의 속성명을 동적으로 생성이 가능. 이전에는 객체 리터럴 밖에서 [ES+6]으로 만들었지만, 이제 객체 리터럴 안에서 만들 수 있는 모습을 확인할 수 있음.

  - `⇒`
    function 대신 ⇒ 기호로 선언. return 문을 줄일 수 있는 장점. this 바인드 방식에서 차이점이 존재
    ⇒ 사용하면 바깥 스코프의 this를 그대로 사용
  - 비구조화 할당
    객체나 배열에서 속성 혹은 요소를 꺼내올 때 사용.
  - `Promise 등장`
    `new Promise`로 프로미스 생성. 안에 `resolve와 reject`를 매개변수로 갖는 콜백 함수를 넣는 방식. 선언한 promise 벼수에 then과 catch 메서드를 붙이는 것이 가능

- ES7(ES2016)
  - 제곱연산자 등장
  - Array.include 등장
- ES8(ES2017)
  - async await
  - Object.values()
  - Object.entries() <<Object.keys()+Object.valuse()>>
  - 문자열 앞부분에 공백을 넣어 자리수를 맞춰주는 String.padStart()
  - 문자열 뒷부분에 공백을 넣어 자리수를 맞춰주는 String.padEnd()
  - 매개변수 마지막에 콤마를 붙이는 것 허용

## ES3 vs ES5

ES3는 오래된 자바스크립트 표준이며, try/catch, switch, do-while 등 기본 문법 중심.
ES5(2009)는 strict mode, Object.defineProperty, Array.prototype.forEach, JSON 지원, getter/setter, bind() 등을 추가하여 객체지향과 함수형 프로그래밍을 더 풍부하게 지원.
현재 대부분 브라우저는 ES5를 완벽히 지원하고, ES6 이후 문법은 Babel같은 트랜스파일러를 사용해서 트랜스파일링하여 사용.
`ES5(2009)`

1. 배열에 forEach, map, filter, reduce, some, every와 같은 메소드 지원
2. Object에 대한 getter / setter 지원
3. 자바스크립트 strict 모드 지원 (더 깐깐한? 문법 검사를 한다.)

   1. 기존에는 조용히 무시되던 에러들을 throwing함
   2. JavaScript 엔진의 최적화 작업을 어렵게 만드는 실수들을 바로잡음.
   3. 엄격 모드는 ECMAScript의 차기 버전들에서 정의 될 문법을 금지.
   4. script 범위에서는 맨 위에 , 함수 레벨이라면 함수 선언 맨 위에 엄격모드 선언한 스크립트와 선언하지 않은 스크립트 사이 연결하는 부분은 문제를 일으킬 수 있음! → 상충되지 않은 스크립트들끼리 맹목적인 연결이 불가능
   5. js module에선 기본적으로 엄격모드

4. JSON 지원 ( 과거에는 XML을 사용하다가, json이 뜨면서 지원하게 됨 )

## 객체나 배열 구조 분해 할당(Destructuring)의 예시를 들어주세요.

```jsx
const user = { name: "SY", job: "baeksu" };
const { name, job } = user;

const arr = [1, 2, 3];
const [first, second] = arr;
//객체나 배열의 값을 변수로 손쉽게 추출할 수 있어 코드 가독성과 유지보수성이 향상
```

## 전개 연산자(spread)와 나머지 인자(rest)의 차이와 장점은?

- 스프레드: 배열, 객체를 펼쳐서 전달
  ```jsx
  const arr = [1, 2];
  const newArr = [...arr, 3]; // [1, 2, 3]
  ```
- rest: 여러 인자를 하나로 묶음
  ```jsx
  function sum(...args) {
    return args.reduce((a, b) => a + b);
  }
  ```
  문법은 같지만 사용 목적이 다름

## 옵셔널 체이닝, 널 병합 연산자 사용법 설명

- `?.`: 안전하게 속성 접근
- `??`: null 또는 undefined일 때 기본값 설정

## 템플릿 리터럴(Template Literal)로 문자열을 생성하는 예를 보여주세요.

```jsx
const name = "SY";
const greeting = `Hello, ${name}!`;
// 백틱(`)을 사용하여 변수 삽입, 줄바꿈, 다중 라인을 손쉽게 처리할 수 있음
```

## `'use strict'` (strict mode)는 무엇이며, 장단점은 무엇인가요?

`'use strict'`는 엄격 모드(strict mode)를 활성화하는 지시어
예를 들어 암묵적 전역변수 생성을 막고, this가 명확하지 않으면 undefined로 설정되는 등 버그 유발 가능성을 줄여줌

- 장점: 안정성, 예측 가능성 증가
- 단점: 예전 코드와 호환되지 않을 수 있음

## JavaScript로 컴파일되는 언어(TypeScript, Elm 등)를 사용하는 것의 장단점은?

장점:

- 정적 타입으로 인해 개발 단계에서 오류 발견 가능
- IDE 자동완성과 리팩토링이 용이
- 유지보수에 유리

단점:

- 러닝 커브 존재 (초기 진입 장벽)
- 빌드 과정 필요
- JS보다 긴 코드 작성
