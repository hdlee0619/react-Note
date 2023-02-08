# useRef?

## (1) useRef hook 소개

JavaScript에서는 DOM 요소에 접근하기 위해서 아래와 같은 코드를 사용했었다. 

```javascript
// (1) getElementById 이용
const divTag = document.getElementById('#myDiv');

// (2) querySelector 이용
const divTag2 = document.querySelector('#myDiv');
```

리액트에서도 DOM을 선택해야 할 상황이 생기기 마련인데, 예를 들어 화면이 렌더링 되자마자 특정 `input` 태그가 focusing이 돼야 하는 경우가 있다. → [[input 태그 자동 focusing| 항해99 입문 과제 to Do List 에서 사용]]

이때 DOM 요소에 접근할 수 있도록 하는 React hook이 `useRef`이다. 

## (2) 사용 방법

```jsx
import "./App.css";
import { useRef } from "react";

function App() {
  const ref = useRef("초기값");
  console.log("ref", ref); // {current: '초기값'} 출력

  return (
    <div>
      <p>useRef에 대한 이야기에요.</p>
    </div>
  );
}

export default App;
```

변경도 가능하다. 

```jsx
import "./App.css";
import { useRef } from "react";

function App() {
  const ref = useRef("초기값");
  console.log("ref 1", ref); // {current: "초기값"}

  ref.current = "바꾼 값";
  console.log("ref 1", ref); // {current: '바꾼 값'}

  return (
    <div>
      <p>useRef에 대한 이야기에요.</p>
    </div>
  );
}

export default App;
```

```ad-important
이렇게 설정된 ref 값은 컴포넌트가 계속해서 렌더링 되어도 unmount 전까지 값을 유직하게 됨
```

위와 같은 특징 때문에 useRef의 사용용도는 다음과 같다.

### 사용 법

#### 1. 저장공간

a. `state`와 비슷한 역할을 한다. _다만_ `state`는 변화가 일어나면 다시 렌더링이 일어나고 내부 변수들은 초기화가 된다. 
b. `ref`에 저장한 값은 렌더링을 일으키지 않는다. 즉, `ref`의 값 변화가 일어나도 렌더링으로 인해 내부 변수들이 초기화 되는 것을 막을 수 있다.
c. 컴포넌트가 100번 렌더링 → `ref`에 저장한 값은 유지

정리하자면, 
- **state는 리렌더링이 꼭 필요한 값을 다룰 때 쓰면 된다**
- **ref는 리렌더링을 발생시키지 않는 값을 저장할 때 사용한다.**

#### 2. DOM

a. 렌더링이 되자마자 특정 input이 focusing 돼야 한다면 `useRef`를 사용할 수 있다. 
[[input 태그 자동 focusing|항해99 과제 toDoList에서 사용]]

#### 간단한 사용 코드

```jsx
import { useEffect, useRef } from "react";
import "./App.css";

function App() {
  const idRef = useRef("");

  // 렌더링이 될 때
  useEffect(() => {
    idRef.current.focus();
  }, []);

  return (
    <>
      <div>
        아이디 : <input type="text" ref={idRef} />
      </div>
      <div>
        비밀번호 : <input type="password" />
      </div>
    </>
  );
}

export default App;
```