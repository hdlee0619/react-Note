
# useNavigate?

다른 페이지로 보내고자 할 때 사용할 수 있다. 
html에서 `a` tag와 상당히 유사한데
버튼의 클릭 이벤트 핸들러에 아래와 같이 코드를 작서하면 버튼을 클릭했을 때 우리가 보내고자 하는 path로 페이지를 이동시킬 수 있다. 
꼭 버튼이 아니더라도, 컴포넌트의 클릭 이벤트 핸들러를 통해서 활용이 가능하다. 

> 1. `navigate`를 생성
> 2. `navigate('보내고자하는 url')`을 통해 페이지를 이동

```jsx
// src/pages/home.js
import { useNavigate } from "react-router-dom";

const Home = () => {
  const navigate = useNavigate();

  return (
    <button
      onClick={() => {
        navigate("/works");
      }}
    >
      works로 이동
    </button>
  );
};

export default Home;
```