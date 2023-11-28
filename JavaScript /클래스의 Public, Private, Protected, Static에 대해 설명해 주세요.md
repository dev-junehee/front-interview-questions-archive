## class field
클래스 필드는 **클래스가 생성할 인스턴스의 프로퍼티를 의미**합니다.

```jsx
class Person {
	name = 'Olive';

	method() {
		return this.name;
	}
}

```

원래 클래스 바디에서는 메소드만 정의 가능하고 프로퍼티를 정의할 경우 `Syntax Errorr`가 발생했으나, 다른 객체 지향 언어와 같이 자바스크립트에서도 클래스 필드를 정의할 수 있도록 ECMAScript에 클래스 필드 문법이 제안되어 있으며 Chrome과 Node.js에서 선제적으로 구현해두어 현재는 에러가 발생하지 않고 클래스 필드를 클래스 바디에 정의할 수 있습니다.

```jsx
class Person {
	this.name = 'Olive';   // SyntaxError: Unexpected token '.'
}
```

유의할 점은 `this`는 클래스의 constructor와 메서드 내에서만 유효하기 때문에 클래스 필드를 정의할 때는 사용할 수 없습니다.

```jsx
class Person {
	name = 'Olive';

	constructor() {
		console.log(this.name);
	}

	introduce() {
		return `제 이름은 ${this.name}입니다.`
	}
}
```

그리고 클래스 필드를 참조할 때에는 반드시 `this`를 사용해야 합니다.

<br />

## Public

어디서든 접근할 수 있는 필드값을 의미합니다.<br />
클래스의 프로퍼티와 메서드는 기본적으로 public하기 때문에 인스턴스를 통해 클래스 외부에서 언제든 참조할 수 있습니다.

```jsx
class Person {
	constructor(name) {
		this.name = name;    // public!
	}
	
	age = 100;             // public!
}

const olive = new Person('Olive');

console.log(olive.name);   // Olive
console.log(olive.age);    // 100
```

<br />

## Private (#)
프라이빗 프로퍼티와 메서드는 클래스의 내부에서만 접근할 수 있으며 클래스 외부나 자식 클래스에서 접근할 수 없습니다.<br />
때문에 내부 인터페이스를 구성할 때 사용하며 프리픽스로 `#`를 붙여 작성합니다. public 필드와 상충하지 않기 때문에 함께 사용할 수 있습니다.

```jsx
class Person {
	#name = '비밀 이름';
	name = '이름';

	constructor(name) {
		this.#name = name;
	}
}
```

<br />

## Protected (_)
클래스 자신과 자식 클래스에서만 접근 할 수 있습니다. 내부 인터페이스를 구성할 때 사용하며, 프리픽스로 `_`를 붙여 작성합니다.<br />
`_`는 자바스크립트의 정식 문법이 아닌 개발자 사이의 암묵적 약속입니다.

```jsx
class Person {
	constructor(name, age) {
		this._name = name;
		this._age = age;
	}

	getName() {
		return this._name;
	}

	_setName(name) {
		this._name = name;
	}
}
```

클래스 외부에서 protected에 접근할 때에는 getter, setter 함수를 통해 접근할 수 있으며 setter 함수 없이 getter만 정의할 경우 해당 프로퍼티를 읽기 전용으로 만들 수 있습니다.

<br />

## Static
프로토타입이 아닌 클래스 자체에 메서드와 프로퍼티를 정의할 수 있는데, 이것을 **정적 메서드**와 **정적 프로퍼티**라고 하며 `static` 키워드를 사용해 생성합니다.

```jsx
class Person {
	static name = 'Kim';

	static #age = 100;

	static introduce() {
		return `My name is ${this.name}, and I'm ${this.#age} years old.`
	}
}

console.log(Person.introduce());
// My name is Kim, and I'm 100 years old.
```

<br />

## 정리

- 클래스 필드는 클래스가 생성할 인스턴스의 프로퍼티를 의미합니다.
- public은 클래스 내부 혹은 외부 어디서든 접근할 수 있으며, 모든 필드값은 기본으로 public합니다.
- private은 클래스 내부에서만 접근할 수 있으며 프리픽스로 `#`을 붙여 작성합니다.
- protected는 클래스 자신과 자식 클래스에서만 접근할 수 있으며 프리픽스로 `_`를 붙여 사용합니다. protected는 자바스크립트 정식 문법이 아닌 개발자 사이의 암묵적 약속입니다.
- static은 프로토타입이 아닌 클래스 자체에 정적 데이터를 정의할 수 있으며 static 키워드를 사용합니다.
- static을 통해 정의할 수 있었던 것은 정적 메서드 뿐이었으나 현재 static public, static private 필드, static private 메서드를 정의할 수 있는 표준 사양이 제안되어 있으며 크롬과 Node.js에서 이미 사용할 수 있습니다.
