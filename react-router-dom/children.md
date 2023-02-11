# children?

> **공식문서**
> 어떤 컴포넌트들은 어떤 자식 엘리먼트가 들어올지 미리 예상할 수 없는 경우가 있다. 범용적인 '박스'역할을 하는 Sidebar 혹은 Dialog와 같은 컴포넌트에서 특히 자주 볼 수 있다. 

여기서 말하는 범용적인 “박스” 역할을 하는 컴포넌트란 크게 봤을 때 Layout 역할을 하는 컴포넌트라고 생각해볼 수 있습니다. children props를 찾아보시면 composition이라는 말을 많이 보시게 될 텐데요, composition은 합성이라는 의미가 있다고 합니다.

이번 섹션에서는 children props를 가지고 페이지 레이아웃을 만들며 개별적으로 존재하는 Header, Footer, Page를 합성하여 개발자가 의도하는 UI를 만들어주는 Layout 컴포넌트를 만들어 보겠습니다.

## 사용 코드

### src/shared/Layout.js

```jsx
// src/shared/Layout.js

import React from 'react';

function Header() {
  return (
    <div style={{ ...HeaderStyles }}>
      <span>Sparta Coding Club - Let's learn React</span>
    </div>
  );
}

function Footer() {
  return (
    <div style={{ ...FooterStyles }}>
      <span>copyright @SCC</span>
    </div>
  );
}

function Layout({ children }) {
  return (
    <div>
      <Header /> 
      {/* 
      고정되고 Header와 Footer사이에서 
      계속 컴포넌트가 
      변경되는 식 
      */}
      <div style={{...layoutStyles}}>
        {children}
      </div>
      <Footer />
    </div>
  );
}

export default Layout;
```

### src/shared/Router.js

```jsx
import React from 'react';
import { BrowserRouter, Route, Routes } from 'react-router-dom';
import Home from '../pages/Home';
import About from '../pages/About';
import Contact from '../pages/Contact';
import Works from '../pages/Works';
import Layout from './Layout';

const Router = () => {
  return (
    <BrowserRouter>
      <Layout>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="about" element={<About />} />
          <Route path="contact" element={<Contact />} />
          <Route path="works" element={<Works />} />
        </Routes>
      </Layout>
    </BrowserRouter>
  );
};

export default Router;
```
