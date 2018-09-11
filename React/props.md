# props

properties의 줄임마로서 컴포넌트 속성을 설정할 때 사용하는 요소이다.
부모 컴포넌트에서만 설정할 수 있다. 자식은 읽기전용으로만 사용할 수 있다.

## 렌더링

```javascript
import React, { Component } from 'react'

class Child extends Component {
  render() {
    return (
      <div>{this.props.name}</div>
    )
  }
}

export default Child
```

## 값 설정

```javascript
import React, { Component } from 'react'
import Child from './Child'

class Parent extends Component {
  render() {
    return (
      <Child name="React" />
      <Child name={3} /> // 문자열 종류 외의 값을 전달할 때에는 {} 로 감싸야 한다.
    )
  }
}

export default Parent
```

## 클래스 내부에 기본 값(defaultProps) 설정

```javascript
...
Child.defaultProps = {
  name: 'xxx'
}
```

## 클래스 외부에 기본 값(defaultProps) 설정

ES6 stage-2 transform-class-properties 문법 사용 가능 시

```javascript
class Child extends Component {
  static defaultProps = {
    name: 'xxx'
  }
  ...
}
```

## 검증(propTypes)

```javascript
import React, { Component } from 'react'
import PropTypes from 'prop-types'

class Child extends Component {
  ...
}

Child.propTypes = {
  name: PropTypes.string,
  age: PropTypes.number.isRequired // 필수값인 경우
}

export default Child
```

참고:
리엑트를 다르는 기술 by 김민준님