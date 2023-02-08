# 정의

- `useEffect()`는 리액트 컴포넌트가 렌더링이 될 때 마다 특정 작업을 수행하도록 설정할 수 있는 #hook
- 쉽게 말해 ==어떤 컴포넌트가 화면에서 사라졌을 때 무언가를 실행하고 싶다면?== `useEffect()`를 사용

# 사용법
```jsx
// src/App.js

import React, { useEffect } from "react";

const App = () => {

  useEffect(() => {
		// 이 부분이 실행된다.
    console.log("hello useEffect");
  });

  return <div>Home</div>;
}

export default App;
```

> 브라우저에서 우리가 App 컴포넌트를 눈으로 보는 순간, 즉 App 컴포넌트가 최초에 화면에 렌더링이 될 때 `useEffect`안에 있는 `console.log()`가 실행된다. 
> ==컴포넌트가 렌더링 될 때 실행된다.== 가 바로 핵심 기능이다. 

## useEffect와 리렌더링(re-rendering)

앞서 말했듯 `useEffect`는 화면이 렌더링 될 때마다 실행된다. 따라서 `useEffect()`의 의존성 배열을 활용해서 우리가 원할 때만 코드가 실행될 수 있도록 설정할 수 있다. 

### 의존성 배열

- 의존성 배열(dependency array)이란 쉽게 말해 **"이 배열에 값(`state`)을 넣었을 때만 `useEffect`내의 코드를 실행해줘"** 라는 뜻


```jsx
// src/App.js

const [value, setValue] = useState("");
  useEffect(() => {
    console.log("hello useEffect");
  }, []); // 비어있는 의존성 배열
/* **************************************** */
const [value, setValue] = useState("");
  useEffect(() => {
    console.log("hello useEffect");
  }, [value]); // value가 들어있는 의존성 배열
}
```

> 비어있는 의존성 배열일 때는 **최초 렌더링이 될 때 단 한번만 실행**하게 됩니다. 

> 의존성 배열에 값이 있을 때는 배열 안에 있는 값이 바뀔 때만, 위의 코드에서는 **`value`가 변경이 돼서 렌더링이 될 때에만 실행** 하게 됩니다. 

### 클린업 (clean up)

#### 클린 업이란?
"컴포넌트가 화면에서 사라졌을 때 무엇을 실행"하고 싶다면 **clean up**을 사용하면 된다. 

#### 클린 업 방법

```jsx
// src/App.js

import React, { useEffect } from "react";

const App = () => {

	useEffect(()=>{
		// 화면에 컴포넌트가 나타났을(mount) 때 실행하고자 하는 함수

		return ()=>{
			// 화면에서 컴포넌트가 사라졌을(unmount) 때 실행하고자 하는 함수
		}
	}, [])

	return <div>hello react!</div>
};

export default App;
```

# 정리
- `useEffect`는 화면에 컴포넌트가 mount 또는 unmount 됐을 때 실행하고자 하는 함수를 제어하게 해주는 Hook
- 의존성 배열을 통해 함수의 실행 조건을 제어할 수 있고, 딱 한번만 실행하고자 할 때는 의존성 배열을 빈 배열로 둔다
