# Component Length Testing (Feat. Jest)

특정 컴포넌트의 개수를 테스트하는 코드를 작성해보자.

```javascript
import React from 'react';
import { shallow } from 'enzyme';
import preload from '../data.json'; // shows 개수만큼 컴퍼넌트가 생성된다.
import Search from '../js/Search'; // 부모 컴포넌트
import ShowCard from '../js/ShowCard'; // 자식 컴포넌트

test('올바른 개수의 ShowCard가 렌더되어야 한다.', () => {
  const component = shallow(<Search />);

  // preload.shows의 개수와
  // Search의 자식 컴포넌트인 ShowCard의 개수를 비교한다.
  expect(preload.shows.length).toEqual(component.find(ShowCard).length);
});
```

* 테스트 실행 : `yarn test`

> 팁 1. `test` 는 `it` 으로 대체해도 된다.

```
test('some suite', () => {})
it('some suite', () => {})
```

> 팀 2. 여러개의 `test`를 `describe` 를 사용하여 그룹핑할 수 있다. 이렇게 하면, 그룹별로 오류/성공 메세지를 확인할 수 있다.

```javascript
describe('Search 가 올바르게 렌더되어야 한다.', () => {
  test('suite 1', () => {});
  test('suite 2', () => {});
  ...
});
```

> 팁 3. 테스트를 원하지 않는 경우 `xtest` 라고 수정한다.

```javascript
describe('Search', () => { // xdescribe 일 경우 이 그룹의 모든 테스트를 수행하지 않음
  test('suite 1', () => {});
  xtest('suite 2', () => {}); // 이 테스트는 수행하지 않는다.
  ...
});
```

> 팁 4. `expect(테스트할 대상).toEqual(기대하는 결과)`
> 이번 예제의 경우 ShowCard 의 개수가 **테스트할 대상**이며,
> preload.shows 의 개수가 **기대하는 결과**이다. 이렇게 하는 이유는 좀 더 의미있는(시맨틱) 실패 메시지를 표시하기 위함이다. 따라서 아래와 같이 작성하는 것이 좋다.

```javascript
// expect(preload.shows.length).toEqual(component.find(ShowCard).length);
expect(component.find(ShowCard).length).toEqual(preload.shows.length);
```

> 팁 5. 컴포넌트의 특정 자식 또는 태그를 찾고자 하는 경우
> `find(컴포넌트 또는 CSS Selector)`

```javascript
const component = shallow(<Search />);
component.find(ShowCard); // ShowCard 컴포넌트를 찾는다.
component.find(input); // Search 컴포넌트의 input 을 찾는다.
```
