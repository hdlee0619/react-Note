# Dynamic Route?

Dynamic Route란, 동적 라우팅이라고도 하는데, `path`에 유동적인 값을 넣어 특정 페이지로 이동하게 구현하는 방법을 말한다. 

예를 들어 , works 페이지에 여러개의 work가 보이고 우리가 work마다 독립적인 페이지를 가지도록 구현하려면 어떻게 해야 할까?

## Dynamic Route 설정

```jsx
import React from "react";
import { BrowserRouter, Route, Routes } from "react-router-dom";
import Home from "../pages/Home";
import About from "../pages/About";
import Contact from "../pages/Contact";
import Works from "../pages/Works";

const Router = () => {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="about" element={<About />} />
        <Route path="contact" element={<Contact />} />
        <Route path="works" element={<Works />} />
				{/* 아래 코드를 추가 👇 */}
        <Route path="works/:id" element={<Works />} />
      </Routes>
    </BrowserRouter>
  );
};

export default Router;
```

`wortks:id`라고 path가 들어간다. 
`:id`라는 것이 바로 동적인 값을 받겠다는 의미이다. 
따라서 `works/1`, `works/2`, `works/3`, `works/4` ... `works/100` 모두 `<Work />`로 이동하게 된다. 

그리고 `:id`는 `useParams` hook을 사용해서 조회할 수 있고 조회한 값에 따라 다른 컴포넌트를 보여줄 수 있다. 
→ [[useParams]]
