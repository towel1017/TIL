# Typescript

---

## 타입 스크립트의 특징

- **크로스 플랫폼 지원** : 자바스크립트가 실행되는 모든 플랫폼에서 사용이 가능하다.
- **객체 지향 언어** : 클래스, 인터페이스, 모듈 등의 강력한 기능을 제공하며, 순수한 객체 지향 코드를 작성할 수 있습니다.
- **정적 타입** : 정적 타입을 사용하기 때문에 코드를 입력하는 동안에 오류를 체크할 수 있습니다.
- **DOM 제어** : 자바스크립트와 같이 DOM을 제어해 요소를 추가하거나 삭제할 수 있습니다.
- **최신 ECMAScript 기능 지원** : ES6 이상의 최신 자바스크립트 문법을 손쉽게 지원할 수 있습니다.

## 컴파일러 옵션

타입스크립트 컴파일을 위한 다양한 옵션을 지정할 수 있습니다. <br />
보통 `tsconfig.json` 파일로 옵션을 관리 합니다.

---

## 1. 타입 지정

타입 스크립트는 일반 변수, 매개변수(파라미터), 객체속성(프로퍼티) 등에 `: TYPE` 형식과 같은 형태로 타입을 지정할 수 있습니다.

```ts
const someFunc = (a : TYPE_A , b : TYPE_B) : TYPE_RETURN {
      return a + b;
}
let some : TYPE_SOME = someFunc(1, 2);
```

다음 예시를 보면
`add` 함수의 매개변수 `a`와 `b`는 `number` 타입이고, <br />
그렇게 실행된 함수의 반환 값은 추론(Inference)되기 때문에 `sum`도 `number`타입이어야 한다고 지정했습니다.

```ts
const add = (a: number, b: number) => {
  return a + b;
};
const sum: number = add(2, 3);
```

---

## 2. 타입 에러

만약 위의 `sum`을 `number`가 아닌 `string`타입 이어야 한다고 작성하게 되면, <br>
파일을 컴파일 하는 과정에서 에러가 나는 것이 아닌 코드를 작성하는 과정에서 에러가 발생합니다.

## 3. 타입 선언

### Boolean (불린)

---

단순한 참(`true`)/거짓(`false`) 값을 나타냅니다.

```ts
let isBoolean: boolean;
let is_Done: boolean = false;
```

### Number (숫자)

---

모든 부동 소수점 값을 사용할 수 있습니다.
ES6에 도입된 2진수 및 8진수 리터럴도 지원합니다.

```ts
let num: number;
let integer: number = 6;
let float: number = 3.14;
let hex: number = 0xf00d;
let binary: number = 0b1010; // 10
let octal: number = 0o744;
let infinity: number = Infinity;
let nan: number = NaN;
```

### String (문자열)

---

문자열을 나타냅니다.
작은 따옴표(`''`), 큰 따옴표(`""`) 뿐만 아니라 ES6의 템플릿 문자열도 제공합니다.

```ts
let str: string;
let red: string = "Red";
let green: string = "Green";
let myColor: string = `My color is ${red}.`;
let yourColor: string = "Your color is" + green;
```

### Array (배열)

---

순차적으로 값을 가지는 일반 배열을 나타냅니다 .
배열은 다음과 같이 두 가지 방법으로 타입을 선언할 수 있습니다.

```ts
//문자열만 가지는 배열
let fruits: string[] = ["apple", "banana", "mango"];
//or
let fruits: Array<string> = ["Apple", "Banana", "Mango"];

//숫자만 가지는 배열
let onToSeven: number[] = [1, 2, 3, 4, 5, 6, 7];
//or
let onToSeven: Array<number> = [1, 2, 3, 4, 5, 6, 7];
```

유니언 타입(다중 타입)의 '문자열과 숫자를 동시에 가지는 배열'도 선언할 수 있습니다.

```ts
let array: (string | number)[] = ["Apple", 3, 4, "Banana"];
//or
let array: Array<string | number> = ["Apple", 3, 5, "Banana"];
```

배열이 가지는 항목의 값을 단언할 수 없다면 `any`타입을 사용할 수 있습니다.

```ts
let someArr = any[] = ["apple", 3, {}, [], false];
```

인터페이스(interface)나 커스텀 타입 (Type)을 사용할 수도 있습니다.

```ts
interface IUser {
  name: string;
  age: number;
  isValid: boolean;
}
let userArr: IUser[] = [
  {
    name: "Neo",
    age: 85,
    isValid: true,
  },
  {
    name: "Lewis",
    age: 52,
    isValid: false,
  },
  {
    name: "Evan",
    age: 36,
    isValid: true,
  },
];
```

