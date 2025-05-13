# 타입스크립트

## any, unknown, never의 차이는?

any

- 어떤 타입이든 허용됨. 타입 검사가 수행되지 않음.
- 타입 안정성이 전혀 없고, 가능한 한 사용을 피하는 것이 좋음.

unknown

- 어떤 값이든 할당 가능하지만, 사용 전에 타입 검사가 필요.
- 타입 안정성을 제공함.

```ts
let value: unknown = "hello";
if (typeof value === "string") {
  console.log(value.toUpperCase()); // 안전하게 사용 가능
}
```

never

- 절대 발생할 수 없는 타입 (예: 무한 루프, 오류만 던지는 함수 등)

## 타입 단언(as)과 타입 가드(type guard)의 차이는?

타입 단언 (Type Assertion, as)

- 컴파일러에게 "이 값은 특정 타입이다"라고 개발자가 직접 단언함.

- 런타임 검사가 없어 위험할 수 있음.
- 확실히 타입이 특정일 때 사용

타입 가드 (Type Guard)

- 조건문 등을 통해 타입을 좁혀가는 안전한 방식.
- 여러 타입 중 구분할 때 사용

```ts
function handle(value: string | number) {
  if (typeof value === "string") {
    console.log(value.toUpperCase()); // string으로 안전하게 좁혀짐
  }
}
```

## 유니온(Union)과 인터섹션(Intersection) 타입의 차이는?

유니온 타입 (|)

- 여러 타입 중 하나를 허용함.

```ts
let value: string | number;
value = "hello";
value = 42;
```

인터섹션 타입 (&)

- 여러 타입을 모두 만족하는 값을 의미함.

```ts
type A = { name: string };
type B = { age: number };
type C = A & B; // { name: string; age: number }

const person: C = { name: "John", age: 30 };
```

## 타입 추론(Type Inference)은 어떻게 동작하나요?

- 변수나 함수의 초기값을 보고 TypeScript가 자동으로 타입을 유추함.
- 함수의 반환값도 타입을 명시하지 않아도 추론됨.
- 추론이 되지 않을 경우 any로 처리될 수 있음 (주의)

## interface vs type의 차이는?

