# HMR (Hot Module Replacement)

HMR 은 특정 코드 변경 시, 브라우저 새로고침 없이 해당 부분만 리로드하는 것을 의미한다.
개발모드에서만 사용된다.

코드가 변경 후 저장을 누르더라도, state 를 유지시켜주므로, 수정한 결과가 표시되기까지 거쳐야 하는 여러 과정들을 생략할 수가 있다. 이로 인해 개발 시 생산성은 높이고 불필요한 대기시간을 없앨 수 있게 된다.

예를들어, 검색로직에서 필터조건을 하나 추가했다고 가정해보자. 수정된 로직을 검증하려면 일반적으로 다음 과정들을 거쳐야 한다.

_코드수정 &rarr; 저장 &rarr; 새로고침 &rarr; 검색어 입력 &rarr; 검색버튼 클릭 &rarr; API 호출 &rarr; 데이터표시_

HMR 을 이용하면, 4 단계를 생략하고 바로 필터 적용여부를 확인할 수 있다.

_코드수정 &rarr; 저장 &rarr; 데이터표시_

### 1. 환경설정

**.babelrc**

```javascript
...
  "plugins": [
    "react-hot-loader/babel",
```

**webpack.config.js**

```javascript
  context: __dirname,
  entry: [ // 아래 순서가 중요하다.
    'react-hot-loader/patch',
    'webpack-dev-server/client?http://localhost:8080',
    'webpack/hot/only-dev-server',
    './js/ClientApp.jsx' // 루트 컴포넌트가 렌더링되는 부분
  ],
  ...
  output: {
    ...
    publicPath: '/public/'
  },
  devServer: {
    hot: true,
    publicPath: '/public/',
    ...
  },
  ...
  plugins: [
    new webpack.HotModuleReplacementPlugin(),
    new webpack.NamedModulesPlugin()
  ],
  ...
```

### 2. App.jsx 에 HMR 적용

루트 컴포넌트인 App 을 별도의 파일로 분리하고, 불러들인다.

**Client.jsx**

```javascript
import React from 'react';
import { render } from 'react-dom';
import App from './App';

const renderApp = () => {
  render(<App />, document.getElementById('app'));
};
renderApp();

// App 내용 수정 시 renderApp 이 수행된다.
if (module.hot) {
  module.hot.accept('./App', () => {
    renderApp();
  });
}
```

### 3. 서버를 재시작한다.

테스트하는 방법은,

* 특정 state(예: 검색어를 입력)를 변경
* 텍스트나 일부 로직을 수정한 뒤 저장을 누른다.
* 브라우저 새로고침 없이 검색어가 결과에 반영되는지 확인

**HMR 상태에서 Search.jsx 수정했을 때 console 로그**

```
[WDS] App hot update...
[HMR] Checking for updates on the server...
[HMR] Updated modules:
[HMR]  - ./js/Search.jsx
[HMR]  - ./js/App.jsx
[HMR] App is up to date.
```
