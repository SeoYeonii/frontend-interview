# 함수와 this

## 함수의 정의 방식 (4가지)

1. 함수 선언문

`function a(){}`

자바스크립트 엔진은 암묵적으로 생성된 함수 이름과 동일한 이름의 식별자를 생성하고, 거기에 함수 객체를 할당해서 함수가 실행 될 수 있도록 함.

함수 선언문으로 정의한 함수와 함수 표현식으로 정의한 함수는 생성 시점이 다름

함수선언문으로 함수를 정의하면 런타임 이전에 코드 평가 과정에서 함수객체가 먼저 생성됨. 즉, 함수 호이스팅이 발생

2. 함수 표현식

`const 변수 이름 = function () {}`  
함수는 객체 타입의 값. 그러므로 객체 리터럴을 통해 객체를 생성하듯이 함수를 생성할 수도 있음.

할당문 + 함수 → function objcet의 name 프로퍼티로 할당문의 변수 이름을 사용.

함수 선언문으로 정의한 함수는 정의하기 전에 실행하면 실행이 되지만, 함수 표현식으로 정의한 함수는 실행이 안됨. 함수표현식으로 함수를 정의하면 변수 호이스팅이 발생. sub이라는 변수에 할당되는 값은 런타임에 결정되기 때문에, 변수 호이스팅에 의해 undefined(var)로 초기화.

함수 호이스팅은 함수를 사용하기 전에 반드시 함수를 선언해야한다는 규칙을 무시하므로 함수 표현식을 권장한다고 함.

3. new 키워드

`new Function ('params', 'body')`

4. Arrow Function
   - 화살표 함수는 `this` 컨텍스트가 필요 없는 콜백에서 많이 사용

## `function Person() {}`, `var person = Person()`, `var person = new Person()`의 차이는 무엇인가요?

- `function Person()`은 함수 선언문 -> 함수 호이스팅 발생
- `var person = Person()`은 함수 표현식으로 선언한 방식이며, `person()할 때`반환값이 없으면 `undefined`가 할당됨.
- `var person = new Person()`은 생성자 함수로 객체를 생성하고 `this`를 해당 인스턴스에 바인딩

## `function foo() {}`와 `var foo = function() {}`는 어떤 차이가 있나요?

- 첫 번째는 함수 선언식으로 함수 호이스팅 됨
- 두 번째는 표현식으로 변수 선언으로 호이스팅 됨

## this란 무엇인가?

함수가 호출될 때 결정되는 실행 컨텍스트의 소유 객체. 즉, 함수가 정의된 곳이 아니라 어떻게 호출되었는가에 따라 `this`의 값이 달라짐. 이로 인해 동일한 함수라도 호출 방식에 따라 `this`가 다르게 동작할 수 있음.

1. 함수를 호출할 때 new 키워드를 사용하는 경우, 함수 내부에 있는 this는 생성된 새로운 객체
2. 화살표 함수의 this는 상위스코프의 this
3. 일반 함수 this는 window를 가리킴.

## use strict모드에서의 this?

일반함수에서의 this는 undefined가 바인딩 됨.

## this안에는 뭐가 있는가?

함수를 어떻게 호출했는지에 따라 다른 바인딩된 값을 가지고 있음.
함수의 실행 컨텍스트에 따라 `this`가 가리키는 객체가 다르며,
객체 내부에서 호출하면 그 객체, 전역 함수에서 호출하면 전역 객체 (`window`, `global`)를 가리킴

## this랑 같은 위치에 있는 객체 여러가지가 있는데 그것이 무엇인가?

1. 렉시컬 환경 컴포넌트 (Lexical Environment)
   - 렉시컬 환경은 정적 환경이지만, 글로벌 환경과 동적 환경이 이안에서 처리되기 때문에, 세부 값의 변경이 일어날 수 있음
   - Scope의 설정 === Object의 환경이 설정되는 공간
   1. 환경 레코드
      1. 선언적 환경 레코드
         1. 기본 primitive type의 변수와 값을 만나면, k/v형태의 프로퍼티로 저장
      2. 오브젝트 환경 레코드
   2. 외부 렉시컬 환경 참조
      1. 함수 외부에 선언된 함수나 변수의 scope를 저장 → 이를통해 외부에 있는 함수나 변수를 하나의 실행 컨텍스트 안에 묶을 수 있음
2. 변수 환경 컴포넌트 (Variable Enviorment)
   - 변수 환경은 복원을 위해서 존재. 다시 돌아왔을떄. 변수환경의 값을 렉시컬 환경에 적용함으로써 초기값으로 돌아가기 위해서임
   1. 변수환경 컴포넌트와 렉시컬 환경 컴포넌트의 초기값은 같음
3. this 바인딩 컴포넌트 (This Binding)
   - This Binding Component는 함수안에서 this로 참조할 오브젝트를 담음
   1. this로 참조할 오브젝트를 바인딩하는 것
   2. Scope를 사용하는 것 외에, this를 통해 외부에 위치한 변수의 값을 가지고 올 수 있음
   3. function의 경우 default로 window 오브젝트를 참조하게 됨

