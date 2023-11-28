## Component와 PureComponent

```jsx
import React, { Component } from 'react';

class MyComponent extends Component {
  render() 
			// ...
  }
}
```

```jsx
import React, { PureComponent } from 'react';

class MyComponent extends PureComponent {
  render() {
			// ...
  }
}
```

<br />

## shouldComponentUpdate()

```jsx
shouldComponentUpdate(nextProps, nextState)
```

`React.Component`와 `React.PureComponent`의 차이는 리액트의 생명주기 메서드 중 하나인 `shouldComponentUpdate()`를 어떻게 쓰는가 하는 부분입니다. `shouldComponentUpdate()`는 props 또는 state가 변경되어 리렌더링이 발생하기 직전에 호출되며 성능 최적화를 위해 사용할 수 있습니다.

- `React.Component`는 `shouldComponentUpdate`를 따로 설정하지 않은 경우 항상 `true`를 반환합니다. 즉 **props와 state의 실제 변경 여부에 상관없이 setState가 실행되면 무조건 컴포넌트를 리렌더링** 합니다.
- `React.PureComponent`는 `shouldComponentUpdate`가 이미 구현되어 있어 **props와 state에 대한 얕은 비교를 수행하여 변경이 확인되면 true를 반환하여 리렌더링 하고, 변경되지 않았을 경우 false를 반환**합니다.

<br />

## 정리

- `React.Component`와 `React.PureComponent`는 리액트의 클래스형 컴포넌트를 구현할 때 사용합니다.
- `shouldComponentUpdate()`는 리액트의 생명주기 메서드 중 하나입니다.
- `React.Component`는 `shouldComponentUpdate()`를 직접 작성해야 합니다. 직접 작성하지 않았을 경우 항상 true를 반환하여 props와 state의 실제 변경 여부와 상관없이 setState가 실행되면 무조건 컴포넌트를 리렌더링 합니다.
- `React.PureComponent`는 `shouldComponentUpdate()`가 내장되어 있어 props와 state에 대한 얕은 비교를 수행하여 true를 반환할 때 리렌더링 하며, false를 반환 시에는 리렌더링 하지 않습니다.
