# Life Cycle?

리액트 컴포넌트는 각각 `Mount → Update → Unmount`의 과정을 거치게 된다. 
- 사람처럼 태어나고, 변화하고 죽는 것

리액트 생명주기(라이프 사이클)란, 컴포넌트 중심 라이브러리의 집합체라고 보면 된다. 
모든 컴포넌트에는 각각의 생명주기가 존재하고 각 생명주기에 맞는 메서드들이 있다. 

> 생명주기는 클래스형 컴포넌트와 많은 관련이 있는데 현재는 함수형 컴포넌트를 대부분 사용하기 때문에 시간을 너무 쏟지 말고 나중에 필요할 때 다시 찾아서 보는 걸 추천!

## 생명주기 도식화

![](https://i.imgur.com/dBAdkm8.png)

## Mount

### (1) 개요

컴포넌트가 생성될 때를 말한다. 
다음과 같은 메서드가 있음..!

- constructor()
- getDerivedStateFromProps(nextProps, prevState)
- render()
- componentDidMount()

### (2) 각 메서드 소개

- constructor
	a. 컴포넌트가 맨 처음 만들어 질 때 호출
	b. 생성자

- getDerivedStateFromProps
	a. 부모 컴포넌트로부터 props를 전달 받을 때, state에 값을 일치시키는 역할을 하는 메서드
	b. 마운트 될 때, 업데이트(리렌더링) 될 때도 호출'

- render
	a. 최초 mount가 준비완료 되면 호출되는, 즉 렌더링 하는 메서드
	b. 컴포넌트를 DOM에 마운트하기 위해 사용

- componentDidMount
	a. 컴포넌트가 브라우저에 표시가 된 후 호출되는 메서드

## Update

### (1) 개요

컴포넌트가 갱신될 때를 말한다. 
다음과 같은 메서드가 있음..!

- getDerivedStateFromProps(nextProps, prevState)
- shouldComponentUpdate()
- render()
- getSnapshotBeforeUpdate()
- componentDidUpdate()

### (2) 각 메서드 소개

- getDerivedStateFromProps
	a. Mount 과정에서도 동일하게 호출되었던 메서드.
	b. 부모 컴포넌트로부터 props를 전달받을 때, state에 값을 일치시키는 역할을 하는 메서드

- shouldComponentUpdate
	a. 리렌더링 여부 판단(함수 호출 결과 : true / false)
	- i. `true`인 경우 : 리렌더링 진행
	- ii. `false`인 경우 : 리렌더링 하지 않음
	b. 함수형 컴포넌트에서 `memo`, `useMemo`, `useCallback`이 이 역할을 대신한다. 

- render
	a. 변경사항 반영이 다 되어 준비완료 되면 호출되는, 즉 렌더링 하는 메서드
	b. 컴포넌트를 DOM에 마운트하기 위해 사용

- getSnapshotBeforeUpdate
	a. 컴포넌트에 변화가 일어나기 직전 DOM의 상태를 저장
	b. componentDidUpdate 함수에서 사용하기 위한 스냅샷 형태의 데이터

- componentDidUpdate
	a. 컴포넌트 업데이트 작업 완료 후 호출

## Unmount

### (1) 개요

컴포넌트가 DOM에서 제거되는 시점을 말한다.
다음과 같은 메서드가 있음..!

- componentWillUnmount

### (2) 각 메서드 소개

- componentWillUnmount
	a. 컴포넌트가 사가지기 전 호출되는 메서드
	b. useEffect의 return과 동일