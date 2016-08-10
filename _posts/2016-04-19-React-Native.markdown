---
layout:     post
title:      "React Native"
date:       2016-04-19 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# Setup

react-native init AwesomeProject
cd AwesomeProject
react-native run-ios
react-native start

# Tools

## Set indent to 2 space
File name: .editorconfig

```javascript
# editorconfig.org
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false
```

## Webpack
### webpack is a module bundler. This means webpack takes modules with dependencies and emits static assets representing those modules.

Configuration file is: webpack.config.dev.js

```javascript
import webpack from 'webpack';
import path from 'path';

export default {
  debug: true,
  devtool: 'cheap-module-eval-source-map',
  noInfo: false, //Prod: set to true
  entry: [
    'eventsource-polyfill', // necessary for hot reloading with IE
    'webpack-hot-middleware/client?reload=true', //For hot reload. Note that it reloads the page if hot module reloading fails.
    './src/index'
  ],
  target: 'web',
  output: { //Webpack do not generate any code, but we should put it here
    path: __dirname + '/dist', // Note: Physical files are only output by the production build task `npm run build`.
    publicPath: '/',
    filename: 'bundle.js'
  },
  devServer: {
    contentBase: './src'
  },
  plugins: [
    new webpack.HotModuleReplacementPlugin(), //Hot replace module 
    new webpack.NoErrorsPlugin()
  ],
  module: { // Tell webpack the type of files we handle
    loaders: [
      {test: /\.js$/, include: path.join(__dirname, 'src'), loaders: ['babel']},
      {test: /(\.css)$/, loaders: ['style', 'css']},
      {test: /\.eot(\?v=\d+\.\d+\.\d+)?$/, loader: 'file'},
      {test: /\.(woff|woff2)$/, loader: 'url?prefix=font/&limit=5000'},
      {test: /\.ttf(\?v=\d+\.\d+\.\d+)?$/, loader: 'url?limit=10000&mimetype=application/octet-stream'},
      {test: /\.svg(\?v=\d+\.\d+\.\d+)?$/, loader: 'url?limit=10000&mimetype=image/svg+xml'}
    ]
  }
};
```
# Debug

## bug 1

watchman watch-del-all
npm start -- --reset-cache

Select "Debug JS Remotely" from the Developer Menu
 
Redux logger: https://github.com/evgenyrodionov/redux-logger#usage

Url: http://localhost:8081/debugger-ui

# Note

## React Native Skeleton

pluralsight-redux-starter: https://github.com/coryhouse/pluralsight-redux-starter
react-slingshot: https://github.com/coryhouse/react-slingshot

## Tutorial

React-Native学习指南 https://github.com/reactnativecn/react-native-guide

构建 F8 2016 App: http://f8-app.liaohuqiu.net/tutorials/building-the-f8-app/data/
