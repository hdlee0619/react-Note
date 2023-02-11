# redux hooks

## react-redux

- state를 조회하기 위한 **useSelector**를 사용할 수 있다.
-   action을 발생시키기 위한 **useDispatch**를 사용할 수 있다.

## useSelector

- connect 함수를 이용하지 않고 리덕스(store)의 state를 조회할 수 있음

```jsx
import { useSelector } from 'react-redux' const user = useSelector(state => state.user);
```

## useDispatch

- 생성한 action을 useDispatch를 통해 발생시킬 수 있다. 
- 만들어둔 액션생성 함수를 import한다. 

```jsx
import { change_user } from '../modules/user'
import { useDispatch } from 'react-redux'

const User = () => {
  ...
  const dispatch = useDispatch();
  dispatch(change_user(user));
  ...
}
//위에서 dispatch한 change_user는 아래와 같이 정의된 액션 생성 함수이다.
export const change_user = createAction(CHANGE_USER, user => user);
```
