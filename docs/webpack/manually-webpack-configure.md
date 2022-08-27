---
title:  Webpack Config
sidebar_label: Webpack Config
---

# Webpack Config

```js
my-website
├── dist
│   ├── index.html
│   ├── main.js
│ 
├── src
│   ├──index.js
│   
│   
├──package.js
├──webpack.config.js
```

First create 2 folder dist and src, two js file should contain in src folder

other.js
```js
export function other(){
    return "i am from other"
}
```

**other.js** file imported in **index.js** file then this **index.js** file will be entry file in **webpack.config.js**

index.js
```js
import {other} from './other'
console.warn(other());
```

To get **package.json** we have to run below command
```js
npm init
```

Now discuss about webpack
```js
const path = require('path')

module.exports = {
    mode: "production",
    entry:'./src/index.js',
    output:{
        path: path.resolve(__dirname,'dist'),
        filename:"main.js"
    },
}

```
production mode make **minified** js
<code>mode:"production, development"</code>

- **entry** means that which file should entry file. In our case **index.js** will be the entry file and all other file should imported in app.js file
- **output** after run <code>npm run build</code> entry file will be **minified** js file in mentions <code>path.resolve(__dirname,'dist')</code> directory path.

### devServer

devServer means that, if we change something on html file then it will automatically build

first run this command
```js
npm i webpack-dev-server --save-dev
```
after run this command we will see below code in **package.json** file
```js
 "devDependencies": {
    "webpack-dev-server": "^4.10.0"
  }
```

now we have to configure in webpack.config.js

```js
const path = require('path')

module.exports = {
    mode: "production",
    entry:'./src/index.js',
    output:{
        path: path.resolve(__dirname,'dist'),
        filename:"main.js"
    },
      devServer:{
      static: {
      directory: path.join(__dirname, "dist")
    },

    compress: true,
    port: 3500, // default 8000
    }
}

```

in package.json 
```js
 "scripts": {
    "build": "webpack",
    "start":"webpack-dev-server --mode development --open"
  }
```
now if run below command our app will automatically run and render 
```js
npm run start
```