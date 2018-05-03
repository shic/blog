---
layout:     post
title:      "React Native"
date:       2016-04-30 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# [Component Lifecycle](https://reactjs.org/docs/react-component.html)

Each component has several "lifecycle methods" that you can override to run code at particular times in the process. 

Methods prefixed with **will** are called right before something happens 

Methods prefixed with **did** are called right after something happens.

Everytime we change the state of component, it will rerender itself



## MOUNTING

These methods are called when an instance of a component is being created and inserted into the DOM:

- [`constructor()`][1]

    Set default state using a constructor.

    ```
    this.state = {
          loading: false,
          error: null,
          stockProduct,
    };
    ```

    ​

- #### [`componentWillMount()`][2]

    Do nothing here	

- [`render()`][3]

## MOUNTED

- [`componentDidMount()`][4]

  This is the point when you should initiate AJAX requests

## RECEIVING PROPS
- [componentWillReceiveProps](https://reactjs.org/docs/react-component.html#unsafe_componentwillreceiveprops)

  Do nothing here

  ​


### Updating

An update can be caused by changes to props or state. These methods are called when a component is being re-rendered:

- [`componentWillReceiveProps()`][5]

- [`shouldComponentUpdate()`][6]

- [`componentWillUpdate()`][7]

  Component rerender. Put the layout animation here

  Do nothing here

- [`render()`][8]

- [`componentDidUpdate()`][9]

#### Unmounting

This method is called when a component is being removed from the DOM:

- [`componentWillUnmount()`][10]

  Unregister listener



## UPDATED
- componentDidUpdate








# Setup

Mac dev env setup

1.  Update Xcode

2.  Homebrew https://brew.sh/ 

3.  Node `brew install node`

4.  `brew install watchman`

5.  `npm install -g react-native-cli`

    if not permitted to install globally `sudo chown -R $USER /usr/local`

    (Enable the root user)[https://support.apple.com/en-us/HT204012]

6.  `mpn i`




### Start the RN server

npm start --reset-cache



## Tools

(Crashlytics)[https://streetsmartdev.com/react-native-analytics-fabric/]



```

```

## Project init

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



# React and RN

React

- How a component behave
- Take a bunch of components work together



RN

- How to take the output from a component and place it on the screen
- Provide default core components (image, text)



# Project structure

## Component

View

### Create a component

#### Functional component 

-   Used for static data, for presentational use
-   Easy to write

```javascript
const SomeComponent = () => {
    return (
      <Text>Some text</Text>
    );
}

//Make component available to other part of the app
export default SomeComponent;
```

Note: this is a JSX. JSX is JS, also the XML will be converted to JS. Example can be found [here][11].

#### Class Component 

-   Can add some functions
-   Based on ES6 class

```javascript
import React, {Component} from 'react'
class SomeComponent extends Component {
    render(){
      return (
      	<Text>Some text</Text>
      );
    }
}
```

and the following code have the same result

```javascript
import React, {Component} from 'react'
class SomeComponent extends Component {
    render = ()=>{
      return (
      	<Text>Some text</Text>
      );
    }
}
```



### Use Component

```jsx
import SomeComponent from './src/component/SomeComponent' 

<SomeComponent></SomeComponent>

```

### Return a Component 

We can only return one component! 

```
// This is not allowed
const App = () =>{
    return (
        <Header headerText={'Albums'}/>
        <AlbumList/>
    )
}
//It's like you try to return two elements
const App = () =>{
    return (        <Header headerText={'Albums'}/>    )
    return (        <AlbumList/> )
}
//And it will not work

```



## Render

Render a component to screen means take the view and place it on mobile device.

```javascript
ReactNative.AppRegistry.registerComponent('albums', () => SomeComponent)

//Only the 'root' compoennt uses 'AppRegistry'
//'albums' is the name of the application.
//' () => SomeComponent' is the function that returns the first component to run for our application
```



 

## Import

The **import** statement is used to import bindings which are exported by another module.

ES6 feature, outside code out of file should be imported.

#### Use {} or not.

```java
// if the binding is exported using 'export default myDefaultExport;' you should not use {} to import the binding
import myDefaultExport from '/modules/my-module.js';

// otherwith use
import {myExport} from '/modules/my-module.js';

```



# Storage

## Props, state and store

![Props, state and store][image-1]

## Props

Short for porperties

Passing data from parent component to child component 

- Consider props **immutable**
- Use props for event handlers to communicate with child components. (parent, child communication)

```javascript
//Parent provide the prop that the child is expecting
<ChildComponent contentPassToChild={'I am a child'}/>

//Child
const ChildComponent = (props)=>{
    return(
    	<Text>{props.contentPassToChild}</Text>
    )
}
```

Note that `contentPassToChild` can be text, function ecc.

 

#### props.children

Father can pass any views to the child, and the child receive with `props.children`

```
//Father
const AlbumDetail =(props)=>{
    return(
        <Card>
            <Text>{props.album.title}</Text>
        </Card>
    )
}

//Child
const Card =(props)=>{
    return(
        <View>
            {props.children}
        </View>
    )
}
```

#### Destructure the props

```
const AlbumDetail = (props) => {
    const {thumbnailStyle,headerContentStyle}=styles;

    return (
        <Card>
            <CardSection>
                <View>
                    <Image
                        style={thumbnailStyle}
                        source={{uri: props.album.thumbnail_image}}
                    />
                </View>
                <View style={headerContentStyle}>
                    <Text>{props.album.title}</Text>
                    <Text>{props.album.artist}</Text>
                </View>

            </CardSection>
        </Card>
    )
}
```



the code above can be writen in this way 

##### attention to the  ({album}) instead of  (album) 

```
const AlbumDetail = ({album}) => {
    const {title,artist,thumbnail_image} = album;
    const {thumbnailStyle,headerContentStyle}=styles;

    return (
        <Card>
            <CardSection>
                <View>
                    <Image
                        style={thumbnailStyle}
                        source={{uri: thumbnail_image}}
                    />
                </View>
                <View style={headerContentStyle}>
                    <Text>{title}</Text>
                    <Text>{artist}</Text>
                </View>

            </CardSection>
        </Card>
    )
}
```



## State

The state belongs to the component. 

-   It is used for component internal record keeping, so we use it to update data.


-   Use state for **storing simple view state** like wether or not drop-down options are visible.
-   **Never modify this.state directly**, use this.setstate instead.
-   State is the component that changed in this.






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

[Redux react official tutorial][12]



### MobX

https://github.com/mobxjs/mobx

[Medium blog][13]

### Baobab

github https://github.com/Yomguithereal/baobab

http://www.christianalfoni.com/articles/2015\_02\_06\_Plant-a-Baobab-tree-in-your-flux-application

http://www.christianalfoni.com/articles/2015\_04\_26\_Handling-complex-state-with-Baobab

http://www.jianshu.com/p/6d4cce9d914f 

# File organization

We can create a `index.js` file in folder `src/components/common` that contains all the exports in this folder.

it can be imported from other files because it will be recognized automatically . 

```
//index.js

import Alerts from './Alerts';
import Button from './Button';
import Card from './Card';

export {
  Alerts,
  Button,
  Card
};

//Use it in other file 
import {Alerts} from './components/common';
//instead of
import {Alerts} from './components/common/Alerts';



```





# Logo

#### In Android:

the app icon is picked up from <your project>\android\app\src\main\res\mipmap-xxxx\ directories.



#### In IOS:

- you should set `AppIcon` in `Images.xcassets`.
- you should upload 9 different size icons `29pt` `29pt*2` `29pt*3` `40pt*2` `40pt*3`57pt\`\` `57pt*2` `60pt*2` `60pt*3`.”




# APIs

### [Linking](https://facebook.github.io/react-native/docs/linking.html)

Open webpage  [Linking.openURL(url)](https://facebook.github.io/react-native/docs/linking.html#openurl)



# Debug

## Android debug

Simulator debug menu on the Android Simulator click `Cmd + M`

### Launch emulator

1. `emulator -list-avds`

    emulator located in folder: `${ANDROID\_SDK}/tools/emulator ` which on Mac located at  `~/Library/Android/sdk/tools/emulator `

   Cmd is `~/Library/Android/sdk/tools/emulator -list-avds`

2. `emulator @Nexus\_4\_Android\_4\_4\_API\_19`



### Debug on device

1. Check if your device is connected.

   Run `adb devices` from the`android_sdk/platform-tools/` directory. If connected, you'll see the device name listed as a "device." i.e. `ce041604d44c0e1603 device`

   On mac command is `/Users/shi/Library/Android/sdk/platform-tools/adb devices`

2. react-native run-android

3. Make sure your laptop and your phone are on the **same** Wi-Fi network.

4. find the computer IP address in **System Preferences** → **Network**.

5. Open the in-app [Developer menu][14].

6. Go to **Dev Settings** → **Debug server host for device**.

7. Type in your machine's IP address and the port of the local dev server (e.g. 192.168.1.11**:8081**).

## iOS debug

Simulator debug menu on the iOS Simulator: `Cmd + D`

Show log:  `Cmd + D` -> `Remote JS Debugging`

Navigate to HomeScreen: `Cmd + Shift + h`

https://facebook.github.io/react-native/docs/running-on-device.html

Show simulator system log (when app crash): `Cmd+/`



# Bugs

### [NPM modules get required from /Users/node\_modules/ instead of the project directory][15]

1. rm -fr node\_modules && npm i
2. node\_modules/react-native/packager/packager.sh --reset-cache
3. watchman watch-del-all

Select "Debug JS Remotely" from the Developer Menu

Redux logger: https://github.com/evgenyrodionov/redux-logger#usage

Url: http://localhost:8081/debugger-ui

## Pause on caught Exception

In chrome developer tool, sources-right most trangle button- active pause button

## Inspect
- Nuclide: cmd-shift-p -\> inspector show 
- Emulator: Show inspector



## Comment

  {/*Comment*/}



# Crash Reporting

[Bug report system www.bugsnag.com](https://www.bugsnag.com/platforms/react-native-error-reporting/)



# Build And Realease

## Android

### Debug Build

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

```
open app/build/outputs/apk && cd ..
```

```
react-native bundle --dev false --platform android --entry-file index.android.js --bundle-output ./android/app/build/intermediates/assets/debug/index.android.bundle --assets-dest ./android/app/build/intermediates/res/merged/debug && cd android && ./gradlew assembleDebug && open app/build/outputs/apk && cd ..

```



## iOS

```
react-native bundle --dev false --platform ios --entry-file index.ios.js --bundle-output ios/main.bundle 
```



## Rename the project

1.  Rename the app name in app.json file

    ```
    {
      "name": "Album",
      "displayName": "Album"
    }
    ```

2.  Rename the app name in index.android.js and index.ios.js

3.  Rename the app name in package.json

4.  Delete android and ios folder

5.  Run `react-native link`

6.  Run ` react-native eject`

7.  Run `react-native run-ios`

8.  Android SDK location 

    `sudo nano ~/.bashrc`

    Add `export ANDROID_HOME=/Users/ufirstuser/Library/Android/sdk`

9.  Android Studio download 'android-23' and 'Build Tools revision 23.0.1/25.0.2/26.0.1'




# [AppState](https://facebook.github.io/react-native/docs/appstate.html)

`AppState` can tell you if the app is in the foreground or background, and notify you when the state changes.



# [NetInfo](https://facebook.github.io/react-native/docs/netinfo.html)

NetInfo exposes info about online/offline status



# Http (not Https) on iOS simulator

Modify plist which located in `ios/Uper/info.plist`

```
	<key>NSAppTransportSecurity</key>
	<dict>
		<key>NSExceptionDomains</key>
		<dict>
			<key>localhost</key>
			<dict>
				<key>NSExceptionAllowsInsecureHTTPLoads</key>
				<true/>
			</dict>
			<key>uupper.com</key>
			<dict>
				<key>NSExceptionAllowsInsecureHTTPLoads</key>
				<true/>
				<key>NSIncludesSubdomains</key>
				<true/>
			</dict>
		</dict>
	</dict>

```



# Note

## Step to copy a project

1. Add local.properties file in android folder with the sdk location `sdk.dir=/Users/shi/Library/Android/sdk`
2. Change iOS plist to allow http
3. Install npm
4. Run `react-native link`
5. Run `react-native run-ios`

## Attention!

-   All the network request must be https

## [Airbnb React/JSX Style Guide][16]

## Eslint rules

https://github.com/yannickcr/eslint-plugin-react/tree/master/docs/rules

## Webstorm env setup
1. install ESLint:  `npm install -g eslint`



### Collapse by default

Settings/Preferences dialog -\> Editor | General | Code Folding 



## Online build service

bitrise https://www.bitrise.io/

## E-book

[Gitbook][17]

[Video][18]

## React Native Skeleton

[Snowflake React-Native Android iOS Starter App/ BoilerPlate][19]

[pluralsight-redux-starter][20]

[react-slingshot][21]

[Udemy React with Redux Course][22]

## UI Library

[Avocode nachos ui][23]

## Libraries

[React native web][24]

### Barcode/QR code scanner

react-native-camera

```
npm install --save react-native-camera
react-native link react-native-camera
```



http://manojsinghnegi.com/blog/2017/08/18/Implementing-Barcode-scanner-in-react-native/

# Trouble Shooting

### - ENOENT: no such file or directory, uv\_chdir

react-native upgrade

### SDK location not found. Define location with sdk.dir in the local.properties file or with an ANDROID_HOME environment variable.

Add local.properties file in android folder with the sdk location `sdk.dir=/Users/shi/Library/Android/sdk`

### No bundle URL present, make sure you are running a package server

#### Solution 1

Kill app on iOS device and relaunch it

#### Solution 2

rm -r ./ios/build/

react-native run-ios



### Warning: Each child in an array or iterator should have a unique "key" prop.

This is for render efficiency ; just add a unique key for each elements in the iterator like this

```java
    renderAlbums(){
        return this.state.albums.map(album=>
            <Text key={album.id}>{album.title}</Text>
        )
    }
```

### Directory /src/components/AlbumDetail doesn't exist

```java
//The following is not work, because the directory name should contain ./
import AlbumDetail from '/src/components/AlbumDetail';
//like this
import AlbumDetail from '/src/components/AlbumDetail';
//but if you are not in the root folder, use
import AlbumDetail from './AlbumDetail';
```



[Error Example](http://www.jianshu.com/p/98c8f2a970eb)



## Tutorial

[Github repo](https://github.com/StephenGrider/ReactNativeReduxCasts) for the  [The Complete React Native and Redux Course](https://www.udemy.com/the-complete-react-native-and-redux-course/)

[React Native Tips][25]

[Snowflake code comments][26]

[Lcode blog][27]

React-Native学习指南 https://github.com/reactnativecn/react-native-guide

[React Native之React速学教程(上)][28]

React Native 高质量学习资料汇总 http://www.jianshu.com/p/454f2e6f28e9

掘金list http://gold.xitu.io/tag/React%20Native

构建 F8 2016 App: http://f8-app.liaohuqiu.net/tutorials/building-the-f8-app/data/

## Projects

Project list http://www.lcode.org/category/react-native-zong/react-native-source-code/

嘎嘎商城客户端 http://www.lcode.org/react-native-source-gagamall/

[1]:	https://facebook.github.io/react/docs/react-component.html#constructor
[2]:	https://facebook.github.io/react/docs/react-component.html#componentwillmount
[3]:	https://facebook.github.io/react/docs/react-component.html#render
[4]:	https://facebook.github.io/react/docs/react-component.html#componentdidmount
[5]:	https://facebook.github.io/react/docs/react-component.html#componentwillreceiveprops
[6]:	https://facebook.github.io/react/docs/react-component.html#shouldcomponentupdate
[7]:	https://facebook.github.io/react/docs/react-component.html#componentwillupdate
[8]:	https://facebook.github.io/react/docs/react-component.html#render
[9]:	https://facebook.github.io/react/docs/react-component.html#componentdidupdate
[10]:	https://facebook.github.io/react/docs/react-component.html#componentwillunmount
[11]:	http://babeljs.io/
[12]:	http://redux.js.org/docs/basics/UsageWithReact.html
[13]:	https://medium.com/@dabit3/react-native-with-mobx-getting-started-ba7e18d8ff44#.elp9693qk
[14]:	https://facebook.github.io/react-native/docs/debugging.html#accessing-the-in-app-developer-menu
[15]:	https://github.com/facebook/react-native/issues/4968
[16]:	https://github.com/airbnb/javascript/tree/master/react
[17]:	https://unbug.gitbooks.io/react-native-training/content/
[18]:	http://bbs.reactnative.cn/topic/759/%E6%89%8B%E6%8A%8A%E6%89%8B%E6%95%99react-native%E5%AE%9E%E6%88%98%E5%BC%80%E5%8F%91%E8%A7%86%E9%A2%91%E6%95%99%E7%A8%8B-%E6%9B%B4%E6%96%B0%E5%88%B050%E9%9B%86%E5%95%A6/124
[19]:	https://github.com/bartonhammond/snowflake
[20]:	https://github.com/coryhouse/pluralsight-redux-starter
[21]:	https://github.com/coryhouse/react-slingshot
[22]:	https://github.com/StephenGrider/ReduxSimpleStarter
[23]:	https://avocode.com/nachos-ui/docs
[24]:	https://github.com/necolas/react-native-web#why
[25]:	https://github.com/JackPu/react-native-tips
[26]:	http://bartonhammond.github.io/snowflake/containers/Main.js.html
[27]:	http://www.lcode.org/
[28]:	https://github.com/crazycodeboy/RNStudyNotes/blob/master/React%20Native%E4%B9%8BReact%E9%80%9F%E5%AD%A6%E6%95%99%E7%A8%8B/React%20Native%E4%B9%8BReact%E9%80%9F%E5%AD%A6%E6%95%99%E7%A8%8B%20(%E4%B8%8A).md

[image-1]:	https://unbug.gitbooks.io/react-native-training/content/QQ20160702-0.png

