# Class

작성일: 2018-02-09

```javascript
class Person {
  constructor(name) {
    this._name = name;
  }

  sayHi() {
    console.log(`Hi, ${this._name}!`);
  }
}

const me = new Person('Park');
me.sayHi();

console.log(me instanceof Person);
```

## contructor

* 인스턴스의 생성 및 초기화
* 클래스 내 한개만 존재해야 함
* 생략 가능

## 멤버변수

* 클래스 바디에는 메소드만 포함 가능
* contructor 내부에서 멤버 변수의 선언 및 초기화는 가능

## this

* 클래스의 인스턴스이다.
* public 이며, 외부에서 참조 가능하다.

## 호이스팅(Hoisting)

```javascript
const foo = new Foo();
class foo {}
```

* 클래스 선언문 이전에 클래스를 참조하면 참조 오류 발생

## getter

```javascript
class Foo {
  constructor(arr = []) {
    this._arr = arr;
  }

  get firstEl() {
    return this._arr.length ? this._arr[0] : null;
  }
}

const foo = new Foo([1, 2]);
console.log(foo.firstEl); // 1
```

* 멤버변수처럼 사용된다.
* getter 는 반드시 무언가를 반환해야 한다.

## setter

```javascript
class Foo {
  ...
  set firstEl(el) {
    this._arr = [el, ...this_arr] // [100, 1, 2]
  }
}

foo.firstEl = 100;
console.log(foo.firstEl); // 100
```

## 정적 메소드

```javascript
class Foo {
  ...

  static staticMethod() {
    return 'Hi'
  }
}
```

* 클래스의 인스턴스화 없이 호출한다.
* 클래스의 인스턴스로 호출할 수 없다.
* ex) Math.abs(-1)

## 클래스 상속(Inheritance)

**Base Class**

```javascript
Class BaseClass {
  constructor(weight) {
    this._weight = weight;
  }

  weight() {
    console.log(this._weight);
  }

  eat() {
    console.log('Animal eat.');
  }
}
```

**Sub Class**

```javascript
class Human extends Animal {
  constructor(weight, language) {
    super(weight);
    this._language = language;
  }

  // 메소드 오버라이드: 상위 클래스의 메소드를 하위 클래스가 재정의함.
  eat() {
    console.log('Human eat.');
  }

  speak() {
    console.log(`speaking language is ${language}.`);
  }
}

const korean = new Human(45, 'Korean');
korean.weight(); // 45
korean.eat(); // Human speak Korean
korean.speak(); // speaking language is Korean.

console.log(Korea instance of Human); // true
console.log(Korea instance of Animal); // true
```

* super 키워드는 부모 클래스의 contructor 를 호출한다.
* 자식 클래스에서 super()를 호출하지 않으면 참조 오류가 발생한다.
* super()를 호출하기 이전에는 this 를 참조할 수 없다.
* 부모 클래스의 정적 메소드도 상속된다.
* 자식 클래스의 일반 메소드에서는 super 를 사용하여 정적 메소드를 호출할 수 없다.
* 오버로딩(메소드 확장)은 지원하지 않으나 arguments 객체를 활용할 수는 있다.

## 기타

* private, public, protected 와 같은 접근 제한자를 지원하지 않는다.

참고

[poiemaweb](http://poiemaweb.com/es6-class)
