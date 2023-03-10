# 리-렌더링
→ [[Rendering#2. 리렌더링|리-렌더링 정리]]

## 리-렌더링의 발생 조건

- 컴포넌트에서 state가 바뀌었을 때
- 컴포넌트가 내려받은 props가 변경되었을 때
- 부모 컴포넌트가 리-렌더링 된 경우 자식 컴포넌트 **모두** 리-렌더링 ^367a5a

## 최적화

[[useState]], [[useEffect]], [[useRef]], [[useContext]] 등 많은 hook에서 리-렌더링이 발생하게 된다. 
하지만 리액트에서 리-렌더링이 자주 일어난다는 것은 좋은 현상만은 아니다. 리-렌더링을 최대한 줄여야, _불필요한 렌더링을 줄여야_ 하는데 이 작업을 `최적화(Optimization)`이라고 한다. 

### 최적화 방법

- [[memo(React.memo)|React.memo]] : 컴포넌트를 캐싱
- [[useCallback]] : 함수를 캐싱
- [[useMemo]] : 값을 캐싱