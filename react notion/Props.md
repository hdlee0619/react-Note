# 정의

## 컴포넌트 끼리의 정보교환 방식!

부모 컴포넌트가 자식 컴포넌트에게 물려준 데이터에요! 다시 말해, **컴포넌트 간의 정보 교류 방법**이다. 

1.  props는 반드시 위에서 아래 방향으로 흐른다. 즉, [부모] → [자식] 방향으로만 흐른다==(단방향)==
2.  props는 반드시 읽기 전용으로 취급하며, 변경하지 않는다.

## 코드로 보기

```jsx
// src/App.js
import React from "react";

function App() {
	return <GrandFather />;
}

function GrandFather() {
	return <Mother />;
}

function Mother() {
	const name = '홍부인';
	return <Child motherName={name} />; // 💡"props로 name을 전달."
}

function Child(props) {
	console.log(props) // {motherName: '흥부인'} 출력
	return <div>연결 성공</div>;
}

export default App;
```

## 사용 방법

#### 1. 하위 컴포넌트에 값을 전달할 때 사용

```jsx
import Component from './Component';

function Sample() {
  const text = '항해 12기 화이팅';

  return (
      <Component text={text}/> /* 항해 12기 화이팅 */
  );
}

function Component(props) {
  return (
      <div>{props.text}</div>
  );
}
```

#### 2. defaultProps
- defaultProps는 props 값을 따로 지정하지 않았을 때 설정하는 기본값
- 하위 컴포넌트에 전달되는 props가 없을 때 defaultProps를 설정하여 값을 지정할 수 있음

```jsx
import Component from './Component';

function Sample() {

  return (
    <React.Fragment>
      <Component/>
    </React.Fragment>
  );
}

function Component(props) {
  return (
    <React.Fragment>
      <div>{props.text}</div> /* 디폴트 값입니다. */
    </React.Fragment>
  );
}

Component.defaultProps = {
	text: '디폴트 값입니다.'
};
```

#### 3. children
- props의 children을 사용하면 컴포넌트 태그 사이의 내용을 보내줄 수 있음

```jsx
import Component from './Component';

function Sample() {
	const text = '12기 a반';

  return (
    <React.Fragment>
      <Component text={text}>항해 99 12기</Component>
    </React.Fragment>
  );
}

function Component(props) {
  return (
    <React.Fragment>
      <div>{props.text}</div> /* 12기 a반 */
			<div>{props.children}</div> /* 항해 99 12기 */
    </React.Fragment>
  );
}
```

#### 4. props destructuring (구조 분해 할당)
-   ES6의 비구조화 할당을 사용하면 props 객체의 값을 추출하여 사용할 수 있음
-   비구조화 할당은 함수형 컴포넌트에서 많이 사용
```jsx
function Component(props) {
	const {name, children} = props; // 구조를 분해해서 변수에 담아 사용

  return (
    <React.Fragment>
      <div>{text}</div>
			<div>{children}</div>
    </React.Fragment>
  );
}
```

#### 5. prop-types
- 컴포넌트 props의 타입이나 필수값을 지정할 때 사용

```jsx
import PropTypes from 'prop-types';

function Component(props) {
  const {num, text, children} = props;

  return (
    <React.Fragment>
      <div>{text}</div>
			<div>{children}</div>
			<div>{num}</div>
    </React.Fragment>
  );
}

Component.propTypes = { // 타입을 지정
  text: PropTypes.string.isRequired,
  num: PropTypes.number
};
```

```ad-warning
title: 주의점

-  props가 Types에서 지정한 타입과 일치하지 않으면 에러 발생
-  필수값으로 지정된 props를 전달하지 않을 경우에도 에러 발생
-  따라서 propTypes를 사용한 경우엔 타입과 필수로 설정된 props에 유의하여 사용
```

## prop drilling

### 정의

prop drilling이란 부모컴포넌트에서 자식 컴포넌트, 그 자식의 컴포넌트 ...
부모 → 자식 → 그 자식 → 그자식의 자식 ...
위와 같이 데이터를 계속 뚫고 내려가는 것을 말한다. 

### 문제점

prop 전달이 3~5개 정도의 스코프인 프로젝트에서는 크게 문제가 되지 않지만 prop 전달이 10번, 20번 정도 더 많은 과정을 거치게 되면 prop추적이 힘들게 되고 그에 따라 유지보수가 더욱 어려워지게 된다. 

### 해결방법

#### 전역 상태 관리 라이브러리 사용

`redux`, `MobX`, `recoil` 등을 사용하여 해당 값이 필요한 컴포넌트에서 직접 불러서 사용하기