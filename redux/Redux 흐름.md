# Redux 흐름

## 리덕스의 핵심 요소  5가지

![](https://i.imgur.com/x4DmqoW.png)

-   Action:  
    State가 변하는것. “무엇이 일어날지”
- Reducer:  
    변화를 일으키는, 즉 데이터(state)를 수정하는 함수. action을 통해 어떠한 행동을 정의했다면, 그 결과 어플리케이션의 상태가 어떻게 바뀌는지는 특정하게 되는 함수이다.
-   Store:  
    action과 action에 따라 상태를 수정하는 reducer를 저장하는 어플리케이션에 있는 단 하나의 객체. 스토어는 State 를 수시로 확인해 View 한테 변경된 사항을 알려주는 역할을 한다.
-   Dispatch:  
    스토어의 내장 함수 중 하나로 리듀서에게 Action 을 발생하라고 시키는 것 store에서 reducer함수를 실행시켜 state를 업데이트한다.
-   Subscribe:  
    액션이 디스패치 될 때 마다 전달해준 함수를 호출한다.
-   Middleware: 액션을 디스패치 했을때 리듀서에서 이를 처리하기에 앞서 사전에 지정된 작업들을 실행한다.  
    thunk 와 saga 가 대표.

## 리덕스 흐름

![](https://i.imgur.com/7V1fkQp.gif)

1.  View 에서 액션이 일어난다.
2.  dispatch 에서 action이 일어나게 된다.
3.  action에 의한 reducer 함수가 실행되기 전에 middleware가 작동한다.
4.  middleware 에서 명령내린 일을 수행하고 난뒤, reducer 함수를 실행한다. 
5.  reducer 의 실행결과 store에 새로운 값을 저장한다.
6.  store의 state에 subscribe 하고 있던 UI에 변경된 값을 준다.

### 간단 정리 

**action —> dispatch —> reducer**

## 리덕스 3가지 대표 룰

-  하나의 어플리케이션은 하나의 Store만 가진다.
-  리듀서는 순수함수이다.  
    동일안 파라미터로 호출 된 리듀서는 언제나 같은 패턴의 결과값을 반환해야만 한다.
-  state는 read-only 이다  
    기존의 state 고유 값은 수정하지 않고 새로운 state 를 만들어 이를 수정하는 방식으로 업데이트를 한다.이는 리덕스 고유의 불변성을 지키기 위함임.