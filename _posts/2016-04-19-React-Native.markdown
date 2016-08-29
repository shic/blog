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

- consider props immutable
- Use props to for event handlers to communicate with child components.

### State

- Use state for storing simple view state like wether or not drop-down options are visible.
- Never modify this.state directly, use this.setstate instead.

## Components

### TouchableHighlight

```javascript
class Touch extends Component {
  handlePress(){
    console.log('press');
  }
  handleLongPress(){
    console.log('longPress');
  }
  render() {
    return (
      <TouchableHighlight
        onPress={this.handlePress}
        onLongPress={this.handleLongPress}>
        <View>
          <Text>Press me!</Text>
        </View>
      </TouchableHighlight>
    );
  }
}
```

### TextInput

```javascript
class Test extends Component {
  //...
  //handle events
  //...
  render() {
    return (
      <TextInput 
        onBlur={...}
        onChange={...}
        onEndEditing={...}
        onSelectionChange={...}
        onSubmitEditing={...}
      </TextInput>
    );
  }
}
```

### [Gesture Responder System](https://unbug.gitbooks.io/react-native-training/content/24_events.html)

```java
 render() {
    return (
      <View 
        onStartShouldSetResponderCapture={this.handleStartShouldSetResponderCapture}
        onMoveShouldSetResponderCapture={this.handleMoveShouldSetResponderCapture}
        onStartShouldSetResponder={this.handleStartShouldSetResponder}
        onMoveShouldSetResponder={this.handleMoveShouldSetResponder}
        onResponderGrant={this.handleResponderGrant} 
        onResponderReject={this.handleResponderReject}
        onResponderMove={this.handleResponderMove}
        onResponderRelease={this.handleResponderRelease}
        onResponderTerminationRequest={this.handleResponderTerminationRequest}
        onResponderTerminate={this.handleResponderTerminate}>
          <Text>Press me!</Text>
      </View>
    );
  }
```

### Style

#### Flexbox

```java
flexDirection:'row'|'column'

justifyContent:'flex-start'|'flex-end'|'center'|'space-between'|'space-around'

alignItems:'flex-start'|'flex-end'|'center'|'stretch'

alignSelf:'auto'|'flex-start'|'flex-end'|'center'|'stretch'

flexWrap:'wrap'|'nowrap'

```

#### absolute

```java
  box1: {
    position: 'absolute',
    top: 40,
    left: 40,
    width: 100,
    height: 100,
    backgroundColor: 'red'
    transform: [{'translate': [0,0, 1]}]
    borderRadius: 20,

  }
```

#### Base Style

```html

// BaseStyles.js
import {  StyleSheet,Dimensions } from 'react-native';
let winSize = Dimensions.get('window');
const BaseStyles = StyleSheet.create({
  text: {
    fontSize: 40/winSize.scale
  }
});
export default BaseStyles;

// Component
import BaseStyles from './BaseStyles';

class InheritanceStyle extends Component {
  render() {
    return (
      <View style={this.props.parentColor}>
        <Text style={[BaseStyles.text, styles.text]}> this is a long text </Text>
      </View>
    );
  }
}
const styles = StyleSheet.create({
  text:{
    color: '#ffffff'
  }
});
```


#### absolute

```java

```


## 数据流的处理

### Redux

```java
function reducer(state, action) //state: old state; action: sort of event, it may contains description or some data
{
  //calculate newState, here we mutate state into new state
  return newState;
}
redux.createStore(reducer);//create a store which gets used by react components

```

#### Create a Redux store

```java
//todoStore.js
import { createStore } from 'redux';

const defaultTodos = [
    {
        task: 'Initial todo in store',
        state: 'pending',
    },
];

const defaultState = {
    todos: defaultTodos,
    filter: 'pending',
    filteredTodos: defaultTodos,
};

function getFilteredTodos(allTodos, filter) {
    return allTodos.filter(todo => todo.state === filter);
}

function todoStore(state = defaultState, action) {
    switch (action.type) {//switch the type attribute
    case 'ADD_TODO':
        //state.todos: takes the old todos
        const allTodos = state.todos.concat([{
            task: action.task,
            state: 'pending',
        }]);
        
        //Use Object.assign to mutate the old state
        return Object.assign({}, state, {
            todos: allTodos,
            //filteredTodos: getFilteredTodos(allTodos, state.filter),
        });

    case 'DONE_TODO':
        const doneTodo = Object.assign({}, action.todo, {
            state: 'done',
        });

        const allTodosContainingDone = state.todos
            .map((todo) => {
                return todo === action.todo ? doneTodo : todo;
            });

        return Object.assign({}, state, {
            todos: allTodosContainingDone,
            filteredTodos: getFilteredTodos(allTodosContainingDone, state.filter),
        });
    case 'TOGGLE_STATE':
        const filter = state.filter === 'pending' ? 'done' : 'pending';
        return Object.assign({}, state, {
            filter,
            filteredTodos: getFilteredTodos(state.todos, filter),
        });
    default:
        return state;
    }
}

export default createStore(todoStore); // Use createStore that we got from redux

```
#### Sync PluralTodo component’s state with Redux state

