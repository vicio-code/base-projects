# Creating a React base project

## First Things

Using GitHub create a repo for you base project and clone it to you machine. Then initialize the project with `yarn init --yes`.

Setup the folder structure

```bash
public/
src/
|
| --- components/
      |
      | --- core/ # commom components
      | --- GeneralComponents.js ...
| --- assets/
     | --- img.png
| --- pages/
     |
     | --- MyPage.js
| --- index.js # app entrypoint
| --- app.js # app setup
```

Add at least the direcotires `node_modules`and `dist` to `.gitignore`

Add `index.html` to `public` directory

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />
    <title>React Starter</title>
  </head>

  <body>
    <div id="root"></div>
    <noscript> You need to enable JavaScript to run this app. </noscript>
    <script src="../dist/bundle.js"></script>
  </body>
</html>
```

## Babel

Run `yarn add -D @babel/core @babel/cli @babel/preset-env @babel/preset-react`

In the root, create a file `.babelrc` with:

`{ "presets": ["@babel/env", "@babel/preset-react"] }`

## Webpack

Run `yarn add -D webpack webpack-cli webpack-dev-server style-loader css-loader babel-loader`

In the root, create a file `webpack.config.js` with:

```javascript
const path = require("path");
const webpack = require("webpack");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: path.resolve(__dirname, "./src/index.js"),
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: ["babel-loader"],
      },
      {
        test: /\.css$/,
        exclude: /node_modules/,
        use: ["style-loader", "css-loader"],
      },
    ],
  },
  resolve: {
    extensions: ["*", ".js", ".jsx"],
  },
  output: {
    path: path.resolve(__dirname, "./dist"),
    filename: "bundle.js",
  },
  plugins: [
    new webpack.HotModuleReplacementPlugin(),
    new HtmlWebpackPlugin({ template: "./public/index.html" }),
  ],
  devServer: {
    contentBase: path.resolve(__dirname, "./dist"),
    hot: true,
  },
};

```

## React

Add the packages `react` and `react-dom` and save as regular dependencies

Add `index.js` in `src` directory with:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App.js';

ReactDOM.render(<App />, document.getElementById('root'));

module.hot.accept();
```

Add `App.js` in `src` directory with:

```javascript
import React, { Component } from "react";
import { hot } from "react-hot-loader";
import "./App.css";

class App extends Component {
  render() {
    return (
      <div className="App">
        <h1> Hello, World!</h1>
      </div>
    );
  }
}

export default hot(module)(App);
```

Add `App.css` in `src` directory with:

```css
.App {
  margin: 1rem;
  font-family: Arial, Helvetica, sans-serif;
}
```

## React Hot Loader

Run `yarn add react-hot-loader`

## ESLint

Run `yarn add eslint --dev` and `yarn run eslint --init` to install ESLint

Add this script `"lint": "eslint src --ext .js --fix"` to `package.json`

## Prettier

Run `yarn add eslint-config-prettier eslint-plugin-prettier prettier --dev` to install Prettier

In `.eslintrc.json` add `"plugin:prettier/recommended"` inside extends.
