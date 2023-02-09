# Redux 설정

### (1) 리덕스 설치

리액트에서 리덕스를 사용하기 위해서는 2개의 패키지를 설치해야 한다. 
vscode 터미널에서 아래 명령어를 입력해서 설치하세요
> 참고로 `react-redux`라는 패키지는 __리덕스를 리액트에서 사용할 수 있도록 서로 연결시켜주는 패키지__ 입니다. 

```bash
yarn add redux react-redux

# 아래와 같은 의미
yarn add redux
yarn add react-redux
```

### (2) 폴더 구조 생성하기


![](https://i.imgur.com/i9sxBTp.png)

위의 그림과 같이 폴더 구조를 생성

1. `src` 폴더 안에 `redux` 폴더를 생성
2.  `redux` 폴더 안에 `config`, `modules` 폴더를 생성
3.  `config` 폴더 안에 `configStore.js`파일을 생성합니다.

각각의 폴더와 파일은 역할이 있다.

-   `redux` : 리덕스와 관련된 코드를 모두 모아 놓을 폴더
-   `config` : 리덕스 설정과 관련된 파일들을 놓을 폴더
-   `configStore` : “중앙 state 관리소" 인 Store를 만드는 설정 코드들이 있는 파일
-   `modules` : 우리가 만들 State들의 그룹이라고 생각하면 됩니다. 예를 들어 `투두리스트`를 만든다고 한다면, 투두리스트에 필요한 `state`들이 모두 모여있을 `todos.js`를 생성하게 되텐데요, 이 `todos.js` 파일이 곧 하나의 모듈이 된다.

## 설정 코드 작성

```ad-warning
title: 설정 코드 작성 시, 주의 사항

1. 우리가 작성하는 설정코드는 이해할 필요가 없는 코드들 입니다. 코드 분석 ❌

	설정 코드를 작성하는 이유는 리덕스를 만든 리덕스 팀에서 이렇게 설정을 하라고 안내하고 있기 때문

2. 리덕스 사용 "방법"을 중점으로 공부할 것

	어떻게 만들었는지, 왜 이렇게 설정하는지보다 *리덕스를 사용하는 방법에 집중할 것*
```

### src/configStore.js 폴더 코드

```jsx
import { createStore } from "redux";
import { combineReducers } from "redux";

/*
1. createStore()
리덕스의 가장 핵심이 되는 스토어를 만드는 메소드(함수) 입니다. 
리덕스는 단일 스토어로 모든 상태 트리를 관리한다고 설명해 드렸죠? 
리덕스를 사용할 시 creatorStore를 호출할 일은 한 번밖에 없을 거예요.
*/

/*
2. combineReducers()
리덕스는 action —> dispatch —> reducer 순으로 동작한다고 말씀드렸죠? 
이때 애플리케이션이 복잡해지게 되면 reducer 부분을 여러 개로 나눠야 하는 경우가 발생합니다. 
combineReducers은 여러 개의 독립적인 reducer의 반환 값을 하나의 상태 객체로 만들어줍니다.
*/

const rootReducer = combineReducers({}); 
const store = createStore(rootReducer); 

export default store; 
```

### index.js

디렉토리 가장 최상단의 `index.js`에 입력

```jsx
// 원래부터 있던 코드
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import reportWebVitals from "./reportWebVitals";

// 추가할 코드
import store from "./redux/config/configStore";
import { Provider } from "react-redux";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(

	//App을 Provider로 감싸주고, configStore에서 export default 한 store를 넣어줍니다.
  <Provider store={store}> 
    <App />
  </Provider>
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

## 정리 

-   리액트에서 리덕스를 사용하려면, `redux`, `react-redux` 가 필요하다.
-   설정코드는 지금 당장 이해 할 필요가 없다.
-   “중앙 State 관리소"를 Store (스토어)라고 부른다.
-   모듈이란, State들이 그룹이다.