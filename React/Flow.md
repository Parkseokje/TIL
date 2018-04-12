# Flow

_Static type checking is the process of verifying the type safety of a program based on analysis of a program's text (source code). If a program passes a static type checker, then the program is guaranteed to satisfy some set of type safety properties for all possible inputs. - [en.wikipedia.org](https://en.wikipedia.org/wiki/Type_system#Static_type_checking)_

_Flow is a static type checker for JavaScript. - [flow](https://flow.org/en/)_

## 정적 타입 검사기를 사용하면 무엇이 좋을까?

* 가독성이 좋은 코드의 작성 가능
* 분석하기 좋은 코드의 작성 가능
* 신뢰할 수 있는 리펙터링 허용
* 더 좋은 IDE 지원 허용
* 잠재적인 에러의 사전 식별 가능

## 특징
* 리엑트에 빌트인되어 있다.
* 점진적으로 적용할 수 있다.

## 설치

```
yarn add --dev flow-bin
```

## 초기화

```
yarn (run) flow init
```

## Third Party 라이브러리들을 Flow 에서 인식할 수 있도록 정의

```
> yarn global add flow-typed
> flow-typed install
```

현재 프로젝트의 flow-typed 폴더에서 확인할 수 있다.

## styled-component 에 대한 예외처리
루트에 **.flowconfig** 파일 생성

```
[ignore]
<PROJECT_ROOT>/node_modules/styled-components/*

[libs]
styled-components
```

## Flow 적용
적용하려는 jsx 파일 상단에
```javascript
// @flow
```

## eslint rule 수정
**.eslintrc.json
```json
"extends": [
  "plugin:flowtype/recommended"
],
"plugins": [
  "flowtype"
]
```

## 특정 라인에 대하여 Flow 오류를 무시하려면
```javascript
// $FlowFixeMe
import styled from 'styled-components';
```

## 실행

```
yarn (run) flow
```

## eslint

## 참고

* https://reactjs.org/docs/static-type-checking.html
* http://ahnheejong.name/articles/types-basic-concepts/
* https://djcordhose.github.io/flow-vs-typescript/2016_hhjs.html#
