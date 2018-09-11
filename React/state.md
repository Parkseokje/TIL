# state

컴포넌트 내부에서 읽고 업데이트할 수 있는 값이다.
업데이트를 위해서는 반드시 this.setState 메서드를 사용한다.

## 렌더링

```javascript
import React, { Component } from 'react'

class Child extends Component {
  state = {
    name: 'xxx'
  }

  render() {
    return (
      <div>{this.state.name}</div>
    )
  }
}

export default Child
```

## 초기값 설정

```javascript
import React, { Component } from 'react'
import Child from './Child'

class Parent extends Component {
  // 방법 1
  constructor(props) {
    super(props)
    this.state = {
      name: 'xxx'
    }
  }
  
  // 방법 2
  state = {
    name: 'xxx'
  }  

  render() {
    ...
  }
}

export default Parent
```

## 업데이트(setState)

```javascript
import React, { Component } from 'react'

class Child extends Component {
  state = {
    name: 'xxx'
  }

  render() {
    return (
      <div>
        <button onClick={() => {
          this.setState({
            name: 'yyy'
          })
        }}>이름변경</button>
      </div>
    )
  }
}

export default Child
```

## 잘못된 업데이트 방법

```javascript
this.state.number = this.state.number + 1
this.state.someArray.push(3)
this.state.someObject.value = 3
```

참고:
리엑트를 다르는 기술 by 김민준님