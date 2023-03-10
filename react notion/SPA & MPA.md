
# SPA & MPA

## SPA 란?

- SPA란 Single Page Application의 약자이다.
- 단일 페이지 어플리케이션(SPA)는 현재 웹개발의 트랜드이다.
- 기존 웹 서비스는 요청시마다 서버로부터 리소스들과 데이터를 해석하고 화면에 렌더링하는 방식이다. SPA형태는 브라우저에 최초에 한번 페이지 전체를 로드하고, 이후부터는 특정 부분만 Ajax를 통해 데이터를 바인딩하는 방식이다. 
- 리액트가 SPA 방식

### 장점 & 단점

#### 장점

1.  컴포넌트 단위로 변경사항을 반영하기에 깜빡임이 없다(=페이스북 좋아요 클릭했을 때 딱 그 느낌)
2.  필요한 리소만 부분적으로 로딩(성능상 유리)
3.  모바일 앱 개발 시 동일한 API 사용하도록 설계 가능 

#### 단점
1. SEO가 어려움 : SPA는 index.html파일 하나밖에 없기 때문에 SEO가 약하다. 이 말이 무슨 말이냐면 검색엔진 즉 로봇이 찾을 수가 없다는 것이다. 왜냐면 서버로부터 페이지를 한 개만 받고 그 다음에는 동적으로 계속해서 그려지기 때문이다.(index.html을 한 개만 가지고 있기 때문에 Search할 수가 없다.) (SSR로 해결 가능한 부분
2. 초기 구동 속도가 느리다(Webpack 의 cod splitting으로 해결이 가능한 부분
3. 보안 이슈

## MPA란?

-  여러 개(Single)의 Page로 구성된 Application이다.
-  MPA는 SSR(Server Side Application) 방식으로 렌더링한다.  
- 새로운 페이지를 요청할 때마다 서버에서 렌더링된 정적 리소스(HTML, CSS, JavaScript)가 다운로드된다. 
-  페이지 이동하거나 새로고침하면 전체 페이지를 다시 렌더링한다.

### 장점 & 단점

#### 장점
1.  SEO가 유리하다
2.  서버에서 렌더링해 가져오기 때문에 첫 리로딩이 짧지만, 클라이언트가 JS파일을 모두 다운로드하고 적용하기 전까지 기능이 동작하지 않는다.
#### 단점
1. 하나의 변경사항을 반영하기 위해 전체 페이지를 리로드한다(reloading)(= 좋아요 한 번 누르면 페이지가 리로딩-->엄청 불편)-->즉 새 페이지 이동시 깜빡임
2.  서버 렌더링에 따른 부하 발생
3. 모바일 앱 개발 시 추가적인 백엔드 작업 필요하다.
