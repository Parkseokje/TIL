# Component Manipulating Testing (Feat. Jest)

컴포넌트의 입력값을 전송하는 테스트를 작성해보자.

```javascript
test('Search 컴포넌트는 검색어에 따라 올바른 개수의 ShowCard 를 렌더해야 한다.', () => {
  const component = shallow(<Search />);
  const searchWord = 'black'; // 검색어

  // 제목과 설명이 searchWord를 포함하는 show
  // 의 개수를 구한다.
  const showCount = preload.shows.filter(
    show =>
      `${show.title} ${show.description}`
        .toUpperCase()
        .indexOf(searchWord.toUpperCase()) >= 0
  ).length;

  // input 의 change 이벤트를 발생시킨다.
  component.find('input').simulate('change', {
    target: {
      value: searchWord
    }
  });

  expect(component.find(ShowCard).length).toEqual(showCount);
});
```

## 참고

[enzyme](https://github.com/airbnb/enzyme)
