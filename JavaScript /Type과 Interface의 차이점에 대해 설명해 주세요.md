## 확장하는 법 (상속)

인터페이스는 `extends` 키워드를 이용해 확장하고, 타입은 `&` 연산자를 이용해 확장합니다.

```tsx
interface People {
	name: string;
	age: number;
}

interface Student extends People {
	school: string;
}
```

```tsx
type People = {
	name: string;
	age: number;
}

type Student = People & {
	school: string;
}
```

<br />

## 선언적 확장

인터페이스는 같은 이름의 인터페이스 재선언을 통해 선언적 확장이 가능하지만 타입은 불가능합니다.

```tsx
interface People {
	name: string;
	age: number;
}

interface People {
	nationality: string;
}

const kim: People = {
	name: '김씨',
	age: 100,
	nationality: 'Korea'
}
```

```tsx
interface People {
	name: string;
	age: number;
}

interface People {
	nationality: string;
}
```

<br />

## 자료형 (Data Type)

인터페이스는 객체의 타입을 지정할 때 사용하며 원시형 데이터에는 사용할 수 없습니다.

```tsx
interface People {
  name: string;
}

// 불가능
interface name extends string { }
```

타입은 객체와 원시형 데이터의 타입을 모두 정의할 수 있습니다. 하지만 객체의 타입을 지정할 때는 인터페이스를 사용하는 것이 좋으며 이외 원시형 데이터나 튜플, 유니온의 경우 타입을 사용하는 것이 좋습니다.

```tsx
type People = {
  name: string;
}

type School = string;
type age = number;

type People = [string, number];   // tuple
type People = string | number;    // union
```

<br />

## Computed Value

인터페이스는 computed value 사용이 불가능하지만 타입은 사용할 수 있습니다.

```tsx
type Subjects = 'Math' | 'Science' | 'Sociology';

interface Grades {
  [key in Subjects]: string;   // Errors
}
```

```tsx
type Subjects = 'Math' | 'Science' | 'Sociology';

type Grades = {
  [key in Subjects]: string;
}
```

<br />

## 정리

- 인터페이스는 extends를 통해, 타입은 & 연산자를 통해 확장(상속)합니다.
- 인터페이스는 선언적 확장이 가능하고, 타입은 선언적 확장이 불가능합니다.
- 인터페이스는 객체의 타입을 지정할 때만 사용할 수 있으며, 원시형 데이터에서는 사용할 수 없습니다.
- 타입은 모든 타입을 선언할 때 사용할 수 있습니다.
- 인터페이스는 computed value 사용이 불가능하며, 타입은 사용할 수 있습니다.
- 위와 같은 이유로 객체를 지정할 때는 인터페이스, 원시형 데이터나 튜플, 유니온의 경우 타입을 사용하는 것이 좋습니다.
