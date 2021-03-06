# styled-svg
Generate [styled-components 💅](https://www.styled-components.com/) from SVG files  
  
[![Build Status](https://travis-ci.org/Scout24-CH/styled-svg.svg?branch=master)](https://travis-ci.org/Scout24-CH/styled-svg)
[![Known Vulnerabilities](https://snyk.io/test/github/scout24-ch/styled-svg/badge.svg)](https://snyk.io/test/github/scout24-ch/styled-svg)

## What's this?
This utility generates React components, using the `styled.svg` function. Just drop the .svg somewhere in the project, run the tool and start using your svg files as [inline svg](http://caniuse.com/#feat=svg-html5) with all React and `styled-components` beauty. As a bonus, all svg files are optimized, using the awesome [svgo](https://github.com/svg/svgo) library.

### How it looks like

- Input [warning.svg](./src/test-images/warning.svg)
- Command `npx styled-svg **/*.svg --size=small:18x18 --size=medium:24x24 --size=large:36x36`
- Output
  - Styled component: [Warning.js](./src/test-images/Warning.js)
  - Tests [Warning.test.js](./src/test-images/Warning.js)

### Usage of the generated component
```js
import React from 'react'
import Warning from './Warning'

const ComponentWithImage = props => (
  <div>
    {props.children}
    <Warning size='medium' fillColor='red' />
  </div>
)

export default ComponentWithImage
```

### Props of the generated components
name | type | default | description
:--- | :--- | :--- | :---
fillColor | `String` / `null` | `null` | override fill color of paths and other elements
fillColorRule | `String` | `'&&& path, &&& use, &&& g'` | rule for selecting elements to colorize, you only need to change this, for complex svg structures.
size | `String` / `null` / `Object` | `null` | one of the sizes keys, to set the size, or an object `{ width, height }`
sizes | `Object` | `{}` | Override  possible sizes, example below (by default these are generated with the --size option, so you probably won't need this) 

#### sizes prop example
```js
const sizes = {
  small: { width: 18, height: 18 },
  medium: { width: 24, height: 24 },
  large: { width: 36, height: 36 }
}
```

### Overriding styles
As the components are just regular styled-components, overriding styles is easy. Note if you just want to change colors for hover and other state-changes, you can use the `fillColor` prop of the generated components.
```js
import React from 'react'
import styled from 'styled-components'
import Warning from './Warning'

const CustomizedWarning = styled(Warning)`
  width: 100%;
  border-radius: 3px;
`
```

## Usage
### npm scripts usage (recommended)

Install the dependency
```bash
npm i --save-dev styled-svg
```

Create a npm script entry in your package.json
```js
{
  //...
  "scripts": {
    "svg": "styled-svg src/**/*.svg --size=small:18x18 --size=medium:24x24"
  },
  //...
}
```
Then run `npm run svg` at any time to generate Components

### JS usage
Install the dependency
```bash
npm i --save-dev styled-svg
```

JS example
```js
const convert = require('styled-svg')

// options have the same defaults as the command line usage
const options = {
  clean: true,
  dryRun: false
  noTests: false,
  outputDir: './output',
  templatesDir: : './templates',
  testDir: './output',
  size: [
    'small:18x18',
    'medium:24x24'
  ]
}
const files = [
  'path/to/file/a.svg',
  'path/to/file/b.svg',
  'path/to/file/c.svg'
]

// returns a promise that resolves to an array of results
convert(files, options)
```

### Command line usage
Install the package globally
```bash
npm i -g styled-svg
```

Run it in any directory
```bash
styled-svg **/*.svg
```

## Changelog
[CHANGELOG](CHANGELOG.md)


## Known issues / unimplemented features
- Improve test coverage
- Make it usable in JS with specifying svg strings directly, not only file paths

## Licence 
[MIT](LICENSE.md)

## Credits
- Thanks [svg2react](https://www.npmjs.com/package/svg2react) for some inspiration how to handle
attributes
