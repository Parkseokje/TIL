# event

리액트의 이벤트 시스템은 웹브라우저의 HTML 이벤트와 사용법이 유사하다.

```javascript
<button onClick={() => {
  this.setState({
    number: this.state.number + 1
  })
}}>
```

## 주의사항

1. 이벤트 이름은 camelCase 로 작성
2. 이벤트 핸들러에 실행할 코드를 입력하는 것이 아니라, 함수 형태의 객체를 작성
3. DOM 요소에만 이벤트 설정 가능 (아래 불가)

```javascript
<MyComponent onClick={doSomething} /> // (X)

<div onClick={this.props.onClick}>...</div> // (O)
```

## onChange 이벤트 핸들링

아래에서 e(vent) 객체는 **SyntheticEvent** 로서 웹브라우저 네이티브 이벤트를 감싼 객체이다.
네이트비 이벤트와 인터페이스가 같다.

```javascript
<input
  type="text"
  name="message"
  placeholder="메시지 입력"
  onChange={e => console.log(e.targe.value)}
/>
```

## 함수를 미리 준비하여 전달하는 방법 : 임의메서드

```javascript
class EventPractice extends Component {
  constructor() {
    this.handleChange = this.handleChange.bind(this)
  }

  state = { ... }

  handleChange(e) {
    this.setState({
      message: e.target.value
    })
  }

  render() {
    return (
      <div>
        <input
          type="text"
          name="message"
          placeholder="메시지 입력"
          onChange={this.handleChange}
        />
      </div>
    )
  }
}
```

## Property Initializer Syntax을 사용한 임의메서드 작성

```javascript
class EventPractice extends Component {
  state = { ... }

  handleChange = (e) => {
    this.setState({
      message: e.target.value
    })
  }

  render() {
    return (
      <div>
        <input
          type="text"
          name="message"
          placeholder="메시지 입력"
          onChange={this.handleChange}
        />
      </div>
    )
  }
}
```

## 여러개의 input 이벤트 핸들링

```javascript
class EventPractice extends Component {
  state = { ... }

  handleChange = (e) => {
    this.setState({
      [e.target.name]: e.target.value
    })
  }

  render() {
    return (
      <div>
        <input
          type="text"
          name="message"
          placeholder="메시지 입력"
          onChange={this.handleChange}
        />
      <div>
        <input
          type="text"
          name="message2"
          placeholder="메시지 입력2"
          onChange={this.handleChange}
        />
      </div>
    )
  }
}
```

참고:
리엑트를 다르는 기술 by 김민준님