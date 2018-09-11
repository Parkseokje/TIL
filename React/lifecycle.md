# lifecycle

컴포넌트에는 라이프사이클(수명주기, lifecycle)이 존재한다.
라이프사이클 메서드의 종류는 총 10 가지이며, 마운트, 업데이트, 언마운트 총 3 가지 카테고리로 구분된다.

## 마운트

DOM 이 생성되고, 웹 브라우저상에 나타나는 것을 마운트라 하며, 이 과정에서 호출하는 메소드는 다음과 같다.

1. constructor: 컴포넌트 생성 시 호출되는 클래스 생성자 메서드
2. getDerivedStateFromProps: props 에 있는 값을 state 에 동기화 시 사용

```javascript
static getDerivedStateFromProps(nextProps, pervState) {
  if (nextProps.value !== prevState.value) {
    return { value: nextProps.value }
  }
  return null
}
```

3. render: UI 를 렌더링하는 메서드
4. componentDidMount: 컴포넌트가 웹브라우저상에 나타난 후 호출화는 메서드

## 업데이트

### 컴포넌트 업데이트 상황

1. props 가 바뀔 때
2. state 가 바뀔 때
3. 부모 컴포넌트가 리렌더링될 때
4. this.forceUpdate 로 강제 리렌더링할 때

컴포넌트 업데이트 과정에서 호출되는 메소드는 다음과 같다.

1. getDerivedStateFromProps: 마운트 혹은 props 가 변경되는 경우 호출
2. shouldComponentUpdate: props/state 변경 시 컴포넌트 리렌더링 여부를 결정. false 반환 시 아래 메소드를 호출하지 않음

사용: 프로젝트 성능 최적화 시

```javascript
shouldComponentUpdate(nextProps, nextState) {
  return nextState.number % 10 !== 4 // 숫자의 마지막 자리가 4일 경우 리렌더링하지 않음.
}
```

3. render: 컴포넌트 리렌더링
4. getSnapshotBeforeUpdate: 컴포넌트 변화를 DOM 에 반영하기 직전 호출하는 메소드

사용: 업데하기 직전의 값을 참고하는 경우 (예: 스크롤바 위치 유지)

```javascript
getSnapshotBeforeUpdate(prevProps, prevState) {
  if (prevState.color !== this.state.color) {
    return this.myRef.style.color
  }
  return null
}
```

5. ComponentDidUpdate: 업데이트가 끝난 후 호출하는 메소드

```javascript
componentDidUpdate(prevProps, prevState, snapshot) {
  if (snapshot) ...
}
```

## 언마운트

DOM 으로부터 컴포넌트를 제거하는 것을 언마운트라 하며, 이 과정에서 호출하는 메소드는 다음과 같다.

1. componentWillUnmount: 컴포넌트 제거 직전 호출하는 메서드

## 주의사항

1. render 에서 state 를 변경하거나 브라우저에 접근해서는 안된다.
2. componentDidMount 에서 권장하는 작업

- DOM 정보를 가져오거나 변화를 줄 때
- 다른 라이브러리/프레임워크 함수 호출 시
- 이벤트 등록
- setTimeout, setInterval, 네트워크 요청 등과 같은 비동기 작업

참고:
리엑트를 다르는 기술 by 김민준님