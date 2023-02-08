
# export

**`export`**  문은 JavaScript 모듈에서 함수, 객체, 원시 값을 내보낼 때 사용합니다. 내보낸 값은 다른 프로그램에서 `import문`으로 가져가 사용할 수 있다

### export(유명 내보내기)

- export는 여러개를 내보낼 수 있다
- 가져갈 때는 내보낸 이름과 동일한 이름을 사용해야 한다
- 식별자 충돌을 피하기 위해 유명 내보내기 중 이름을 바꿔줄 수도 있다

```jsx
export { myFunction as function1, myVariable as variable }; //myFunction 를 function1로 변경 //myVariable 를 variable로 변경
```

# export default (기본 내보내기)

- `export default`는 1개만 내보낼 수 있다.
- 기본 내보내기는 어떤 이름으로도 가져올 수 있다. 

```jsx
//export default 예시
//파일에서 다른파일로 내보내기
export default function test(){ // test 라는 이름으로 내보냈지만
return;
} 

//파일에서 다른파일로 가져오기

import text from '/파일 주소 넣기' // text라는 이름으로 받아옴 
```
