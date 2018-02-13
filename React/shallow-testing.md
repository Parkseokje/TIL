# Shallow Testing (Feat. Jest)

Snapshot Testing 과 유사한 기능이다. 다른점은, 하위 컴퍼넌트 변경여부까지는 테스트 하지 않는다는 점이다. **snapshot-testing** 의 경우 하위 컴퍼넌트 변경 시 부모 컴퍼넌트도 수정된 것으로 간주하지만, **shallow-testing** 의 경우 수정된 컴퍼넌트만 검사하므로, 부모 컴퍼넌트의 스냅샷 비교시 하위 컴퍼넌트까지 검사하지 않는다.

* enzyme 설치: `yarn add enzyme --dev`
* package.json 수정

```javascript
...
"jest": {
    "snapshotSerializers": [
      "jest-serializer-enzyme"
    ]
  },
```

```javascript
import React from 'react';
// import renderer from 'react-test-renderer'; // enzyme 과 함께 사용할 수 없다.
import { Shallow } from 'enzyme';
import Search from '../js/Search'; // 스냅샷을 찍을 컴퍼넌트

test('Search 컴퍼넌트가 올바르게 렌더링 되는지 확인한다.', () => {
  // const component = renderer.create(<Search />);
  const component = Shallow(<Search />);
  // const tree = component.toJSON();

  expect(tree).toMatchSnapshot();
});
```

* test 실행 및 업데이트 : `NODE_ENV=test ./node_modules/.bin/jest -u`
* 스냅샷의 달라진 점은, 하위 컴퍼넌트가 html 로 렌더되지 않은 상태 그대로라는 것이다.
* **snapshot-testing**

```html
<div>
    <div
      className="sc-bdVaJa jfzRHo"
    >
```

* **shallow-testing**

```html
<div>
  <ShowCard />
```

* ShowCard.jsx (자식 컴포넌트) 를 수정한 다음 다시 테스트를 해보자.
* test 실행 : `NODE_ENV=test ./node_modules/.bin/jest`
* **성공**하는 것을 볼 수 있다.

## 참고

[Frontend Masters](https://frontendmasters.com/courses)
