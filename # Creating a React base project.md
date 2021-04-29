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
This line was copied from a 2018 article, there is probaly a more evergreen solution. Also need to change npm to yarn.

In the root, create a file `.babelrc` with:

`{ "presets": ["@babel/env", "@babel/preset-react"] }`

## Webpack

Run `yarn add -D webpack webpack-cli webpack-dev-server style-loader css-loader babel-loader`
This line was copied from a 2018 article, there is probaly a more evergreen solution. Also need to change npm to yarn.

In the root, create a file `webpack.config.js` with:

```javascript
const path = require("path");
const webpack = require("webpack");

module.exports = {
  entry: "./src/index.js",
  mode: "development",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /(node_modules|bower_components)/,
        loader: "babel-loader",
        options: { presets: ["@babel/env"] },
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"],
      },
    ],
  },
  resolve: { extensions: ["*", ".js", ".jsx"] },
  output: {
    path: path.resolve(__dirname, "dist/"),
    publicPath: "/dist/",
    filename: "bundle.js",
  },
  devServer: {
    contentBase: path.join(__dirname, "public/"),
    port: 3000,
    publicPath: "http://localhost:3000/dist/",
    hotOnly: true,
  },
  plugins: [new webpack.HotModuleReplacementPlugin()],
};
```

## React

Add the packages `react` and `react-dom` and save as regular dependencies

Add `index.js` in `src` directory with:

```javascript
import React from "react";
import ReactDOM from "react-dom";
import App from "./App.js";
ReactDOM.render(<App />, document.getElementById("root"));
```

Add `App.js` in `src` directory with:

```javascript
import React, { Component } from "react";
import "./App.css";

class App extends Component {
  render() {
    return (
      <div className="App">
        <h1> Hello, World! </h1>
      </div>
    );
  }
}

export default App;
```

Add `App.css` in `src` directory with:

```css
.App {
  margin: 1rem;
  font-family: Arial, Helvetica, sans-serif;
}
```

## Last detail

This [Article](https://blog.usejournal.com/creating-a-react-app-from-scratch-f3c693b84658) sugestes using `react-hot-loader` to tell HRM how to update our client. But I have no idea what is so I`m skiping this step for now.

## ESLint

Run `yarn add eslint --dev` and `yarn run eslint --init` to install ESLint

Add this script `"lint": "eslint src --ext .js --fix"` to `package.json`

## Material-UI

Run `yarn add @material-ui/core`

Add Roboto Font and Font icons

```html
<link
  rel="stylesheet"
  href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap"
/>
<link
  rel="stylesheet"
  href="https://fonts.googleapis.com/icon?family=Material+Icons"
/>
```

Add SVG Icons `yarn add @material-ui/icons`

In App.css update the font

Also do this "Setup de um tema central inicializado na base de renderização do app
Uso de um hook de estilo como exemplo (pode ser um componente básico como button)"
