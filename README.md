# <h1 align="center" style="font-weight: bold; margin-top: 20px; margin-bottom: 20px;">Demo AntDesign NextJS</h1>
  
<h3 align="center" style="font-weight: bold; margin-top: 20px; margin-bottom: 20px;">Guide setup AntDesign for Nextjs</h3>
  
<p align="center">
  <a href="https://github.com/phungnlg/demo-nextjs-ant-design"><img alt="GitHub Workflow Status" src="https://img.shields.io/github/workflow/status/phungnlg/demo-nextjs-ant-design/build"></a>
  <a href="#last-commit"><img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/phungnlg/demo-nextjs-ant-design"></a>
  <a href="#node-current"><img alt="node-current" src="https://img.shields.io/node/v/next"></a>
  <a href="#license"><img alt="GitHub" src="https://img.shields.io/github/license/phungnlg/demo-nextjs-ant-design"></a>
</p>
  
<p align="center">
  <a href="#getting-started">Getting Started</a> •
  <a href="#documentation">Documentation</a> •
  <a href="#support">Need Help?</a> •
  <a href="#about">About</a> •
  <a href="#license">License</a>
</p>
  
<br/>

## Introduction

1. You want integrated `Ant Design` to your `NextJS project`.
2. This project will help you understand and how setup `Ant Design` - `Ant Design charts` and `styled-components`
  
**Demo AntDesign NextJS** is a small project for basic setup `Ant Design` for NextJS.

<br/>
  
## Key Features

- **[Next JS](https://nextjs.org/docs/getting-started)**
- **[Ant Design](https://ant.design/)**
- **[Charts Ant Design](https://charts.ant.design/)**
- **[styled-components](https://github.com/styled-components/styled-components)**

<br/>
  
## Usage

```sh
# install libs
yarn
# run dev
yarn dev
# generate
yarn export
```

<br/>
  
## Getting Started

### **Structure**

```js
.
├── 📁 assets
│   ├── 📁 styles
│   │   └── 📝 globals.scss
│   └── 📁 images
├── 📁 components
│   ├── 📁 common
│   └── 📁 partials
├── 📁 layouts
│   ├── 📁 components
│   └── 📝 default.jsx
├── 📁 pages
│   ├── 📝 _app.jsx
│   ├── 📝 _document.jsx
│   ├── 📝 index.jsx
│   ├── 📝 chart.jsx
│   └── 📝 user.jsx
├── 📁 public
├── 📝 .env
├── 📝 .env.development
├── 📝 .env.production
├── 📝 jsconfig.js
├── 📝 next.config.js
└── 📝 README.md
```

<br/>

### **Prerequisites**

- [Node.js](https://nodejs.org/en)
- [yarn](https://yarnpkg.com/getting-started/install)
  
## Documentation

### **Configuration**

- Install lib

```bash
yarn add antd ant-design-pro @ant-design/charts styled-components babel-plugin-styled-components
```

### **API**

1. Setup [styled-components](https://github.com/styled-components/styled-components)

- Update `/.babelrc`

```json
{
  "presets": ["next/babel"],
  "plugins": [["styled-components", { "ssr": true }]]
}
```

- Update `/pages/_document.js`

```jsx
import Document from 'next/document'
import { ServerStyleSheet } from 'styled-components'

export default class MyDocument extends Document {
  static async getInitialProps(ctx) {
    const sheet = new ServerStyleSheet()
    const originalRenderPage = ctx.renderPage

    try {
      ctx.renderPage = () =>
        originalRenderPage({
          enhanceApp: (App) => (props) =>
            sheet.collectStyles(<App {...props} />),
        })

      const initialProps = await Document.getInitialProps(ctx)
      return {
        ...initialProps,
        styles: (
          <>
            {initialProps.styles}
            {sheet.getStyleElement()}
          </>
        ),
      }
    } finally {
      sheet.seal()
    }
  }
}
```

2. Setup Ant Design

- import css in `_app.jsx`

```jsx
import 'antd/dist/antd.css'
```

3. **Example using [Card - Ant Design](https://ant.design/components/card/)**

```jsx
import { Card } from 'antd'

export const CardStyled = props => {
  const bodyStyle = {
    padding: '20px 24px 8px'
  }
  if (props.type === 'stats') {
    bodyStyle.padding = '20px 16px 16px'
  }
  return <Card bodyStyle={bodyStyle} bordered={false} {...props} />
}
```

4. **Example using [Charts - Ant Design/](https://charts.ant.design/)**

```jsx
// You need using dynamic import, because this lib not support SSR
import dynamic from 'next/dynamic'
const Line = dynamic(
  () => import("@ant-design/charts").then((mod) => mod.Line),
  { ssr: false }
)

const ChartsPage = () => {
  const data = [
    { year: '1991', value: 3 },
    { year: '1992', value: 4 },
    { year: '1993', value: 3.5 },
    { year: '1994', value: 5 },
    { year: '1995', value: 4.9 },
    { year: '1996', value: 6 },
    { year: '1997', value: 7 },
    { year: '1998', value: 9 },
    { year: '1999', value: 13 },
  ];
  const config = {
    data,
    height: 400,
    xField: 'year',
    yField: 'value',
    point: {
      size: 5,
      shape: 'diamond',
    },
  }

  return (
    <Line {...config} />
  )
}

export default ChartsPage
```

### **Performance and testing**

Any of testing activities and reports goes here.

<br/>

## Support
  
### **Get Help**
  
**You have a question or problem wasn't solved?** No worries! Just open up a new issue in the `GitHub issue tracker`. Please provide all information to reproduce your problem. If you don't have a GitHub account, you can [contact](#contact) me directly.
  
<br/>
  
## About

### **Known Issues**
  
 - none (that are reported)

<br/>
  
### **Contact**
  
If you haven't done so already, please check out [Get Help](#get-help) for the fastest possible help on your issue. Alternatively you can get in touch with me by:

- Email: phungnlg0810@gmail.com
  
<br/>

## License

This project is proudly licensed under the [MIT license][git-license].

<!-- LINKS -->
<!-- in-line references: websites -->
[phungnlg.github.io]:https://phungnlg.github.io
[react-bootstrap]:https://react-bootstrap.github.io/

<!-- in-line references to github -->

[git-profile]:https://github.com/phungnlg
[git-readme]:README.md
[git-license]:LICENSE.md