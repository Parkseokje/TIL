# Flexbox

Flex 의 기본 사용법에 대해 설명한다.

## index.html

```html
<div class="container">
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
</div>
```

## Flexbox Container 요소

```css
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100vh;
}
```

## Flexbox Item 요소

⭐️ 부모 div 가 반드시 Flexbox 컨테이너여야 한다.

```css
.item {
  width: 300px;
  height: 300px;
  background-color: blue;
  border: 1px solid white;  
}
```

## flex-direction 속성

- 기본값은 row.
- row 일 경우 main-axis 는 수평 cross-axis 는 수직이다.
- row 일 경우 main-axis 는 수평 cross-axis 는 수직이다.
- column 일 경우 main, cross axis 는 각각 반대 방향으로 적용.

## justify-content 속성

- main axis

## align-items 속성

- cross axis
- ⭐️ 높이(height)가 item 의 높이보다 커야 확인할 수 있다.

## flex-wrap 속성

item 사이에 더이상 공간이 없을 때 flexbox 가 해야하는 행동을 정의.

- wrap: item 이 줄어들지 않도록 한다.
- nowrap

```css
.container {
  ...
  flex-wrap: wrap;
}
```

## align-self 속성

특정 item 의 cross-axis 속성을 변경하고자 하는 경우 사용.

```css
.item:first-child {
  align-self: flex-end;
}
```