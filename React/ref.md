# ref

DOM에 직접적인 접근을 할 때 사용

## 필요한 상황

1. input/textarea 등에 포커스를 해야 하는 경우
2. 특정 DOM의 크기를 알아야 할 때
3. 특정 DOM의 스크롤 위치를 가져오거나 설정할 때
4. 외부 라이브러리(플레이어, 차트, 캐로셀 등)을 사용할 때

## 권장되지 않음

1. 서로 다른 컴포넌트 간 데이터 교류

## input 사용예시

```javascript
<input ref={(ref) => {this.input=ref}} />
this.input.focus()
```

## 컴포넌트 사용예시

MyComponent 내부의 메서드 및 멤버 변수 접근 가능

```javascript
// #1
<MyComponent ref={(ref) => {this.MyComponent=ref}} />

// #2
<ScrollBox ref={(ref) => {this.scrollBox=ref}} />
<button onClick={() => this.scrollBox.scrollToBottom()}>
```

