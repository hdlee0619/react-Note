# JSX란?

- JavaScript와 XML을 합친 것, HTML을 품은 JS -> JSX

```jsx
// JavaScript를 확장한 문법
// JavaScript의 모든 기능이 포함되어 있으며, React Element를 생성하기 위한 문법
const element = <h1>Hello, world!</h1>;
```

```ad-note
리액트에서는 딱 하나의 html 파일만 존재(public 폴더의 index.html)하는데, 리액트 에서는 App.js 파일의 JSX문법을 사용해서 React 요소를 만들고 DOM에 렌더링 시켜서 그리게 된다. 
즉, 자바스크립트 파일이 html을 그리는 것.
```

→ [[DOM? virtual DOM ?|DOM 정보]]
→ [[JSX|JSX 사용]]

HTML 태그는 .js 파일에서 쓸 수 없기 때문에 나온 것이 JSX이며, 자바스크립트 안에서 html 태그같은 마크업을 넣어 뷰(UI) 작업을 편하게 할 수 있다. 

```jsx
const start_half = <div>
    <h1>안녕하세요!</h1>
    <p>시작이 반이다!</p>
  </div>;
```

```ad-warning
title: 그럼 JSX에서 쓰는 html 태그는 DOM 요소인가?

정확히는 REACT 요소이다. 차이는 가상돔에서 더 자시히 설명..!
리액트 돔을 구성하는 건 리액트 요소이고 DOM을 구성하는건 DOM 요소이다. 
```


[[JSX]]

# 규칙

#### 1. 태그는 꼭 닫아주기!

#### 2. 무조건 1개의 엘리먼트를 반화하기!

#### 3. JSX에서 javascript 값을 가져오려면 중괄호를 사용하기 !

JSX가 편한 이유는 html태그 내(JSX이지만)에서 JS문법을 사용할 수 있다. 
→ map, 삼항 연산자 등등 사용이 가능.. 

```jsx
import React from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  const number = 1;

  return (
    %3Cdiv className="App"%3E
      <p>안녕하세요! 리액트 반입니다 :)</p>
      {/* JSX 내에서 코드 주석은 이렇게 씁니다 :) */}
      {/* 삼항 연산자를 사용했어요 */}
      <p>{number > 10 ? number+'은 10보다 크다': number+'은 10보다 작다'}</p>
    </div>
  );
}

export default App;
```

#### 4. class 대신 className!

JSX는 html이 아니기 때문에 속성값이 다른 경우가 있다. 

#### 5. 인라인으로 style을 줄 수 있다. 

주로 사용하진 않는다고 한다. 