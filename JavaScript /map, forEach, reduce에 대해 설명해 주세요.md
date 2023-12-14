## map()

배열 내 모든 요소를 순회하면서 함수를 호출한 결과를 모아 새로운 배열로 반환합니다.

```tsx
const arr = [1, 2, 3];

const newArr = arr.map((element) => element + 10);

console.log(newArr);

// result
// [11, 12, 13]
```

<br />

## forEach()

배열 내 모든 요소를 순회하면서 제공된 함수를 한 번씩 실행합니다.

```tsx
const arr = [1, 2, 3];

arr.forEach((element) => {
	console.log(element + 10);
})

// result
// 11
// 12
// 13
```

<br />

## reduce()

배열 내 모든 요소를 순회하면서 주어진 리듀서 함수를 실행하여 하나의 결과값을 반환합니다.

```tsx
arr.reduce(콜백[, 초기값]);
```

```tsx
const arr = [1, 2, 3];

const sumArr = arr.reduce((acc, cur) => acc + cur, 10);

console.log(sumArr);

// result
// 16
```
