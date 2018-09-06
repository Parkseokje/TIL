# Parcel Experiment

Setting up a professional React project with Parcel as a code bundler.

## Feature

- React
- ES6 with Babel
- SCSS
- CSS Modules
- Typography.js
- Build for production

## 프로젝트 초기화

```
yarn init
```

## 설치

```
yarn global add parcel-bundler
yarn add react react-dom
yarn add babel-preset-env babel-preset-react --dev
yarn add postcss-modules
yarn global add node-sass
yarn add autoprefixer
yarn add typography
```

## package.json

```json
...
  "scripts": {
    "start": "parcel index.html",
    "build": "parcel build index.html -d build --public-url ./"
  }
```

## index.html 작성

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Parcel Experiments</title>
</head>

<body>
  <div id="app"></div>
  <script src="./index.js"></script>
</body>

</html>
```

## src/App.js 작성

```javascript
import React from 'react'

export default () => <div>lalala</div>
```

## index.js 작성

```javascript
import React from 'react'
import ReactDOM from 'react-dom'
import App from './src/App'

ReactDOM.render(<App />, document.getElementById('app'))
```

## Parcel 실행

```
parcel index.html
```

## .babelrc 작성

```json
{
  "presets": ["env", "react"]
}
```

## .postcssrc 작성

```json
{
  "modules": true,
  "plugins": {
    "autoprefixer": {
      "browsers": ["> 1%", "Last 2 versions", "IE 10"]
    }
  }
}
```

## typography.js 작성

```javascript
import Typography from 'typography'

const typography = new Typography({
  baseFontSize: '16px',
  baseLineHeight: 1.666,
  googleFonts: [
    {
      name: 'Montserrat',
      styles: ['700']
    },
    {
      name: 'Open Sans',
      styles: ['400']
    }
  ],
  headerFontFamily: ['Montserrat', 'Helvetica Neue', 'Open Sans'],
  bodyFontFamily: ['Open Sans', 'sans-serif']
})

typography.injectStyles()

export default typography
```

## 참고

- https://parceljs.org/
- https://youtu.be/Xe3aQx9nx4Y
- https://postcss.org/
- https://kyleamathews.github.io/typography.js/
