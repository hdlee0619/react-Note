# Link?

Link는 html 태그 중에 a 태그의 기능을 대체하는 API 이다. 만약 JSX에서 a 태그를 사용해야 한다면, 반드시 Link를 이용해서 구현해야 한다. 

> 왜냐하면 a 태그를 사용하게 되면 페이지를 이동하면서 브라우저가 새로고침(refresh)가 되고 브라우저가 새로고침이 되면 모든 컴포넌트가 다시 렌더링되야 하고, 리덕스나 useState를 통해 메모리 상에 구축해놓은 모든 상태값이 초기화 된다.
> - 이것은 성틍에 악역향을 줄 수 있고, 불필요한 움직임이다. 

## 사용 코드

```jsx
import { Link, useLocation } from 'react-router-dom';

const Works = () => {
  const location = useLocation();
  console.log('location :>> ', location);
  return (
    <div>
      <div>{`현재 페이지 : ${location.pathname.slice(1)}`}</div>
      <Link to="/contact">contact 페이지로 이동하기</Link>
    </div>
  );
};

export default Works;
```