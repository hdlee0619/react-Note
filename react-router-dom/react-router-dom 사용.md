# react-router-dom 사용

## 사용 방법 순서

아래 순서대로 코드를 작성해 `react-router-dom`을 사용해볼 것이다. 

1. 페이지 컴포넌트 생성
2. `Router.js` 생성 및 router 설정 코드 작성
3. `App.js`에 import 및 적용

### 1. 페이지 컴포넌트 생성

> 생성 페이지 : `Home`, `About`, `Contact`, `Works` 총 4개의 컴포넌트

`src` 폴더에 pages라는 폴더를 만들고 그 안에 component 생성

```jsx
import React from "react";
// react-router-dom 을 사용하기 위해 아래 API들을 import
import { BrowserRouter, Route, Routes } from "react-router-dom";

//2. Router 라는 함수를 만들고 아래와 같이 작성
// BrowserRouter를 Router로 감싸는 이유는, 
// SPA의 장잠인 브라우저가 깜빡이지 않고 다른 페이지로 이동할 수 있게 해줌
import Home from "../pages/Home";
import About from "../pages/About";
import Contact from "../pages/Contact";
import Works from "../pages/Works";

const Router = () => {
  return (
    <BrowserRouter>
      <Routes>
		{/* 
		Routes안에 이렇게 작성합니다. 
		Route에는 react-router-dom에서 지원하는 props들이 있습니다.
		path는 우리가 흔히 말하는 사용하고싶은 "주소"를 넣어주면 됩니다.
		element는 해당 주소로 이동했을 때 보여주고자 하는 컴포넌트를 넣어줍니다.
		 */}
        <Route path="/" element={<Home />} />
        <Route path="about" element={<About />} />
        <Route path="contact" element={<Contact />} />
        <Route path="works" element={<Works />} />
      </Routes>
    </BrowserRouter>
  );
};

export default Router;
```

### 2. App.js에 Router.js import 해주기

```jsx
import React from "react";
import Router from "./shared/Router";

function App() {
  return <Router />;
}

export default App;
```

`Router.js`를 App 컴포넌트에 넣어주는 이유는 프로젝트에서 가장 최상위에 존재하는 컴포넌트가 App.js이기 때문..!

우리가 어떤 컴포넌트를 화면에 띄우던, 항상 App.js를 거쳐야만 한다. 그래서 path별로 분기가 되는 `Router.js`를 App.js에 위치시키고 서비스를 이용하느 모든 사용자가 항상 `App.js → Router.js`를 거치도록 코드를 구현해주는 것이다. 
