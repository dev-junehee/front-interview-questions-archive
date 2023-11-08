## var

var 변수가 **함수 외부에서 선언될 때 var의 스코프(scope)는 전역**입니다.<br />
var로 선언된 모든 변수를 윈도우 전체에서 사용할 수 있는 것입니다.

```javascript
var a = 1;

function print() {
	console.log(a);
}

print();   // 1
```

이렇게 함수 바깥에서 선언된 변수 a를 print() 함수 내부에서도 접근할 수 있는데,<br />
가능한 이유는 **스코프 체이닝(scope chaning)** 때문입니다.<br />
스코프 체이닝이란 변수를 찾을 때 먼저 자신이 속한 스코프에서 찾고,<br />
없을 경우 상위 스코프로 올라가면서 찾는 현상을 말합니다.

<br />

var 변수가 **함수 내부에서 선언될 때에는 스코프가 함수 범위로 한정**됩니다.<br />
함수 내부에서만 해당 변수에 접근할 수 있고, 사용할 수 있습니다.
```jsx
var a = 'global';

function print() {
	var b = 'local';
	console.log(b);
}

print();   // local

console.log(a);   // global
console.log(b);   // ReferenceError: b is not defined
```

위 예제에서 변수 `b`는 `print` 함수 내부에서 선언되었기 때문에 `print` 함수 내부에서만 접근하고 사용할 수 있습니다.<br />
때문에 `print` 함수 바깥에서 작성된 `console.log(b)`는 값을 제대로 출력할 수 없고 에러가 발생합니다.

<br />

var로 선언한 변수는 **재선언과 재할당이 가능**합니다.<br />
같은 변수를 다시 선언하거나, 같은 변수에 다른 값을 할당해도 오류가 발생하지 않아 유연한 사용이 가능합니다.

```jsx
var a = 'hi';
var a = 'hello';

console.log(a);   // hello
```

```jsx
var a = 'hello';
a = 'world';

console.log(a);   // world
```

<br />

var를 사용하여 변수 선언을 할 경우 유연한 사용으로 편리할 수 있지만, 프로젝트 규모가 커지거나 코드량이 많아진다면 해당 변수가 어디에서 어떻게 사용되고 변하는지 파악하기 힘들어질 수 있으며 이로 인해 개발자가 예상하지 못한 사이드 이펙트가 발생할 수 있습니다. 이러한 이유로 ES2015(ES6) 이후 변수 선언의 단점을 보완하기 위해 let과 const가 새로운 변수 선언 방식으로 추가되었습니다.

<br />

## let

let은 블록 스코프(block scope)의 범위를 가진 지역 변수를 선언합니다.<br />
하나의 블록은 중괄호(`{ }`)로 감싸져 있으며, 중괄호 안에 있는 것은 모두 블록 범위입니다.<br />
let으로 선언된 변수는 해당 블록 내에서만 접근하고 사용할 수 있습니다.

```jsx
let num = 123;
let count = 7;

if (count > 3) {
	let fruits = 'banana';
	console.log(fruits);
}

console.log(fruits);   // ReferenceError: fruits is not defined
```

중괄호로 감싸진 if문 내에서 선언된 변수 `fruits`는 해당 블록 범위인 if문 안에서만 접근과 사용이 가능합니다.<br />
때문에 블록 범위 바깥에서 사용된 `console.log(fruits)` 에서는 에러가 발생합니다.

<br />

let으로 선언한 변수는 **재선언은 불가능하지만, 재할당이 가능**합니다.<br />
동일한 이름의 변수가 다른 스코프를 가진다면, 즉 다른 범위 내에서 정의된다면 재선언도 가능합니다.<br />
재선언이 가능한 이유는 두 변수의 스코프가 달라 다른 변수로 취급되기 때문입니다. 

```jsx
let a = 'hi';
let a = 'hello';   // SyntaxError: Identifier 'test' has already been declared
```

```jsx
let a = 'hi';

if (true) {
	let a = 'hello';
	console.log(a);   // hello
}

console.log(a);   // hi
```

```jsx
let a = 'hello';
a = 'world';

console.log(a);   // world
```

<br />

## cosnt

const는 블록 범위(block scope)의 범위를 가진 상수를 선언합니다.<br />
var와 let으로 변수를 선언할 때, 변수에 값을 초기화(할당)하지 않은 상태로 선언할 수 있지만<br />
const의 경우 변수의 선언과 함께 값을 무조건 초기화(할당)해야 합니다.

```jsx
var apple;
let apple;

const apple;   // SyntaxError: Missing initializer in const declaration
```

<br />

const로 선언한 상수는 **재선언과 재할당이 모두 불가능**합니다.

```jsx
const a = 'hi';
const a = 'hello';   // SyntaxError: Identifier 'ggg' has already been declared
```

```jsx
const a = 'hi';
a = 'hello';   // TypeError: Assignment to constant variable
```

<br />

그러나 const로 선언된 객체의 경우 내부 **속성값에 한하여 재할당**을 할 수 있습니다.

```jsx
const fruits = {
	apple: '사과',
	banana: '바나나',
	cherry: '체리',
}

fruits.apple = '애플';

console.log(fruits.apple);   // 애플
```

<br />

대신 객체 자체를 업데이트 할 수 없습니다.

```jsx
const fruits = {
	apple: '사과',
	banana: '바나나',
	cherry: '체리',
}

fruits = {
	melon: '멜론',
	fig: '무화과',
}

// TypeError: Assignment to constant variable.
```

<br />

## 정리

- `var`로 선언한 변수는 전역 스코프(global scope) 혹은 함수 스코프(functional scope)를 가집니다.
- `let`과 `const`로 선언한 변수/상수의 스코프는 블록 스코프(block scope)입니다.
- `var`로 선언한 변수는 재할당과 재선언이 가능한 반면에, `let`으로 선언한 변수는 재할당만 가능합니다.
- `const`로 선언한 상수는 재할당과 재선언이 모두 불가능합니다.
- 세 가지의 변수 선언 모두 최상위로 호이스팅 되며,
`var` 변수의 경우 `undefined`로 초기화되지만, `let`과 `const`는 초기화되지 않습니다.
- `var`와 `let`은 변수에 값을 초기화(할당)하지 않은 상태로 선언만 할 수 있지만,
`const`의 경우 선언과 동시에 값을 초기화(할당)해야 합니다.
