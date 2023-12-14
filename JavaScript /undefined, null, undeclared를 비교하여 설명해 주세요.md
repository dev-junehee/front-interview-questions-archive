## undefined

변수를 선언했으나 아직 값이 할당되지 않은 상태입니다.

```tsx
let x;

console.log(x);          // undefined
console.log(typeof x);   // undefined
```

<br />

## null

변수에 의도적으로 ‘값이 없음’을 할당한 것을 나타냅니다.

```tsx
let x = null;

console.log(x);          // null
console.log(typeof x);   // object
```

<br />

## undeclared

접근 가능한 스코프에 변수가 선언조차 되지 않은 상태입니다.

```tsx
console.log(x);          // Reference Error
console.log(typeof x);   // undefined
```
