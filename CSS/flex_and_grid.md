# Flex and Grid

## Flex

- `display: flex`: To sort/align items, you need a container to wrap them. Such as is a div styled with `display: flex`

  ````css
  .wrapper {
    display: flex;
  }
  ``` d

  ````

- `flex-direction: row`: If flex-direction is `row` (or main axis) which is by default, `justify-content` property aligns items horizontally, and `align-items` vertically.

  ```css
  .wrapper {
    display: flex;
    height: 100vh;
    flex-direction: row;
    justify-content: flex-start; /* Horizontal alignment */
    align-items: center; /* Vertical alignment */
  }
  ```

- `flex-direction: column`: If flex-direction is `column` (or cross axis), `align-items` property aligns items horizontally, and `justify-content` vertically.

  ```css
  .wrapper {
    display: flex;
    height: 100vh;
    flex-direction: column;
    justify-content: space-between; /* Vertical alignment */
    align-items: flex-start; /* Horizontal alignment */
  }
  ```

- `align-self`: If you want to align a single item(or wrapper's child), you can use `align-self` property.

  ```css
  .box {
    width: 100px;
    height: 100px;
    background-color: peru;
  }

  .box:nth-child(2) {
    align-self: center;
  }
  ```

- `order`: If you want to change the order of a single or a group of items or when you can't change the html, you can simply use `order` property. The `order` of each items in wrapper is 0 by default.

  ```css
  .box: nth-child(2) {
    order: 1; /* Move right by 1 */
  }
  ```

  When there are 3 items and 2th child `order` exceeds the total number, it is positioned rightmost.
  And 1th child which `order` is smaller than 2th child, relatively placed in front of the last item(2th child).

  ```css
  .box: nth-child(1) {
    order: 2; /* Move right by 2 --> in front of last item */
  }

  .box: nth-child(2) {
    order: 3; /* Move right by 3 --> rightmose */
  }
  ```

- `flex-wrap`: Flex basically tries to pack/squeeze all the items in one line. During this process, the originally specified width of an item is reduced.
  This property allows child items get properly arranged across multiple rows.

  ```css
  .wrapper {
    display: flex;
    flex-wrap: nowrap; /* wrap | wrap-reverse */
  }
  ```

  - `flex-flow`: The two properties flex-direction and flex-wrap are used so often together that the shorthand property flex-flow was created to combine them. This shorthand property accepts the value of one of the two properties separated by a space.

    ```css
    .wrapper {
      display: flex;
      flex-direction: column;
      flex-wrap: wrap;
    }

    to:

    .wrapper {
      display: flex;
      flex-flow: column wrap; /* shorthand of flex-direction and flex-wrap */
    }
    ```

  - `align-content`: Used to specify the height between rows when items are arranged across multiple rows.
    It has same values as `justify-content` property and `space-around` is the default value.

    ```css
    .wrapper {
      display: flex;
      flex-wrap: wrap;
      align-content: flex-start
    }
    ```

- `flex-shrink`: It determines how much the flex item will shrink relative to the rest of the flex items in the flex container when there isn’t enough space on the row.

  ```css
  .box:nth-child(2) {
    background-color: tomato;
    flex-shrink: 2;
  }
  ```

## Reference sites/docs

- https://flexboxfroggy.com/
- https://css-tricks.com/almanac/properties/f/flex-shrink/