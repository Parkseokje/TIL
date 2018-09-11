# map

배열 객체의 내장 함수인 map 함수를 사용하여 반복되는 컴포넌트를 렌더링하는 작업을 구현해본다.

## 예제코드

```javascript
import React, { Component } from 'react'

class IterationSample extends Component {
  render() {
    const names = ['참외', '복숭아', '수박']
    const nameList = names.map(name => <li>{name}</li>)

    return <ul>{nameList}</ul>
  }
}
```

## Key

컴포넌트 배열을 렌더링했을 때 어떤 원소에 변동이 있었는지 추척하기 위한 용도로 사용한다.

## 예제코드

```javascript
const nameList = names.map((name, index) => <li key={index}>{name}</li>)
```

## state 변경 시 push 혹은 concat ?

state를 변경하는 경우 기본 배열 자체가 변경되면 안된다.
push 를 사용할 경우 자동으로 리렌더링을 트리거하지 못하게 된다.

```javascript
this.state.names.push('newName') // (X)
this.state.names.concat('newName') // (O)
```

## state 에서의 filter 사용

```javascript
this.setState({
  names: this.state.names.filter((item, i) => i !== index)
}
```
