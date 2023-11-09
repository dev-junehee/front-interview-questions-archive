## TDZ (Temporal Dead Zone)

TDZ란 **일시적 사각지대** 라는 의미로, 스코프의 시작 지점부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간을 뜻합니다.

자바스크립트 엔진에서 변수를 선언할 때 런타임(runtime) 환경이 아닌 그 이전 단계에서 먼저 실행되어 **선언 단계**와 **초기화 단계**를 거치는데,<br />
**선언이 실행되고 초기화가 되지 않은 상태의 단계**를 TDZ라고 부릅니다.

- **선언** : 변수명을 등록하여 자바스크립트 엔진에 변수의 존재를 알림
- **초기화** : 값을 저장하기 위해 메모리 공간을 확보하고 암묵적으로 undefined를 할당하여 초기화 함
- **할당** : 변수에 실제 값이 할당 됨 (undefined → 실제 값)

|  | 선언 단계 |
| --- | :---: |
|  | **일시적 사각지대 (TDZ)** |
| let foo; | **초기화 단계** |
| foo = 1; | **할당 단계** |

<br />

## let

```jsx
console.log(hello);   // ReferenceError: b is not defined
let hello;
hello = 'say hello!';
```

```jsx
let hello;
console.log(hello);   // undefined
```

```jsx
let hello;
hello = 'say hello!';

console.log(hello);   // say hello!
```

`let`은 선언 전에 변수에 접근할 경우 TDZ의 영향을 받게되어 참조 에러가 발생합니다.

<br />

## const

```jsx
console.log(pi);   // SyntaxError: Missing initializer in const declaration
const pi;
```

```jsx
console.log(pi);   // ReferenceError: pi is not defined
const pi = 3.14;
```

```jsx
const pi = 3.14;
console.log(pi);   // 3.14
```

`const`는 단독 선언이 불가능하기 때문에 선언 전에 변수에 접근할 경우 구문 에러와 참조 에러가 발생합니다.<br />
때문에 `const`를 사용할 때에는 초기화/할당 단계까지 모두 거쳐 변수를 사용해야 합니다.

<br />

## class

```jsx
const sony = new Player('손흥민');   // ReferenceError: Player is not defined

class Player {
	constructor(name) {
		this.name = name;
	}
}
```

```jsx
class Player {
	constructor(name) {
		this.name = name;
	}
}

const sony = new Player('손흥민');

console.log(sony.name);   // 손흥민
```

`class`는 선언 이전에 인스턴스를 생성할 수 없기 때문에 참조 에러를 발생킵니다.

<br />

## constructor() 내부의 super()

```jsx
class Parent {
	constructor() {
		this.lastName = 'kim';
	}
}

class Child extends Parent {
	constructor(lastName, age) {
		this.age = age;
		super(lastName);
	}
}

const daughter = new Child('kim', 7);

// ReferenceError: Must call super constructor in derived class before
// accessing 'this' or returning from derived constructor
```

```jsx
class Parent {
	constructor() {
		this.lastName = 'kim';
	}
}

class Child extends Parent {
	constructor(lastName, age) {
		super(lastName);
		this.age = age;
	}
}

const daughter = new Child('kim', 7);

console.log(daughter.lastName);   // kim
console.log(daughter.age);        // 7
```

상속 `class`의 생성자에서는 `this`를 사용하기 전 반드시 `super()`를 호출 후 사용해야 합니다.<br />
`super()`를 호출하지 않은 상태에서 `this`는 `TDZ` 상태에 속합니다.

<br />

## 함수 매개변수의 기본값 (Default Function Parameter)

```jsx
const a = 2;

function plus(a = a) {
	return a + a;
}

plus();   // ReferenceError: Cannot access 'a' before initialization
```

```jsx
const init = 2;

function plus(a = init) {
	return a + a;
}

plus();   // 4
```

매개변수의 기본값은 선언 및 초기화 단계를 거친 후 사용되어야 하기 때문에 그 이전에 사용할 경우 참조 에러가 발생합니다.<br />
매개변수에 기본값을 할당할 때는 매개변수와 다른 변수를 별도로 선언하여 사용해야 합니다.

<br />

## var, function, import

```jsx
console.log(food);   // undefined
var food;
```

```jsx
square(7);   // 49

function square(a) {
	return a * a;
}
```

```jsx
getName();
import { getName } from './getName.js';
```

`var`와 `function`은 각자의 스코프 내에서 호이스팅 되기 때문에 변수와 함수 선언 전에 사용되어도 에러가 발생하지 않고 정상적으로 작동됩니다.
또한 `import` 구문도 호이스팅 되기 때문에 자바스크립트 파일 시작 부분에 디펜던시 모듈(의존성 모듈)을 가져오는 것이 좋습니다.

<br />

## 정리

- TDZ는 일시적 사각지대라는 뜻으로, 선언이 실행되고 초기화가 되지 않은 상태의 단계입니다.
- TDZ는 변수나 클래스 구문의 유효성에 영향을 끼치기 때문에 선언 전에 사용하는 것을 금지합니다.
- 특히 let, const, class TDZ 단계에서 접근할 경우 참조 에러를 발생 시킵니다.
- var, function, import의 경우 스코프 내에서 호이스팅 되기 때문에 선언 전에도 사용이 가능합니다. (var는 변수 선언의 여러가지 특성상 사용을 지양하는 것이 좋습니다.)