|      항목       |          interface           |               type                |
| :-------------: | :--------------------------: | :-------------------------------: |
|    선언 병합    |             가능             |              불가능               |
|    객체 타입    | 주로 객체 구조 선언에 특화됨 | 더 유연하게 다양한 타입 표현 가능 |
| 유니온/인터섹션 |             안됨             |        가능 (`type A = B)         |
|    확장 방식    |        extends 키워드        |           & 연산자 사용           |

## 옵셔널 체이닝(?.)과 Nullish 병합(??) 차이는?

옵셔널 체이닝 (?.)

- 값이 null 또는 undefined인 경우 평가 중단하고 undefined 반환.

Nullish 병합 (??)

- 왼쪽 피연산자가 null 또는 undefined인 경우에만 오른쪽 사용.

## 제네릭(Generic)의 활용 예시와 장점은?

- 타입을 파라미터처럼 외부에서 주입받을 수 있는 방식
- 재사용성과 타입 안전성을 동시에 확보 가능

장점

- 다양한 타입에 대해 재사용 가능한 코드 작성 가능
- 런타임 타입 체크 없이 컴파일 타임에 타입 안정성 확보

## keyof, in, typeof, as const는 언제 사용하나요?

keyof

- 객체의 키를 유니온 타입으로 반환

```ts
type User = { name: string; age: number };
type UserKeys = keyof User; // 'name' | 'age'
```

in

- 매핑된 타입 생성 시 반복자로 사용

```ts
type Keys = "a" | "b";
type Flags = { [K in Keys]: boolean }; // { a: boolean; b: boolean }
```

typeof

- 기존 변수나 객체의 타입을 가져올 때 사용

```ts
const user = { name: "Alice", age: 30 };
type UserType = typeof user; // { name: string; age: number }
```

as const

- 값을 리터럴 타입으로 고정 (readonly로 변환)

```ts
const roles = ["admin", "user"] as const;
// type Role = 'admin' | 'user'
```

## Partial, Required, Pick, Omit 유틸리티 타입의 용도는?

Partial<T>

- 모든 속성을 선택적(optional)으로 만듦

```ts
type User = { name: string; age: number };
type PartialUser = Partial<User>; // { name?: string; age?: number }
```

Required<T>

- 모든 속성을 필수(required)로 만듦

```ts
type RequiredUser = Required<PartialUser>;
```

Pick<T, K>

- 특정 속성만 선택

```ts
type NameOnly = Pick<User, "name">; // { name: string }
```

Omit<T, K>

- 특정 속성을 제거

```ts
type NoAge = Omit<User, "age">; // { name: string }
```

## extends 키워드는 어떤 용도로 쓰이나요?

타입 상속 또는 제네릭에서 제약 조건을 설정할 때 사용됨

## keyof T는 어떤 값을 가질까요?

객체 타입 T의 속성 이름(key)들을 문자열 유니온 타입으로 반환

- 속성명을 타입으로 제한하거나 Record 등에서 키 타입 지정할 때 많이 사용

## 제네릭을 사용한 컴포넌트나 훅의 예시?

```ts
function useState<T>(initial: T): [T, (v: T) => void] {
  let value = initial;
  const setValue = (v: T) => {
    value = v;
  };
  return [value, setValue];
}

const [count, setCount] = useState<number>(0);
```

- useState, useReducer, useQuery 등에서 제네릭을 자주 활용
- API 응답 타입 등에서도 제네릭은 매우 유용함

## 함수 오버로드(Overloading)는 어떻게 하나요?

여러 타입의 파라미터에 대해 하나의 함수 구현을 제공하는 것.
오버로드 시그니처는 실제 구현 시그니처보다 위에 있어야 하며, 실제 구현에서는 가장 넓은 범위로 처리함.

```ts
function add(x: number, y: number): number;
function add(x: string, y: string): string;
function add(x: any, y: any): any {
  return x + y;
}
```

## enum과 const enum 차이점은?

enum

- 기본적인 열거형 타입
- 런타임에도 객체로 존재함

const enum

- 컴파일 타임에 상수로 인라인 처리됨
- 런타임에 코드로 존재하지 않음 → 더 가볍고 빠름

## 타입이 복잡할 때 어떤 전략으로 관리하나요?

- 공통 타입은 type 또는 interface로 분리
- 레벨 별로 types/ 디렉토리 구조화
- 유틸리티 타입 (Pick, Omit, Partial 등) 적극 사용
- 제네릭을 활용해 중복 제거

## third-party 라이브러리에 타입이 없을 때 어떻게 대처하나요?

- DefinitelyTyped에서 @types/라이브러리명 패키지 검색
- 없을 경우 \*.d.ts 선언 파일 직접 작성
  ```ts
  // types/some-lib.d.ts
  declare module "some-lib" {
    export function doSomething(): void;
  }
  ```
- 임시로 any 처리 후, 타입을 점진적으로 작성

## 비동기 함수의 반환 타입은 어떻게 지정하나요?

- 반환 타입은 Promise<타입> 형태로 명시

## tsconfig.json에서 자주 설정하는 옵션은?

|       옵션       | 설명                              |
| :--------------: | :-------------------------------- |
|      strict      | 엄격한 타입 검사 활성화 (추천)    |
|      target      | 컴파일될 JS 버전 (ES2020 등)      |
|      module      | 모듈 시스템 (ESNext, CommonJS 등) |
| moduleResolution | 모듈 경로 해석 방식               |
|  baseUrl, paths  | 절대 경로 import 설정             |
|  noImplicitAny   | 암시적 any 금지                   |
| esModuleInterop  | CommonJS와의 호환 import 가능     |

## 타입 오류가 있을 때 주로 어떤 식으로 디버깅하나요?

- 에러 메시지 확인: 타입 간 충돌 원인을 분석

- 타입 추론 확인: typeof, ReturnType, keyof 등으로 확인

- 점진적 단순화: 문제 타입을 줄이거나 나누어 테스트

- VSCode 오류 메시지 + quick fix 제안 확인
