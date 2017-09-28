---
layout:     post
title:      "React Native"
date:       2016-04-19 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# Lifecycle

### The Component Lifecycle

Each component has several "lifecycle methods" that you can override to run code at particular times in the process. Methods prefixed with **will** are called right before something happens, and methods prefixed with **did** are called right after something happens.

#### Mounting

These methods are called when an instance of a component is being created and inserted into the DOM:

- [`constructor()`](https://facebook.github.io/react/docs/react-component.html#constructor)
- [`componentWillMount()`](https://facebook.github.io/react/docs/react-component.html#componentwillmount)
- [`render()`](https://facebook.github.io/react/docs/react-component.html#render)
- [`componentDidMount()`](https://facebook.github.io/react/docs/react-component.html#componentdidmount)

#### Updating

An update can be caused by changes to props or state. These methods are called when a component is being re-rendered:

- [`componentWillReceiveProps()`](https://facebook.github.io/react/docs/react-component.html#componentwillreceiveprops)
- [`shouldComponentUpdate()`](https://facebook.github.io/react/docs/react-component.html#shouldcomponentupdate)
- [`componentWillUpdate()`](https://facebook.github.io/react/docs/react-component.html#componentwillupdate)
- [`render()`](https://facebook.github.io/react/docs/react-component.html#render)
- [`componentDidUpdate()`](https://facebook.github.io/react/docs/react-component.html#componentdidupdate)

#### Unmounting

This method is called when a component is being removed from the DOM:

- [`componentWillUnmount()`](https://facebook.github.io/react/docs/react-component.html#componentwillunmount)

  ​

## MOUNT

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

## State 
The state belongs to the component




# Setup

1. react-native init AwesomeProject // Suggest: use upper case for the project name 
2. cd AwesomeProject
3. npm start
4. react-native run-ios
5. npm i

## babel
1. Add dependency In package.json

```java
    "babel-eslint": "4.1.6",
    "eslint": "1.10.3",
    "eslint-config-airbnb": "2.1.1",
    "eslint-plugin-react": "3.12.0",
    "react-native-swipeout": "2.0.12",
    "redux": "^3.3.1"
```
2. Add .eslintrc

## Props, state and store

![Props, state and store](https://unbug.gitbooks.io/react-native-training/content/QQ20160702-0.png)

### Props

- Consider props **immutable**
- Use props for event handlers to communicate with child components.

### State

- Use state for storing simple view state like wether or not drop-down options are visible.
- Never modify this.state directly, use this.setstate instead.
- State is the component that changed in this 





# Functions

## Object.assign()

**Object.assign()** method is used to copy the values of all enumerable own properties from one or more source objects to a target object. It will return the target object.

```java
Object.assign({},todo,{
    completed: !todo.completed; //toggle the todo, change state
  }   
)
  
//3 arg of todo: 
{}: target
todo: source
{completed...}: overwrited data of source
```

## Array

### ...

```
return [...list,0] //return a cancat 0 to the original list
```

### splice

remove elements from array

```
list.splice(index,1)
```

## slice

```
list.slice(0,index) //get sublist from 0 to index elements
```

## concat

```
list.concat(element)
```





## State management (Data management)

### Redux

### Exp2

[Redux react official tutorial](http://redux.js.org/docs/basics/UsageWithReact.html)





### MobX

https://github.com/mobxjs/mobx

[Medium blog](https://medium.com/@dabit3/react-native-with-mobx-getting-started-ba7e18d8ff44#.elp9693qk)

### Baobab 

github https://github.com/Yomguithereal/baobab

http://www.christianalfoni.com/articles/2015_02_06_Plant-a-Baobab-tree-in-your-flux-application

http://www.christianalfoni.com/articles/2015_04_26_Handling-complex-state-with-Baobab

http://www.jianshu.com/p/6d4cce9d914f 

# Tools

# Debug

## Simulator debug menu:

On the iOS Simulator click `Cmd + D`

On the Android Simulator click `Cmd + M`

## Android debug

 ### launch emulator

1. emulator -list-avds (emulator located in folder: ${ANDROID_SDK}/tools/emulator )
2. emulator @Nexus_4_Android_4_4_API_19

## iOS debug

Navigate to HomeScreen: ` Cmd + Shift + h`



## Simulator system log (when app crash)

`Cmd+/`

## bug 

### [NPM modules get required from /Users/node_modules/ instead of the project directory](https://github.com/facebook/react-native/issues/4968)

1. rm -fr node_modules && npm i
2. node_modules/react-native/packager/packager.sh --reset-cache
3. watchman watch-del-all

Select "Debug JS Remotely" from the Developer Menu

Redux logger: https://github.com/evgenyrodionov/redux-logger#usage

Url: http://localhost:8081/debugger-ui

## Pause on caught Exception

In chrome developer tool, sources-right most trangle button- active pause button

## Inspect
- Nuclide: cmd-shift-p -> inspector show 
- Emulator: Show inspector



## Comment

  {/*Comment*/}



# Build And Realease

## Android

### Debug

Bundle debug build:

```
react-native bundle --dev false --platform android --entry-file index.android.js --bundle-output ./android/app/build/intermediates/assets/debug/index.android.bundle --assets-dest ./android/app/build/intermediates/res/merged/debug
```

Create debug build:

```
cd android
./gradlew assembleDebug
```

Generated `apk` will be located at 

`android/app/build/outputs/apk`

## iOS

```
react-native bundle --dev false --platform ios --entry-file index.ios.js --bundle-output ios/main.bundle 
```



# Note

[Airbnb React/JSX Style Guide](https://github.com/airbnb/javascript/tree/master/react)

## Webstorm env setup
1. install ESLint:  `npm install -g eslint`



### Collapse by default

Settings/Preferences dialog -> Editor | General | Code Folding 



## Online build service

bitrise https://www.bitrise.io/

## E-book

[Gitbook](https://unbug.gitbooks.io/react-native-training/content/)

[Video](http://bbs.reactnative.cn/topic/759/%E6%89%8B%E6%8A%8A%E6%89%8B%E6%95%99react-native%E5%AE%9E%E6%88%98%E5%BC%80%E5%8F%91%E8%A7%86%E9%A2%91%E6%95%99%E7%A8%8B-%E6%9B%B4%E6%96%B0%E5%88%B050%E9%9B%86%E5%95%A6/124)

## React Native Skeleton

[Snowflake React-Native Android iOS Starter App/ BoilerPlate](https://github.com/bartonhammond/snowflake)

[pluralsight-redux-starter](https://github.com/coryhouse/pluralsight-redux-starter)

[react-slingshot](https://github.com/coryhouse/react-slingshot)

[Udemy React with Redux Course](https://github.com/StephenGrider/ReduxSimpleStarter)

## UI Library

[Avocode nachos ui](https://avocode.com/nachos-ui/docs)

## Libraries

[React native web](https://github.com/necolas/react-native-web#why)



# Problem Resolving

- ### ENOENT: no such file or directory, uv_chdir

react-native upgrade



## Tutorial



[React Native Tips](https://github.com/JackPu/react-native-tips)

[Snowflake code comments](http://bartonhammond.github.io/snowflake/containers/Main.js.html)

[Lcode blog](http://www.lcode.org/)

React-Native学习指南 https://github.com/reactnativecn/react-native-guide

[React Native之React速学教程(上)](https://github.com/crazycodeboy/RNStudyNotes/blob/master/React%20Native%E4%B9%8BReact%E9%80%9F%E5%AD%A6%E6%95%99%E7%A8%8B/React%20Native%E4%B9%8BReact%E9%80%9F%E5%AD%A6%E6%95%99%E7%A8%8B%20(%E4%B8%8A).md)

React Native 高质量学习资料汇总 http://www.jianshu.com/p/454f2e6f28e9

掘金list http://gold.xitu.io/tag/React%20Native

构建 F8 2016 App: http://f8-app.liaohuqiu.net/tutorials/building-the-f8-app/data/

## Projects

Project list http://www.lcode.org/category/react-native-zong/react-native-source-code/

嘎嘎商城客户端 http://www.lcode.org/react-native-source-gagamall/

