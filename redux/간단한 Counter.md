# 리덕스를 이용한 간단한 Counter

#### App.jsx

```jsx
import './App.css';
import { useDispatch, useSelector } from 'react-redux';

function App() {
  // 여기서 store에 접근, counter의 값을 읽어와야 함
  // useSelector를 이용
  const counter = useSelector((state) => {
    return state.counter;
  });
  // dispatch 가져오기
  const dispatch = useDispatch();
  // dispatch에 action type을 보내줌
  const plusOne = () => {
    dispatch({
      type: 'PLUS_ONE',
    });
  };
  const minusOne = () => {
    dispatch({
      type: 'MINUS_ONE',
    });
  };

  return (
    <div className="App">
      <div>현재 카운트 : {counter.number}</div>
      <button onClick={plusOne}>+</button>
      <button onClick={minusOne}>-</button>
    </div>
  );
}

export default App;
```

#### modules > counter.js

> modules에서 *초기의 state를 설정*하고 dispatch를 통해 `action type`과 현재 `View에서 보여지고 있는 state`를 받아와서 `type`에 따라 `state`를 변경하는 로직을 처리 후 다시 `store`로 보내주고 `store`는 다시 `View쪽으로 보내 업데이트` 해준다.

```javascript
// 초기 상태값(state)
const initialState = {
  number: 0,
};

// 리듀서 : 'state'의 변화를 일으키는 함수
// (1) state를 action이 type에 따라 변경하는 함수
// (2)
// input : state, action
// action은 state를 어떻게 처리할 것인지
const counter = (state = initialState, action) => {
  console.log(state.number);
  switch (action.type) {
    case 'PLUS_ONE':
      return { number: state.number + 1 };
    case 'MINUS_ONE':
      return { number: state.number - 1 };
    default: // 아무것도 넣지 않을 때
      return state;
  }
};

export default counter;
```

#### config > configStore.js

```javascript
import { createStore } from 'redux';
import { combineReducers } from 'redux';
import counter from '../modules/counter';
/*
1. createStore()
리덕스의 가장 핵심이 되는 스토어를 만드는 메소드(함수) 
리덕스는 단일 스토어로 모든 상태 트리를 관리
리덕스를 사용할 시 creatorStore를 호출할 일은 한 번밖에 없다.
*/

/*
2. combineReducers()
리덕스는 action —> dispatch —> reducer 순으로 동작
이때 애플리케이션이 복잡해지게 되면 reducer 부분을 여러 개로 나눠야 하는 경우가 발생하게 되는데,
combineReducers은 여러 개의 독립적인 reducer의 반환 값을 하나의 상태 객체로 만들어준다.
*/

const rootReducer = combineReducers({
  // 기본 리듀서
  counter,
});
const store = createStore(rootReducer);

export default store;
```

[[Redux 흐름#간단 정리|action → dispatch → reducer 흐름 설명]]

## 리팩토링

### action value
`action type`들을 하드코딩으로 하면 나중에 변수 변경이 까다롭다. 
따라서, `action type`를 변수화 하는 것이 좋다. 

#### modules > counter.js
```js
export const PLUS_ONE = 'PLUS_ONE';
export const MINUS_ONE = 'MINUS_ONE';

...

const counter = (state = initialState, action) => {
  console.log(state.number);
  switch (action.type) {
    case PLUS_ONE:
      return { number: state.number + 1 };
    case MINUS_ONE:
      return { number: state.number - 1 };
    default: // 아무것도 넣지 않을 때
      return state;
  }
};

export default counter;
```

#### App.jsx

```jsx
import { PLUS_ONE, MINUS_ONE } from './redux/modules/counter';

...

const plusOne = () => {
    dispatch({
      type: PLUS_ONE,
    });
  };

  const minusOne = () => {
    dispatch({
      type: MINUS_ONE,
    });
  };

...
```

### action creator

action 객체를 만들어주는 역할을 하는 함수도 따로 만들어서 보관하는 것이 좋음
→ 리액트 공식문서에서도 권장

#### modules > counter.js

```jsx
...

// action creator : action value를 return 하는 함수

export const plusOne = () => {
  return {
    type: PLUS_ONE,
  };
};
export const minusOne = () => {
  return {
    type: MINUS_ONE,
  };
};

...
```

#### App.jsx

```jsx
import { plusOne, minusOne } from './redux/modules/counter';

...

const plusOneNum = () => {
    dispatch(plusOne());
  };
  const minusOneNum = () => {
    dispatch(minusOne());
  };

...
```

> 코드가 훨씬 깔끔해지고 유지보수가 용이해짐

## payload

> payload를 통해서 action 객체에 값을 담아, 즉 App.jsx에서 사용한 값을 store로 보낼 수 있다. 

#### modules > counter.js

```jsx
export const plusN = (payload) => {
  return {
    type: PLUS_N,
    payload: Number(payload), // 문자열로 넘어오길래 Number로 바꿔줌
  };
};
export const minusN = (payload) => {
  return {
    type: MINUS_N,
    payload: Number(payload), // 문자열로 넘어오길래 Number로 바꿔줌
  };
};

... 

const counter = (state = initialState, action) => {
  console.log(state.number);
  switch (action.type) {
    case PLUS_N:
      console.log(action);
      return {
        number: state.number + action.payload,
      };
    case MINUS_N:
      return {
        number: state.number - action.payload,
      };
    default: // 아무것도 넣지 않을 때
      return state;
  }

...
```

#### App.jsx

```jsx
...

const plusNum = () => {
    dispatch(plusN(number)); // state 값을 넣어서 store에 보내줌
  };

  const minusOneNum = () => {
    dispatch(minusN(number)); // state 값을 넣어서 store에 보내줌
  };

...
```