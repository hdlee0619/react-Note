
# 정의
 - useState는 가장 기본적인 hook이며, 함수 컴포넌트에서 가변적인 상태를 가지게 해줍니다
 - React에서 정의하는 `state`를 Fuction Component에서 사용하게 해주는 #hook 입니다
 - 클래스형 컴포넌트에서 `this.state`와 `this.setState`를 대체 합니다

# 사용법

```jsx
const [value, setValue] = useState(0);
```

- `value, setValue` : 
`value`
관리할 value(변수 선언)
`setValue`
value를 관리, value를 재선언할 수 있다
- 주의
`value`가 원시 데이터타입이 아닌 객체 데이터 타입 (주소를 참조하는)인 경우에는 **불변성을 유지**  해주어야 한다.

## 업데이트

### 기존의 업데이트 방식
```jsx
// src/App.js

import { useState } from "react";

const App = () => {
  const [number, setNumber] = useState(0);
  return (
    <div>
			{/* 버튼을 누르면 1씩 플러스된다. */}
      <div>{number}</div> 
      <button
        onClick={() => {
          setNumber(number + 1); // 첫번째 줄 
          setNumber(number + 1); // 두번쨰 줄
          setNumber(number + 1); // 세번째 줄
        }}
      >
        버튼
      </button>
    </div>
  );
}

export default App;
```

> 이때 기대되는 값은 `setNumber`가 3번이 실행이 되었으므로 `number`가 **3** 이 될 것이라고 예상할 수 있지만, 값은 **1**이 나온다. 

### 함수형 업데이트 방식
```jsx
// src/App.js

import { useState } from "react";

const App = () => {
  const [number, setNumber] = useState(0);
  return (
    <div>
			{/* 버튼을 누르면 3씩 플러스 된다. */}
      <div>{number}</div>
      <button
        onClick={() => {
          setNumber((previousState) => previousState + 1);
          setNumber((previousState) => previousState + 1);
          setNumber((previousState) => previousState + 1);
        }}
      >
        버튼
      </button>
    </div>
  );
}

export default App;
```

#### 왜 다르게 동작할까요?

 **일반 업데이트 방식**은 버튼을 클릭했을 때 첫번째 줄 ~ 세번째 줄의 있는 setNumber가 각각 실행되는 것이 아니라, [[DOM? virtual DOM ?#Batch Update|배치(batch)]]로 처리합니다. **즉 우리가 onClick을 했을 때 setNumber 라는 명령을 세번 내리지만, 리액트는 그 명령을 하나로 모아 최종적으로 한번만 실행**을 시킵니다. 그래서 setNumber을 3번 명령하던, 100번 명령하던 1번만 실행됩니다.

반면에 **함수형 업데이트 방식**은 **3번을 동시에 명령을 내리면, 그 명령을 모아 순차적으로 각각 1번씩 실행**시킵니다. 0에 1더하고, 그 다음 1에 1을 더하고, 2에 1을 더해서 3이라는 결과가 우리 눈에 보이는 것이죠.

#### 그렇다면 왜 리액트는 위 방식으로 동작할까?

공식문서에서
리액트는 성능을 위해 단일 업데이트(batch update)로 한꺼번에 처리함
즉, 불필요한 리-렌더링을 방지(렌더링 최적화)를 위해서 한꺼번에 state를 모아놓고 같은 state를 같은 방식으로 처리한다면 딱 한번만 실행하게 된다.
하지만 함수형 업데이트를 사용하면 **``setState()``에서 인자를 받을 때 이전 값(`previousState`)을 받고 그 값에 대한 것을 실행** 하기 때문이다. 

# 정리
1. useState의 업데이트 방식은 2가지이며 각각 다르게 동작한다.
2. useState로 원시 데이터가 아닌 참조형 데이터를 변경할 때는 불변성을 신경써야한다. 

