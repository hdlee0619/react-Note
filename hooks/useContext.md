# useContext?

## context..?

우선 context는 전역적으로 사용되는 어떠한 것을 표현할 때 보통 context라는 말을 사용한다. 

### (1) react context의 필요성
우리는 일반적으로 부모컴포넌트 → 자식 컴포넌트로 데이터를 전달해 줄 때 [[Props|props]]를 사용했었다. 

 그러나 `부모 → 자식 → 그 자식 → 그자식의 자식` 이렇게 너무 깊어지게 되면  prop drilling 현상이 일어나게 된다. 

**prop drilling의 문제점은**

1.  깊이가 너무 깊어지면 이 prop이 어떤 컴포넌트로부터 왔는지 파악이 어려움
2.  어떤 컴포넌트에서 오류가 발생할 경우 추적이 힘들어지니 대처가 늦게 된다.

![](https://i.imgur.com/cHePwpE.png)
→ [[Props#prop drilling|prop drilling 내용]] 

그래서 등장한 것이 react context API라는 것이고, useContext hook을 통해 쉽게 `전역 데이터를 관리`할 수 있게 된다. 

### (2) context API 필수 개념

- `createContext` : context 생성
- `Consumer` : context 변화 감지
- `Provider` : context 전달 (to 하위 컴포넌트)

## useContext 사용 코드

```jsx
import { createContext } from "react";

export const FamilyContext = createContext(null);
```

```ad-note
title: null의 의미?

createContext의 파라미터에는 context의 기본 값을 설정 할 수 있다. 여기서 사용한 null은 context를 쓸 때 값을 따로 지정하지 않을 경우 사용되는 기본 값이다. 
```

```jsx
import React from "react";
import Father from "./Father";
import { FamilyContext } from "../context/FamilyContext";

function GrandFather() {
  const houseName = "스파르타";
  const pocketMoney = 10000;

  return (
    <FamilyContext.Provider value={{ houseName, pocketMoney }}> {/* 감싸고 props를 넣어줌 */}
      <Father />
    </FamilyContext.Provider>
  );
}

export default GrandFather;
```

> `props`를 넘겨주지 않고 컴포넌트화로 만들어서 감싼다. 

```jsx
import React, { useContext } from "react";
import { FamilyContext } from "../context/FamilyContext";

function Child({ houseName, pocketMoney }) {
  const stressedWord = {
    color: "red",
    fontWeight: "900",
  };

  const data = useContext(FamilyContext);
  console.log("data", data);

  return (
    <div>
      나는 이 집안의 막내에요.
      <br />
      할아버지가 우리 집 이름은 <span style={stressedWord}>{data.houseName}</span>
      라고 하셨어요.
      <br />
      게다가 용돈도 <span style={stressedWord}>{data.pocketMoney}</span>원만큼이나
      주셨답니다.
    </div>
  );
}

export default Child;
```

## 주의사항
- `useContext`를 사용할 때, Provider에서 제공한 value가 달라지게 되면 useContext를 사용하기 있는 모든 컴포넌트가 리렌더링이 되게 된다. 
- 따라서 value 부분을 항상 신경을 써주어야한다. 

#### 해결 방안 
- 메모이제이션을 사용해야 한다. 

- - - 
#### 태그
#hook #useContext
