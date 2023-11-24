## useMemo & useCallback

useMemo와 useCallback 두 가지 훅 모두 **Memoization(메모이제이션)** 과 관련이 있습니다.<br />
메모이제이션이란 반복되는 계산을 수행할 때 이전의 값을 저장해서 동일한 입력이 들어왔을 때 저장한 값을 재활용하여 반복 수행을 줄이고, 프로그램 속도를 올리는 기술입니다.

<br />

## useMemo

```jsx
useMemo(() => {}, [dependency]);
```

useMemo는 의존성 배열에 변화가 생기면, 콜백 함수를 실행하고 해당 콜백 함수의 값을 반환합니다.

<br />

## useCallback

```jsx
useCallback(fn, [dependency]);
const memoizationFunc = useCallback(() => console.log(), [testArr]);
```

반면에 useCallback은 메모이제이션된 함수 자체를 반환합니다.<br />
그렇기 때문에 그 함수를 값으로 가지는 변수에 할당하는 것이 일반적인 사용 방법입니다.<br />

리액트에서 특정 state가 변경되어 리렌더링이 일어나기 때문에 useCallback을 사용하지 않은 함수도 다시 새롭게 만들어집니다.<br />
그래서 특정 함수를 자식 컴포넌트에 Props로 전달하거나, Props 등의 외부에서 가져온 값으로 API를 호출하는 경우 매번 새롭게 함수가 만들어지고, API 요청이 가지 않도록 사용할 수 있습니다.

하지만 useCallback만으로는 자식 컴포넌트의 리렌더링을 막을 수 없기 때문에,<br />
자식 컴포넌트에 `React.memo` (고차 컴포넌트, HOC)를 함께 사용해주는 것이 좋습니다.

<br />

## 정리

- useMemo, useCallback 모두 불필요한 리렌더링을 방지하기 위해 사용할 수 있습니다.
- useMemo는 함수의 연산량이 많거나 복잡하여 리렌더링 될 때 마다 매번 함수를 실행하지 않고 이전의 결과값을 재사용하기 위해 사용할 수 있습니다.
- useCallback은 리렌더링 될 때 마다 해당 함수가 재생성되는 것을 방지하기 위해 사용할 수 있습니다.
