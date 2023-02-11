# useParams ?

`useParams`는 path에 있는 (`:<여기 있는 값>`) 이름으로 값을 조회할 수 있게 해주는 훅!

그래서 만약 `works/1`로 이동하면 `useParams`로 값을 빼면 **1**이라는 값을 주고, `works/100`로 이동하면 **100**이라는 값을 준다. 

## 사용 코드

### shared > data.js

```javascript
export const data = [
  {
    id: 1,
    toDo: '리액트 배우기',
  },
  {
    id: 2,
    toDo: '노드 배우기',
  },

  ...
];
```

### shared > Router.js

```javascript
... 
{/* useParams를 사용하기 위해 ':id'를 준다 */}
<Route path="works/:id" element={<Work />}></Route>

...
```

### pages > Works.jsx

```jsx
...
{/* map을 통해 work component와 연결된 Link tag 뿌리기 */}
{data.map((item) => {
        return (
          <div key={item.id}>
            {item.id}&nbsp;
            <Link to={`/works/${item.id}`}>{item.toDo}</Link>
          </div>
        );
      })}
...
```

### pages > Work.jsx

```jsx
import React from 'react';
import { useParams } from 'react-router-dom';
import { data } from '../shared/data';

function Work() {
  const params = useParams();

  // 어떤 todo인지 찾아보기
  // 조건에 맞는 것만 return
  const foundData = data.find((item) => {
    console.log('item.id : ', item.id); // type: int
    console.log('params.id : ', params.id); // type: string
    return String(item.id) === params.id;
  });

  console.log(foundData);
  // id 값에 따라 동적으로 출력이 가능하다!
  return <div>{foundData.toDo}</div>;
}

export default Work;
```