## this는 언제 결정되는가?

어떻게 호출되었는지에 따라 동적으로 결정됨

1. 일반 함수 호출
   - 일반 함수로 호출된 모든 함수 (중첩, 콜백 포함)의 내부 this는 전역 객체에 바인딩된다.
2. 메소드 호출
   - 메서드 내부의 this에는 메서드를 호출한 객체가 바인딩됨
3. 생성자 함수 호출 (new 키워드)
   - 생성자 함수가 생성할 인스턴스가 바인딩됨
4. Function.prototype의 apply call bind 메서드에 의한 간접 호출
   - apply, call, bind로 바인드한 객체

## 참조하는 this를 바꿀 수 있는 방법

- `call`, `apply`, `bind`
- 화살표 함수 사용

1. Call, Apply
   - 본질적으로는 첫번째 인자로 this로 사용할 객체를 넘겨주며, 함수를 호출하는 것
   - call의 경우, 호출할 함수의 인수를 쉼표로 구분한 리스트 형식으로 전달
     - 파라미터의 수가 고정적일때 사용하면 됨
   - apply의 경우, 호출할 함수의 인수를 배열로 묶어 전달
     - 파라미터의 수가 유동적일때 사용하면 된다.
2. Bind
   - 함수를 호출하지 않고, this로 사용할 객체만 전달. 즉, 참조할 오브젝트와 파라미터를 묶음
   - bind의 리턴값은 함수를묶어서 새로운 function Object를 반환
   - primitive type도 바인딩 가능. number의 경우 Number 인스턴스를 생성한 후 바인딩

## Call, Apply, Bind 함수에 대해 설명해주세요.

3가지 방법은 this를 바인딩하기 위한 방법

- Call은 this를 바인딩하면서 함수를 호출하는 것, 두번째 인자를 apply와 다르게 하나씩 넘기는 것
- Apply는 this를 바인딩하면서 함수를 호출하는 것, 두번째인자가 배열
- Bind는 함수를 호출하는 것이 아닌 this가 바인딩 된 새로운 함수를 리턴함.

## `Function.call()`과 `Function.apply()`는 무엇을 하는 함수이며, 둘의 차이는 무엇인가요?

- `call(thisArg, ...args)`는 인자를 하나씩
- `apply(thisArg, [args])`는 인자를 배열로
  둘 다 this를 바인딩해서 함수 실행할 수 있도록 함.

## `Function.prototype.bind()`는 무엇인가요?

- 함수의 `this`를 고정한 새로운 함수를 반환
- 실제 호출은 나중에 하되, `this`는 이미 바인딩되어 있음.

## 화살표 함수 vs 일반 함수의 this

- 화살표 함수는 자신의 this를 가지지 않으며, 상위 스코프의 this를 참조
- 일반 함수는 실행 시점에 따라 `this`가 결정됨

## class에서의 this 특징

- 클래스 내부 메서드는 `this`가 인스턴스를 가리킴.
- 하지만 클래스 메서드를 이벤트 핸들러로 등록하면 `this`가 바뀌어버릴 수 있음

```
class MyComponent extends React.Component {
  handleClick() {
    console.log(this); // 기본적으로 undefined
  }

  render() {
    return (
      <button onClick={this.handleClick}>Click</button>
    );
  }
}
```

- this.handleClick 내의 this는 바인딩되지 않기 때문에 undefined.
  - 생성자에서 this.handleClick = this.handleClick.bind(this)
  - handleClick = () => {} 화살표 함수로 선언

## class와 function에서 this의 차이

this는 함수를 호출할때 결정이 됨. 그러므로 class와 function을 어떻게 불렀는가에 따라서 결정됨.

- 일반 함수를 호출하면 this가 전역 객체에 바인딩
- new를 통해 생성한 class는 인스턴스생성과 함께 그 인스턴스에 바인딩

## button에 eventlistener에서 callback에서 this는 뭘 가리키나요?

함수를 호출한 방법에 따라 달라지는데,

- addEventListener 안에 일반 함수로 선언하면: 버튼 (addEventLister내부에서 자동으로 바인딩해줌)
- 리엑트에서 onCLick 프로퍼티에 바로 일반함수로 선언하면: undefined (strict mode)
- 화살표 함수: 상위 스코프의 this - (대부분 undefined)

## 화살표 함수란?

ES6에 추가되었고, 간략하게 함수를 표현할뿐만 아니라, 일반 함수가 콜백 함수 내부에서 this를 전역객체로 가르키는 문제 때문에 생김
화살표 함수도 일급객체 이므로 Map과같은 고차함수에 파라미터로 전달할 수 있음.

## 화살표 함수(`=>`)를 사용하는 이유는 무엇이며, 기존 함수와 어떤 차이가 있나요?

화살표 함수는 문법이 간결하고, `this` 바인딩이 정적(lexical)으로 결정됨(일반 함수에서 this는 호출 시점에 따라 동적으로 결정). 콜백에서 `this`를 유지하고 싶을 때 유용.

