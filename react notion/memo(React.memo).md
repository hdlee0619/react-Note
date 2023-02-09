# memo?

[[최적화(Optimization)#^367a5a|리-렌더링의 발생 조건 중 3번째 경우]]
부모 컴포넌트가 리렌더링 되면 자식 컴포넌트는 모두 리렌더링 된다는 것을 그림으로 보면

![](https://i.imgur.com/s7IMbYD.png)

- 1번 컴포넌트가 리-렌더링 된 경우, 2~7번 컴포넌트가 모두 리-렌더링!
- 4번 컴포넌트가 리-렌더링이 된 경우, 6, 7번이 모두 리-렌더링!

자녀 컴포넌트 입장에서는 `나는 바뀐게 없는데 왜 리-렌더링이 돼야하지?`라는 의문이 생기게 되는데 이를 해결해주는 도구가 바로 **React.memo**!

# 사용 코드

## 문제 상황 코드

→ **자식 컴포넌트가 모두 바뀌는 경우**

#### App.jsx
```jsx
import React, { useState } from "react";
import Box1 from "./components/Box1";
import Box2 from "./components/Box2";
import Box3 from "./components/Box3";

const boxesStyle = {
  display: "flex",
  marginTop: "10px",
};

function App() {
  console.log("App 컴포넌트가 렌더링되었습니다!"); // 렌더링 시 출력

  const [count, setCount] = useState(0);

  // 1을 증가시키는 함수
  const onPlusButtonClickHandler = () => {
    setCount(count + 1);
  };

  // 1을 감소시키는 함수
  const onMinusButtonClickHandler = () => {
    setCount(count - 1);
  };

  return (
    <>
      <h3>카운트 예제입니다!</h3>
      <p>현재 카운트 : {count}</p>
      <button onClick={onPlusButtonClickHandler}>+</button>
      <button onClick={onMinusButtonClickHandler}>-</button>
      <div style={boxesStyle}>
        <Box1 />
        <Box2 />
        <Box3 />
      </div>
    </>
  );
}

export default App;
```

#### Box1.jsx, Box2.jsx, Box3.jsx 모두 동일한 구조

```jsx
import React from "react";

const boxStyle = {
  width: "100px",
  height: "100px",
  backgroundColor: "#91c49f",
  color: "white",

  // 가운데 정렬 
  display: "flex",
  justifyContent: "center",
  alignItems: "center",
};

function Box1() {
  console.log("Box1이 렌더링되었습니다."); // 렌더링 시 출력
  return <div style={boxStyle}>Box1</div>;
}

export default Box1;
```

#### `+`와 `-` 버튼을 누르는 순간의 콘솔 창

![](https://i.imgur.com/EbvwqbF.png)

## memo를 통해 해결

`React.memo`를 이용해서 컴포넌트를 **메모리에 저장(캐싱)** 해두고 필요할 때 가져다 쓸 수 있게 한다. 이렇게 하면 부모 컴포넌트의 `state`의 변경으로 인해 `props`가 변경이 일어나지 않는 한 컴포넌트는 **리렌더링 되지 않는다.** 
이를 _컴포넌트 memoization_ 이라고 한다. 

```jsx
export default React.memo(Box1); 
export default React.memo(Box2); 
export default React.memo(Box3);
```

![](https://i.imgur.com/OFfsSYk.png)
