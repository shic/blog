---
flayout:     post
title:      "React Redux"
date:       2016-04-10 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# *React Redux*

# Redux Basics

## Props, state and store

![Props, state and store](https://unbug.gitbooks.io/react-native-training/content/QQ20160702-0.png)

### Props

- Consider props **immutable**
- Use props for event handlers to communicate with child components.

### State

- Use state for **storing simple view state** like wether or not drop-down options are visible.
- Never modify this.state directly, use this.setstate instead.
- State is the component that changed in this 




**[Takeaway](https://medium.freecodecamp.org/where-do-i-belong-a-guide-to-saving-react-component-data-in-state-store-static-and-this-c49b335e2a00)**:

keep UI state and transitory data (such as form inputs) in local **state**.

keep data that you intend to share across components in **store**.

use **this** to store things that shouldn’t trigger a re-render.



Steps:

1.  Provider

    ```

    ```

    ​

2.  Create reducers that has initial state, has switch function to switch different action type pass to the reducer, and return new state

3.  Combine reducers toghether 

4.  Create the action that has type property (command to the reducer)

5.  Create mapStateToProps function 

6.  Create an action creator 

    ```
    export const emailChanged = (text) =>{
        return{
            type:'email_changed',
            payload:text
        }
    }
    ```

    Import connect helper in component:

    ```
    import {connect} from 'react-redux'
    ```

    Hook component to connect helper

    ​

    Import action to the file where we call the action from.

    ```
    import * as actions from '../actions'
    ```

    Create a reducer:

    ​

    Combine reducers toghether 

7.  ​

## Example in React.js



#### Reducer

Reducer is the function that trace the previous state, the action to be dispatched and the next state of the app. The function must to be pure.

Reducer must have the initial state, it can not return the state that is undefined

Reducer must return new state that is really changed. 

```
case EMAIL_CHANGED:
	state.email = action.payload;
	return state;
```

will not work, because the returned state changed the content, but when redux compare states with `newstate=oldstate` , the result is true, means the states not changed, the conponents will not render.

return new state in this way

```
return {...state,email:action.payload};
```







```java
function todoStoreReducer(state, action) //state: old state; action: sort of event, it may contains description or some data
{
  //calculate newState, here we mutate state into new state
  return newState;
}

todoStore = Redux.createStore(todoStoreReducer);//create a store which gets used by react components

todoStore.dispatch({ //dispatch: fire an action on the store 
  type: 'ADD_TODO',
  task,
});
```

#### Create a Redux store

Store hold the current state, pass the reducer with `const store = createStore(todoStore)`, here todoStoreReducer is a reducer

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

function todoStoreReducer(state = defaultState, action) {
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

export default createStore(todoStoreReducer); // Use createStore that we got from redux
```

## Action creator

JS funcitons that returns an action that has type and payload (data to pass to an action, it can be for example the library selected, and it is not necessary )

```
export const selectLibrary = ()=>{
    return{
        type:'select_library'
        payload:libraryId
    }
}
```



This is an action creator

```
 ()=>{
    return{
        type:'select_library'       
        payload:libraryId
    }
}
```



When we call the action creator, the returned action will be automatically dispatched for us and send to different reducers. 

Call action creator also means dispatch an action.



### Action creater Workflow:

User type something

Call Action Creater with new text

Action Creater returns an action

Action sent to all reducers

Reducer calculates new app state

State sent to all components

Conponents render with new state



## Sync PluralTodo component’s state with Redux state

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

# React-Redux 

```javascript
npm install --save react-redux
```
#### Container

**VisibleTodoList** filters the todos according to the current visibility filter and renders a`TodoList`

#### `containers/VisibleTodoList.js`

```react
import { connect } from 'react-redux'
import { toggleTodo } from '../actions'
import TodoList from '../components/TodoList'

const getVisibleTodos = (todos, filter) => {
  switch (filter) {
    case 'SHOW_ALL':
      return todos
    case 'SHOW_COMPLETED':
      return todos.filter(t => t.completed)
    case 'SHOW_ACTIVE':
      return todos.filter(t => !t.completed)
  }
}

const mapStateToProps = (state) => {
  return {
    todos: getVisibleTodos(state.todos, state.visibilityFilter)
  }
}

const mapDispatchToProps = (dispatch) => {
  return {
    onTodoClick: (id) => {
      dispatch(toggleTodo(id))
    }
  }
}

const VisibleTodoList = connect(
  mapStateToProps,
  mapDispatchToProps
)(TodoList)

export default VisibleTodoList
```

Async action with Redux use the [Redux Thunk middleware](https://github.com/gaearon/redux-thunk). 

 [Immutable](https://facebook.github.io/immutable-js/)

state is never to be modified. When changing state, create new objects instead. The spread (…) operator helps significantly





## Step by step :

1.  When app bootsup, redux create a new store with  `const store = createStore(reducers);`  with reducers, runs all the registered reducers, we got initial states.
2.  After we create store, we pass it to the provider, it will be persist for the rest of the application
3.  Provider is a component that aids to comminication between React and Redux.
4.  Connect function reach back to the provider and says 'please give me the access to the current state',
5.  The provider gives back the state that contains in the store ,
6.  When the connect helper first boots up, see the LibraryList is about to render, the helper goes up to the provider, to get access to the state, the provider response with yes.
7.  The helper calls  mapStateToProps, get application state returned, pass it to the props of the component



```javascript
import React, {Component} from 'react';
import {connect} from 'react-redux';

class LibraryList extends Component{
    render() {
        //To show that the state is mapped in props
   	    console.log(this.props)
        return;
    }
}

//Takes the global state and map it to props, the arg 'state' here contains the global state
const mapStateToProps = state =>{
    console.log(state);
    //with this return, we can find libraries in props.
	return {
      dataToshow: state.libraries
	}
} 

//connect() is a helper, it returns a function and is called immediately passing 'LibraryList' as arg. The second param is to bind to the component 
export default connect(mapStateToProps)(LibraryList);
```



## Connect

Is the window to the whole world of redux. 

We can use it to get application states and call action creator

Everytime we want to consume some state, we should use mapStateToProps

```
const mapStateToProps = state=>{
    return {
        selectedLibraryId:state.selectedLibraryId 
    }
}

export default connect(mapStateToProps, actions)(ListItem);

//the first arg is mapStateToProps, pass null if you do not have one 
//the second arg is to bind action creators to the component
```

#### Step by step use of connect helper for action

actions contains some action creators, whenever the action calls, 

the action is passed to the right place  

the action is passed to the component as args

#### mapStateToProps

mapStateToProps can receive the component's own props as the second param.

Every time the state changes, mapStateToProps function will rerun passing new state to the props, which cause the component to rerender 



## Provider

<Provider> can have only one child


```
const App = ()=>{

    //This is the store we create with redux's createStore method
    const store = createStore(reducers);

    // Provider is given the store as a prop
    return(
        <Provider store={store}>
            <View>
                <Header headerText='Tech Stack'/>
                <LibraryList/>
            </View>
        </Provider>

    )
}

export default App;
```



## Useful functions

### combineReducers

```
export default combineReducers({
  libraries: LibraryReducer,
  selectedLibraryId: SelectionReducer
});
```
Here declear the state name of all reducers. We we return a state from the reducer, it will be save with this name.