1. arrow function은 인스턴스를 생성할 수 없음 → prototype 프로퍼티가 존재하지 않음
2. 중복된 매개변수 이름을 선언할 수 없음,(일반 함수는 중복된 매개변수 이름 사용할 수 있음(뒤에껄로 덮어씌어짐)
3. arrow function은 함수 자체의 this, arguments, super, 바인딩을 가지고 있지 않음 → 이것들을 참조하면 상위 스코프 체인의 것들을 참조
4. 제일 큰 차이점은 this
   - arrow function은 this바인딩을 갖지 않기 때문에 함수가 정의된 위치에서 결정됨
   - arrow function의 상위 function의 this를 스코프 체인을 통해 찾아냄

## Arrow function의 this 바인딩 특징을 설명해주세요.

화살표 함수는 자신만의 `this`를 가지지 않으며, 선언된 상위 스코프의 `this`를 그대로 사용

## 생성자 내부 메서드에 화살표 함수를 사용하는 이점은 무엇인가요?

이벤트 핸들러나 콜백에서 내부 메서드가 생성자 함수의 `this`를 잃지 않도록 하기 위해 사용.

## 일반 함수와 arrow 함수의 hoisting 차이는?

- 선언식 함수는 함수 호이스팅되어 어디서든 호출 가능
- 화살표 함수는 `const/let`에 할당되면 TDZ(Temporal Dead Zone)의 영향을 받음

## function을 arrow function으로 리팩토링할때 주의할 점

this를 조심하여 리팩토링 해야함. 화살표 함수는 `this`, `arguments`, `super`, `new.target`을 바인딩하지 않기 때문에, 생성자 함수나 클래스 메서드로는 사용 불가능

## 익명 함수(Anonymous function)의 대표적인 사용 예는 무엇인가요?

콜백, IIFE, 함수 표현식 등에서 사용됨

## 선언적 함수랑 익명 함수의 차이점이 뭔가? / 익명함수와 아닌 함수의 차이점?

선언적 함수는 이름이 있어 재귀 호출과 디버깅이 용이하며, 호이스팅됨. 익명 함수는 대개 표현식에 할당되어 사용됨. 변수에 할당한 익명함수는, 변수로 호이스팅되기 때문에 함수로 인식되지 않음

## 즉시실행함수 (IIFE)란? 왜 쓰는지 설명하시오

IIFE는 선언과 동시에 실행되는 함수로, 지역 스코프를 만들어 전역 변수 오염을 막고, 클로저를 형성해 상태를 보호할 수 있음.

- 저장할 필요가 없는 1회성 코드이므로, 반환하고 나면 메모리에서 사라짐. 실행 결과도 메모리에 저장되지 않음. 그래서 주로 초깃값을 설정할때 사용
- Global Scope를 오염시키지 않게 하기 위해서 사용.

## 입급객체란?

1. 변수나 데이터에 할당할 수 있어야됨
2. 함수의 매개변수에게 전달될 수 있음 === 객체의 인자로 넘길 수 있어야됨
3. 함수의 반환값으로 쓰일 수 있어야함 === 객체의 리턴값으로 리턴할 수 있어야됨

## 고차 함수(Higher-order function)란 무엇인가요?

함수를 인자로 받거나 반환하는 함수를 말하며, 대표적으로 `map`, `filter`, `reduce` 등이 있음.

## ES5의 고차함수 7개

`forEach`, `map`, `filter`, `reduce`, `some`, `every`, `sort`

## 자바스크립트 Argument 처리 구

JS 엔진은 0부터 파라미터 수만큼 key값을 부여해 k-v형태로 Arguement 오브젝트에를 저장함. (array-like하게 동작.) 단, 화살표 함수에는 `arguments`가 없음

## Function Object를 생성할 때, 일어나는 일은? (function a(){})

- 함수 객체가 생성되며
- `[[Environment]]`에 현재 렉시컬 환경이 저장되고
- `prototype` 속성과 `length`, `name` 등의 기본 속성이 설정됨.
  - 엔진이 function 키워드를 만났다고 실행되는건 아님. 한참뒤에나 실제 사용을 하게 되므로 저장하는것
- 이후 함수가 호출되면 실행 컨텍스트를 만들고 function Object가 생성될때 만들어진 [[Scope]]에 함수가 속한 영역을 저장 → 이것이 Lexical Scope

## new 키워드로 함수를 생성할 때, 일어나는 일 vs 그냥 함수를 만들면?

- `new`를 사용하면 빈 객체가 생성되고 `this`로 바인딩됨.
- 생성자 함수 내에서 `this`를 조작하며 인스턴스를 반환함.
- 일반 함수 호출은 `this`가 호출 컨텍스트에 따라 달라짐.

## ES5의 map, forEach의 인자에 대해서 설명하시요

- `map(callback, thisArg?)`은 새로운 배열을 반환
- `forEach(callback, thisArg?)`은 반환값이 없고 단순 반복용
- 둘 다 콜백의 인자로 `(element, index, array)`를 받음