```java
// PluralTodo.js
const React = require('react-native');
const {
    Component,
    Navigator,
} = React;
import TaskList from './TaskList';
import TaskForm from './TaskForm';
import todoStore from './todoStore';

class PluralTodo extends Component {
    constructor(props, context) {
        super(props, context);
        this.state = todoStore.getState();

        //State is mutated in the store, so we have to subscribe state mutated, so we can get the update 
        todoStore.subscribe(() => {
            this.setState(todoStore.getState()); // eslint-disable-line react/no-set-state
        });
    }

    onAddStarted() {
        this.nav.push({
            name: 'taskform',
        });
    }

    onCancel() {
        console.log('cancelled!');
        this.nav.pop();
    }

    onAdd(task) {
        console.log('a task was added: ', task);
        // this.state.todos.push({ task });
        // this.setState({ todos: this.state.todos });
        todoStore.dispatch({ //dispatch: fire an action on the store 
            type: 'ADD_TODO',
            task,
        });
        this.nav.pop();
    }

    onDone(todo) {
        console.log('todo was completed: ', todo.task);
        todoStore.dispatch({
            type: 'DONE_TODO',
            todo,
        });
    }

    onToggle() {
        todoStore.dispatch({
            type: 'TOGGLE_STATE',
        });
    }

    renderScene(route, nav) {
        switch (route.name) {
        case 'taskform':
            return (
                <TaskForm
                    onAdd={this.onAdd.bind(this)}
                    onCancel={this.onCancel.bind(this)}
                />
            );
        default:
            return (
                <TaskList
                    filter={this.state.filter}
                    filteredTodos={this.state.filteredTodos}
                    onAddStarted={this.onAddStarted.bind(this)}
                    onDone={this.onDone.bind(this)}
                    onToggle={this.onToggle.bind(this)}
                />
            );
        }
    }

    configureScene() {
        return Navigator.SceneConfigs.FloatFromBottom;
    }

    render() {
        return (
            <Navigator
                configureScene={this.configureScene}
                initialRoute={{ name: 'tasklist', index: 0 }}
                ref={((nav) => {
                    this.nav = nav;
                })}
                renderScene={this.renderScene.bind(this)}
            />
        );
    }
}

export default PluralTodo;

```

```java
//TaskList.js
import React from 'react-native';

const {
    View,
    ListView,
    TouchableHighlight,
    Text,
    Switch,
} = React;

import TaskRow from './TaskRow/Component';

const styles = React.StyleSheet.create({
    container: {
        paddingTop: 40,
        backgroundColor: '#F7F7F7',
        flex: 1,
        justifyContent: 'flex-start',
    },
    button: {
        height: 60,
        borderColor: '#05A5D1',
        borderWidth: 2,
        backgroundColor: '#333',
        margin: 20,
        justifyContent: 'center',
        alignItems: 'center',
    },
    buttonText: {
        color: '#FAFAFA',
        fontSize: 20,
        fontWeight: '600',
    },
});

class TaskList extends React.Component {
    constructor(props, context) {
        super(props, context);

        const ds = new ListView.DataSource({
            rowHasChanged: (r1, r2) => r1 !== r2,
        });

        this.state = {
            dataSource: ds.cloneWithRows(props.filteredTodos),
        };
    }

    componentWillReceiveProps(nextProps) {
        const dataSource = this
            .state
            .dataSource
            .cloneWithRows(nextProps.filteredTodos);

        this.setState({ dataSource });
    }

    renderRow(todo) {
        return (
            <TaskRow
                onDone={this.props.onDone}
                todo={todo}
            />
        );
    }

    render() {
        return (
            <View style={styles.container}>
            <View
                style={{
                    flexDirection: 'row',
                    padding: 10,
                }}
            >
                <Switch
                    onValueChange={this.props.onToggle}
                    style={{
                        marginBottom: 10,
                    }}
                    value={this.props.filter !== 'pending'}
                />
                <Text style={{
                    fontSize: 20,
                    paddingLeft: 10,
                    paddingTop: 3,
                }}
                >
                Showing {this.props.filteredTodos.length} {this.props.filter} todo(s)
                </Text>
            </View>

                <ListView
                    dataSource={this.state.dataSource}
                    renderRow={this.renderRow.bind(this)}
                />

                <TouchableHighlight
                    onPress={this.props.onAddStarted}
                    style={styles.button}
                >
                    <Text
                        style={styles.buttonText}
                    >
                        Add one
                    </Text>
                </TouchableHighlight>
            </View>
        );
    }
}

TaskList.propTypes = {
    filter: React.PropTypes.string.isRequired,
    filteredTodos: React.PropTypes
        .arrayOf(React.PropTypes.object).isRequired,
    onAddStarted: React.PropTypes.func.isRequired,
    onDone: React.PropTypes.func.isRequired,
    onToggle: React.PropTypes.func.isRequired,
};

export default TaskList;
```

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

## iOS debug

Simulator home button: ` Cmd + Shift + h` for navigate to HomeScreen



## Simulator system log (when app crash)

Cmd+/

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
  
  
# Note

## Webstorm env setup
1. install ESLint:  `npm install -g eslint`
2. 

## Online build service

bitrise https://www.bitrise.io/

## E-book

Gitbook [https://unbug.gitbooks.io/react-native-training/content/](https://unbug.gitbooks.io/react-native-training/content/)

Video [http://bbs.reactnative.cn/topic/759](http://bbs.reactnative.cn/topic/759/%E6%89%8B%E6%8A%8A%E6%89%8B%E6%95%99react-native%E5%AE%9E%E6%88%98%E5%BC%80%E5%8F%91%E8%A7%86%E9%A2%91%E6%95%99%E7%A8%8B-%E6%9B%B4%E6%96%B0%E5%88%B050%E9%9B%86%E5%95%A6/124)

## React Native Skeleton

[pluralsight-redux-starter](https://github.com/coryhouse/pluralsight-redux-starter)

react-slingshot: https://github.com/coryhouse/react-slingshot

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

