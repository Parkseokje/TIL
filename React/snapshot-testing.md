# Snapshot Testing (Feat. Jest)

특정 컴포넌트에 대한 스냅샷을 생성하여, 이전 컴퍼넌트와 달라진 부분이 있는지 체크한다. API JSON 에 대해서도 적용할 수 있다.

* jest 설치 :
  `yarn add jest --dev`
* .babelrc 수정

```javascript
...
"env": {
  "test": {
    "plugins": [
      "transform-es2015-modules-commonjs"
    ]
  }
}
```

* .elintrc.json 수정

```javascript
...
"env": {
  "es6": true,
  "browser": true,
  "node": true,
  "jest": true
}
```

* 루트에 `__tests__` 폴더 생성 (Airbnb rule 을 적용중인 경우만 해당)
* `__tests__` 안에 `[컴포넌트명].spec.jsx` 생성
* 아래 코드 입력

```javascript
import React from 'react';
import renderer from 'react-test-renderer';
import Search from '../js/Search'; // 스냅샷을 찍을 컴퍼넌트

test('Search 컴퍼넌트가 올바르게 렌더링 되는지 확인한다.', () => {
  const component = renderer.create(<Search />);
  const tree = component.toJSON();

  expect(tree).toMatchSnapshot();
});
```

* test 실행 : `NODE_ENV=test ./node_modules/.bin/jest`
* 최초 실행시에는 스냅샷만 저장하므로 테스트가 성공한다. 아래 경로에 스냅샷이 생성되었다.

```
__tests__
  __snapshots__
    Search.spec.jsx.snap
```

* Search.jsx 컴포넌트를 수정한 다음 다시 테스트를 해보자.
* test 실행 : `NODE_ENV=test ./node_modules/.bin/jest`

```
Received value does not match stored snapshot 1.

- svideo
+ video
```

* svideo 를 video 로 변경하였다. 이전 스냅샷과 다르므로 테스트가 **실패**했다.
* 만약 현재 상태로 스냅샷을 변경하려면 아래와 같이 해보자.

```
NODE_ENV=test ./node_modules/.bin/jest -u
```

* 스냅샷이 갱신되며, -u 를 제외하고 다시 테스트 해보면 **성공**하는 것을 볼 수 있다.

## 참고

[Frontend Masters](https://frontendmasters.com/courses)
