# useCallback?

React.memo는 컴포넌트를 메모이제이션 했다면, `useCallback`은 인자로 들어오는 함수 그 자체를 메모리에 저장(memoization)한다. 

## 문제 상황 코드

→ [[memo(React.memo)#문제 상황 코드|React.memo에서 사용했던 코드 그대로 사용]]

#### App.jsx

```jsx
...

	// count를 초기화해주는 함수
  const initCount = () => {
    setCount(0);
  };

  return (
    <>
      <h3>카운트 예제입니다!</h3>
      <p>현재 카운트 : {count}</p>
      <button onClick={onPlusButtonClickHandler}>+</button>
      <button onClick={onMinusButtonClickHandler}>-</button>
      <div style={boxesStyle}>
        <Box1 initCount={initCount} />
        <Box2 />
        <Box3 />
      </div>
    </>
  );
}

...
```

#### Box1.jsx

```jsx
...

function Box1({ initCount }) {
  console.log("Box1이 렌더링되었습니다.");

  const onInitButtonClickHandler = () => {
    initCount();
  };

  return (
    <div style={boxStyle}>
      <button onClick={onInitButtonClickHandler}>초기화</button>
    </div>
  );
}

...
```

![](https://i.imgur.com/jO33AUI.png)

- `+ 버튼`이나, `- 버튼`을 누를 때 
- 그리고 `초기화` 버튼을 누를 때 

![](https://i.imgur.com/cpguIPC.png)

```ad-note
title: React.memo를 통해서 Box1.jsx를 메모이제이션을 했는데도 리-렌더링이 되는 이유?

함수형 컴포넌트를 사용하기 때문에 App.jsx가 리-렌더링이 되면서 코드가 다시 만들어지기 때문입니다. 

자바스크립트에서는 함수도 객체의 한 종류이기 때문에 모양은 같더라도 다시 만들어지면 함수를 저장하고 있는 주솟값이 달라지고 이에 따라 하위 컴포넌트인 Box1.jsx는 props가 변경됐다고 리액트에서 인식하게 됩니다. 

위의 코드에서 예를 들자면 App.jsx에 있는 initCount도 App.jsx가 리렌더링 될 때 다시 만들어지게 됨! 
따라서 Box1.jsx에서는 props(initCount)가 변경 됐다고 인식!
```

## useCallback을 통한 함수 메모이제이션

```jsx
// 변경 전
const initCount = () => {
  setCount(0);
};

// 변경 후
const initCount = useCallback(() => {
  setCount(0);
}, []);
```

이렇게 되면 Box1.jsx 컴포넌트는 리렌더링이 되지 않는다. 

> App.jsx가 처음 렌더링이 될 때, 메모리 공간에 `initCount`함수를 메모리 공간에 그래도 저장한다. [[의존성 배열]]안에 아무것도 없기 때문에 끝까지 변하지 않고 setCount 그 자체로 그대로 있음. 새로 함수가 리-렌더링이 되더라도 주소값이 새롭게 갱신되는 것이 아니라 메모이제이션 된 상태로 남아있음! 최초의 props만 계속 내려 받게 된다! 

## 조금 더 나아가기 

count를 초기화 할 때, 콘솔을 찍어보면

```jsx
...

// count를 초기화해주는 함수
const initCount = useCallback(() => {
  console.log(`[COUNT 변경] ${count}에서 0으로 변경되었습니다.`);
  setCount(0);
}, []);

...
```

> 위 코드의 예상 결과는 count를 증가, 감소 시킨만큼 그대로 찍힐 것 같지만 아무리 해도 `0`만 출력될 것이다. 

```ad-note
위와 같은 현상이 발생하는 니유는 useCallback이 count가 0일 때의 시점을 기준으로 메모리에 함수를 저장했기 때문에 우리는 [[의존성 배열|의존성 배열(dependency array)]]가 필요하게 된다. 

기존 코드의 dependency array에 count를 넣으면, count가 변경이 될 때마다 새롭게 함수를 할당하게 된다. 
```

```jsx
...

// count를 초기화해주는 함수
const initCount = useCallback(() => {
  console.log(`[COUNT 변경] ${count}에서 0으로 변경되었습니다.`);
  setCount(0);
}, [count]);

...
```
