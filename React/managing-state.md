# State

작성일: 2018-02-09

```javascript
class Search extends Component {
  constructor(props) {
    super(props);

    this.state = {
      searchTerm: 'some statement..'
    };
  }

  onChangeHander(event) {
    this.setState({
      searchTerm: event.target.value
    });
  }

  render() {
    return (
      <div>
        <input
          onChange="this.onChangeHander"
          value={this.state.searchTerm}
          type="text"
          placeholder="Search"
        />
      </div>
    );
  }
}
```

* render, return 은 반드시 있어야 한다.
* eslint 의 react/prefer-stateless-function 오류를 피하려면 contructor(옵션), state 를 포함시켜야 한다.
* this.onChangeHander 의 this 와 클래스 인스턴스의 this 는 같지 않다. 따라서 bind 메소드를 이용하여 핸들러에게 this(클래스 인스턴스) 를 알려주어야 한다.

```javascript
onChange(this.onChangeHandler.bind(this));
```

* 하지만, bind 는 비용이 꽤 높은 함수이며, render 는 자주 호출되기 때문에 생성자에서 한 번 작성하는 것이 비용 효율적이다.

```javascript
contructor(props) {
  ...

  this.onChangeHandler = this.onChangeHandler.bind(this);
}
```

## bind 의 대안([transform-class-properties])

## .babelrc

```json
"plugins": [
    "babel-plugin-transform-class-properties"
  ]
```

### .eslintrc.json

```json
"parser": "babel-eslint"
```

* 위와 같이 했다면 아래와 같이 바꿀 수 있다.

```javascript
class Search extends Component {
  // constructor(props) {
  //   super(props);

  //   this.state = {
  //     searchTerm: ''
  //   };

  //   this.onChageHandler = this.onChangeHander.bind(this);
  // }

  state = {
    searchTerm: ''
  };

  // onChangeHandler(event) {
  onChangeHandler = event => {
    this.setState({
      searchTerm: event.target.value
    });
  };

  render() {
    return (
      <div>
        <input
          onChange="this.onChangeHandler"
          value={this.state.searchTerm}
          type="text"
          placeholder="Search"
        />
      </div>
    );
  }
}
```

## 참고

[Frontend Master](https://frontendmasters.com/courses/react)

[transform-class-properties]: https://medium.com/@joshblack/writing-a-react-component-in-es2015-a0b27e1ed50a
