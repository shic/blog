---
layout:     post
title:      "React Native"
date:       2016-04-19 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# Lifecyle

## MOUNT
- getDefaultProps
- getInitialState
- componentWillMount
  - Register listener
  - 
- render

## MOUNTED
- componentDidMount

## RECEIVING PROPS
- componentWillReceiveProps
  - update data here
- componentWillMount
- componentWillUnmount
  - Unregister listener

## UPDATED
- componentDidUpdate
- 

## State 
The state belongs to the component




# Setup

1. react-native init AwesomeProject // Suggest: use upper case for the project name 
2. cd AwesomeProject
3. react-native run-ios
4. react-native start
5. npm i

## babel
1. Add dependency In package.json

```javascript
    "babel-eslint": "4.1.6",
    "eslint": "1.10.3",
    "eslint-config-airbnb": "2.1.1",
    "eslint-plugin-react": "3.12.0",
    "react-native-swipeout": "2.0.12",
    "redux": "^3.3.1"
```
2. Add .eslintrc

# Tools

# Debug
## Simulator system log (when app crash)
Cmd+/

## bug 1

watchman watch-del-all

rm -fr node_modules && npm i

npm start -- --reset-cache

Select "Debug JS Remotely" from the Developer Menu
 
Redux logger: https://github.com/evgenyrodionov/redux-logger#usage

Url: http://localhost:8081/debugger-ui

## Pause on caught Exception

In chrome developer tool, sources-right most trangle button- active pause button

## Inspect
- Nuclide: cmd-shift-p -> inspector show 
- Emulator: Show inspector


## 数据流的处理
### Baobab 

github https://github.com/Yomguithereal/baobab

http://www.christianalfoni.com/articles/2015_02_06_Plant-a-Baobab-tree-in-your-flux-application

http://www.christianalfoni.com/articles/2015_04_26_Handling-complex-state-with-Baobab

## Comment

  {/*Comment*/}

# Note

## Gitbook
E-book https://unbug.gitbooks.io/react-native-training/content/
Video http://bbs.reactnative.cn/topic/759/%E6%89%8B%E6%8A%8A%E6%89%8B%E6%95%99react-native%E5%AE%9E%E6%88%98%E5%BC%80%E5%8F%91%E8%A7%86%E9%A2%91%E6%95%99%E7%A8%8B-%E6%9B%B4%E6%96%B0%E5%88%B050%E9%9B%86%E5%95%A6/124

## React Native Skeleton

pluralsight-redux-starter: https://github.com/coryhouse/pluralsight-redux-starter
react-slingshot: https://github.com/coryhouse/react-slingshot

## Tutorial

Studying blog http://www.lcode.org/

Baobab http://www.jianshu.com/p/6d4cce9d914f 

React-Native学习指南 https://github.com/reactnativecn/react-native-guide

React Native 高质量学习资料汇总 http://www.jianshu.com/p/454f2e6f28e9



构建 F8 2016 App: http://f8-app.liaohuqiu.net/tutorials/building-the-f8-app/data/

## E-books
https://github.com/apoterenko/javascript-ebooks

## Projects

Project list http://www.lcode.org/category/react-native-zong/react-native-source-code/

嘎嘎商城客户端 http://www.lcode.org/react-native-source-gagamall/

