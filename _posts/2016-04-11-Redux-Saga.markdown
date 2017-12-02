---
layout:     post
title:      "Redux Saga"
date:       2016-04-11 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# Install

```
npm install --save redux-saga
```

# About Redux Saga

Is a redux middleware

Consumes and emits actions

Maintains continuously running processes called saga

Used for manage async operations



A long running-background process

Responsible for applications' side effects 

Redux saga is the process manager

## How does it works?

Listern for actions and dispatches other actions to who listen for them using Effects

Interact with external APIs or modify system files using Request, Fs or other



# Implementation

## Add Saga middleware

```
import createSagaMiddleware from 'redux-saga'
const sagaMiddleware = createSagaMiddleware();
```



# Redux Saga VS Redux Thunk

Use yield and generator function to simplify asyn calls 



# Redux Saga Effects

Util method provided by Redux Saga

When you invoke an effect it returns an object that contains instructions for Redux Saga



`take, takeEvery, takeLatest` wait for a specific kind of action to create a new process

`call, fork, spawn` create new processes



`take, call` pause the execution of caller process, and others do not

## take

Wait for some event



Pause between concurrent lines of code 

When the action you specify is dispatched, the code resumes.

```Java
le mySaga = function*(){
  console.info('Saga begins');
  const state = yield effects.take('SET_STATE');
  console.info('Got state', state);
}

run(mySaga); //Output: Saga begins
dispatch({type:'SET_STATE', value:42}); //Output: Got state

```



```
    const { id }  = yield take(GET_CURRENT_USER_INFO);
```



## put

Put dispatches an action to the rest of the app

Like calling dispatch in Redux-Thunk or React-Redux

We can use 'put' to pass data.

```
i.e. 1:  
// The function that consumes the put
le mySaga = function*(){
  console.info('Saga begins');
  const state = yield effects.take('SET_STATE');
  console.info('Got state', state);
}

run(mySaga); //Output: Saga begins

// Dispatch an action
let putSaga = function*(){
  yield effects.put({type:'SET_STATE', value:42})
}

run(putSaga); //Output: Got state
```

```
i.e. 2:  
yield put(setCurrentUser(data));

```

## 

## takeEvery

Instead of taking an action once, it takes every time the specified action is dispatched, and every time it forks a new child process to handle it.



```

```



## 

## takeLatest

Combination of fork, takeEvery, and cancel.

It forks child process each time specified action is dispatched , while keeping exactly one instance of child process running at any time.

When the same action is dispatched , it cancels the previous call and fork a new child to complete the function call.

```

```





## select

When you yield to the select effect, it returns a copy of the application state. 

## call



```
    const response = yield call(fetch,`http://localhost:8081/user/${id}`);
```



## fork

Invoke specific method

Caller continues without pausing execution

Finnally block of forked method is invoked during cancellation



```Java
//Function fn is forked and the original fn functions continue run
yield effects.fork(fn);

```



```
yield items.map(items=>fork(loadItemDetails, item))

```





## spawn

Create a new process.

New process is not the child of caller - will not be cancelled if caller errors or is cancelled.



## cancel / cancelled

When you cancel a forked process, stops a forked process.

Stopped process will be cut off at most recent yield.

`finally` is invoked in forked process

```Java
let process = function*(){
  try{
    while (true){
      yield delay(500)
    }
  } finally {
    console.info('Cancelled?', effects.cancelled() );
  }
}

let saga = function*(){
  let forked = yield effects.fork(process);
  yield delay(5000);
  yield effects.cancel(forked);
}

run(saga);
```



 

## all

Combines numerous take statements into one.

Resumes when all actions have been dispatched.

```

```



## apply

Apply works like call, except it changes the scope of call



```
    const data = yield apply(response, response.json);
```



## call

Calls the specified method, equivalent to invoking the method directly, it is used for testing

```
const response = yield call(fetch,`http://localhost:8081/user/${id}`);
```







It creates a promise that resolves after some time.



If you put delay after yield keyword yield will pause the execution of the function for some time.



# Effective use of yield 



# Redux Saga Channels



## Action channel

**Buffer** actions to be processed one at a time 

Records all events of a specified type of events or actions

```
yield actionChannel('UPDATE')
```

##  

## Generic channel

Communicate between two sagas

```
let chan = yield channel();

```



## Event channel

Connects app to outside event sources (Websocket )



# Note

A fully-functional shopping cart built with Redux Saga using Yield : https://github.com/danielstern/redux-saga-cart