읽기 전용 배열을 생성할 수도 있습니다.'

```ts
let arrA: readonly number[] = [1, 2, 3, 4];
let arrB: ReadonlyArray<number> = [0, 3, 4, 5];
arrA[0] = 123; // Error - TS2542: Index signature in type 'readonly number[]' only permits reading.
arrA.push(123); // Error - TS2339: Property 'push' does not exist on type 'readonly number[]'.

arrB[0] = 123; // Error - TS2542: Index signature in type 'readonly number[]' only permits reading.
arrB.push(123); // Error - TS2339: Property 'push' does not exist on type 'readonly number[]'.
```

### Tuple (튜플)

---

Tuple 타입은 배열과 매우 유사합니다.<br>
차이점이라면 **정해진 타입과 고정된 길이 배열**을 표현합니다.

```ts
let tuple: [string, number];
tuple = ["a", 1];
tuple = ["a", 1, 2]; // Error - TS2322
tuple = [1, "a"]; // Error - TS2322
```

이 외에도 Enum (열거형) , Object (객체), Unknown(알 수 없음) 등이 존재합니다.

### **유니언(Union) 과 인터섹션(Intersection)**

---

Union은 2개 이상의 타입을 허용하는 경우에 유니언을 사용합니다.<br/>
`|`(vertical bar)를 통하여 타입을 구분하며, `()`는 선택 사항입니다.

```ts
let union: string | number;
union = "Hello world!";
union = 100;
union = false; // Error - TS2322: Type 'false' is not assignable to type 'string | number'.
```

`Intersection`는 `&`를 사용해 2개 이상의 타입을 조합하는 경우 사용합니다.<br>
인터섹션은 새로운 타입을 생성하지 않고, 기존의 타입을 조합할 수 있기 때문에 유용하지만, 자주 사용하는 방법은 아닙니다.

```ts
// 기존 타입들이 조합 가능하다면 인터섹션을 활용할 수 있습니다.
interface IUser {
  name: string;
  age: number;
}
interface IValidation {
  isValid: boolean;
}
const heropy: IUser = {
  name: "Heropy",
  age: 36,
  isValid: true, // Error -  TS2322: Type '{ name: string; age: number; isValid: boolean; }' is not assignable to type 'IUser'.
};
const neo: IUser & IValidation = {
  name: "Neo",
  age: 85,
  isValid: true,
};

// 혹은 기존 타입(IUser, IValidation)과 비슷하지만, 정확히 일치하는 타입이 없다면 새로운 타입을 생성해야 합니다.
interface IUserNew {
  name: string;
  age: number;
  isValid: boolean;
}
const evan: IUserNew = {
  name: "Evan",
  age: 36,
  isValid: false,
};
```

### **함수(Function)**

---

타입스크립트에서 함수를 작성할 땐, 화살표 함수로 작성하며, <br>
인수(`파라미터`)의 타입과 반환(`리턴 값`) 값의 타입을 입력해야 합니다.

```ts
let myFunc = (arg1: number, arg2: number): number => {
  return arg1 + arg2;
};

//인수도 없고 반환도 없는 경우
const voidFunc = (): void => {
  console.log("Hello World");
};
```

### **타입 추론**

---

명시적으로 타입 선언이 되어 있지 않은 경우 , 타입스크립트는 타입을 추론하여 제공합니다.<br>

```ts
let num1 = 12; // 추론을 통해 명시되어 있진 않지만 number 타입으로 인식
num1 = "Hello"; // TS2322
```

변수 `num1`을 초기화 하면서 숫자 `12`를 할당하면서 추론을 통해 `Number` 타입으로 추론되었고, <br>
`Hello`라는 `String` 값은 할당할 수 없기 때문에 에러가 발생합니다

---

타입스크립트가 추론을 하는 경우는 다음과 같습니다.
<br>

- 초기화된 변수
- 기본값이 설정된 매개 변수
- 반환 값이 있는 함수

```ts
//초기화된 변수 num
let num = 12; // number 타입으로 추론

//기본값이 설정된 매개 변수 `b`
const add = (a: number, b: number = 2): number => {
  //반환 값 (a  + b)가 있는 함수
  return a + b;
};
```

> 타입 추론이 엄격하지 않은 타입 선언을 의미 하는 것은 아닙니다.<br>
> 따라서 이를 활용해 모든 곳, 모든 변수, 함수 등에 타입을 명시할 필요는 없으며, <br>
> 많은 경우 더 좋은 코드 가독성을 제공할 수 있습니다.

---

### **타입 단언**

타입스크립트가 타입 추론을 이용해 판단할 수 있는 타입의 범주를 넘는 경우, 더 이상 추론 하지 않도록 할 수 있습니다.<br>
