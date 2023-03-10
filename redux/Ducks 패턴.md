# Ducks 패턴?

리덕스를 사용하기 위해서는 결국 개발자가 리덕스의 구성요소를 모두 만들어야만 사용이 가능하다. 그런데 만약 리덕스 모듈을 개발하는 개발자마다 구성요소들을 제 각각 구현한다면? 그렇게 된다면 그 개발자와 현업을 해야할 때 구성요소를 구분하기가 쉽지 않을 것이다. 

그래서 `Erik Rasmussn`이라는 개발자가 이것을 패턴화하여 작성할 것을 제안했는데, 그것이 바로 **Ducks** 패턴이다. 

## Ducks 패턴으로 작성하기 

### 1. Reducer 함수를 `export default`로 한다. 

```jsx
// Reducer
export default function reducer(state = {}, action = {}) {
  switch (action.type) {
    // do reducer stuff
    default: return state;
  }
}
```

### 2. Action creator 함수들은 `export`로 한다. 

```jsx
// Action Creators
export function loadWidgets() {
  return { type: LOAD };
}

export function createWidget(widget) {
  return { type: CREATE, widget };
}

export function updateWidget(widget) {
  return { type: UPDATE, widget };
}

export function removeWidget(widget) {
  return { type: REMOVE, widget };
}
```

### 3. Action typedms `app/reducer/ACTION_TYPE` 형태로 작성한다. 

> (외부 라이브러리로서 사용될 경우 또는 외부 라이브러리가 필요할 경우에는 UPPER_SNAKE_CASE 로만 작성해도 무관하다. )

```jsx
// Actions
const LOAD   = 'my-app/widgets/LOAD';
const CREATE = 'my-app/widgets/CREATE';
const UPDATE = 'my-app/widgets/UPDATE';
const REMOVE = 'my-app/widgets/REMOVE';
```
