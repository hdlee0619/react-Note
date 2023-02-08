# 컴포넌트란? 

리액트 공식문서에서의 컴포넌트는
> - 컴포넌트를 통해 **UI를 재사용**이 가능한 개별적인 여러 조각으로 나누고, 각 조각을 개별적으로 살펴볼 수 있다.
> - 덕분에 컴포넌트는 UI 구축 작업을 훨씬 쉽게 만들어 준다
> - 개념적으로 컴포넌트는 ==JavaScript 함수==와 유사.
> - "props"라고 하는 임의의 입력을 받은 후, 화면에 어떻게 표시되는지를 기술하는 ==React 엘리먼트를 반환==

## DOM (명령형 프로그래밍)

리액트의 컴포넌트 기반 개발 이전에는 브라우저에서 동적으로 변하는 UI를 표현하기 위해 직접 DOM객체를 조작을 하는 명령형 프로그래밍 방식으로 구현했다. 

### 명령형(DOM)과 선언형(React)의 차이

- 명령형으로 작성된 코드의 경우 출력을 위해 컴퓨터가 수행하는 절차를 일일히 코드로 작성해야함

```javascript
// Hello, World! 화면에 출력하기
// 순수 javaScript 명령형 코드
const root = document.getElementById('root'); 
const header = document.createElement('h1'); 
const headerContent = document.createTextNode(
	'Hello, World!'
);

header.appendChild(headerContent); 
root.appendChild(header);
```

- React는 내가 UI를 선언하고 render함수를 호출하면 react가 알아서 절차를 수행해 화면에 출력해준다.
- **어떻게** 그러야할지는 React 내부에 잘 숨겨져 추상화 되어 있다. 
```javascript
// React 코드 (선언적인)
const header = <h1>Hello World</h1>; // jsx
ReactDOM.render(header, document.getElementById('root'));
```

## React에서 컴포넌트를  표현하는 두 가지 방법

### 함수형 컴포넌트

```jsx
// props라는 입력을 받음
// 화면에 어떻게 표현되는지를 기술하는 React 엘리먼츠를 반환(return)

function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// 훨씬 쉬운 표현을 해보면 아래와 같죠.
function App () {
	return <div>hello</div>
}
```

### 클래스형 컴포넌트

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

두 컴포넌트 모두 기능상으로는 동일하지만, **공식 홈페이지에서는 함수형 컴포넌트 사용**을 권장하고 있다. 

위를 보면 알겠지만 `html`(JSX)을 `return`하는 형태이다. 

## 부모-자식 컴포넌트

### 컴포넌트 안에 컴포넌트 넣기

컴포넌트는 다른 컴포넌트를 품을 수 있는데, 다른 컴포넌트를 품는 컴포넌트를 **부모 컴포넌트**라고 하고, 품어지는 컴포넌트를 **자식 컴포넌트**라고 한다.

```jsx
// src/App.js
import React from "react";

function Child() {
  return <div>나는 자식입니다.</div>;
}

function App() {
  return <Child />;
}

export default App;
```

`App.js` 파일 안에서 `Child`라는 새로운 컴포넌트를 만들었고, Child 컴포넌트를 App 컴포넌트에서 마치 HTML 태그를 쓰듯이 넣었다. 이렇게 한 컴포넌트 안에 다른 컴포넌트를 넣을 수 있습니다.

이렇게 코드를 작성하면, 화면에는 “나는 자식입니다” 라는 문장이 보여진다. 왜냐하면 이 파일에서 내보내진 _(우리는 “내보내진” 이라는 것을 `export default` 라고 함)_ 컴포넌트는 App 컴포넌트 이기때문에 App 컴포넌트가 화면에 보여진다. 하지만 App 컴포넌트는 Child 컴포넌트를 자식으로 삼고 있기 때문에 결국 자식 컴포넌트에 있는 “나는 자식입니다" 라는 문장이 보여지게 되는 것 이다.

이렇게 만들어진 컴포넌트는 마치 HTML 태그를 쓰듯이 사용하여 화면에 보여지게 할 수 있습니다. 앞으로는 “화면에 보여지게 하다"를 줄여서 `Rendering` 이라고 부르겠습니다. 그리고 이렇게 함수로 만들어진 컴포넌트를 html 태그 사용하듯이 코드를 작성하는 이 방식을 [[JSX]]라고 한다.