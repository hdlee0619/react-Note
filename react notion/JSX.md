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

→ [[DOM? virtual DOM ?#DOM]]  

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

# 규칙



## 2. 무조건 1개의 엘리먼트를 반환할 것

## 3. JSX 내에서 JS 문법을 사용할 때는 중괄호 열기