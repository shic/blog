---
layout:     post
title:      "React Boilerplate"
date:       2016-04-19 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# React-boilerplate

## Setting

1. npm i
2. npm start 
3. You can then open [http://localhost:3000](http://localhost:3000/) to access the server and see your app.

## Learning 

[Introduction](https://github.com/react-boilerplate/react-boilerplate/blob/master/docs/general/introduction.md)

### `app/`

We use the [container/component architecture](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0#.4rmjqneiw). `containers/` contains React components which are connected to the redux store. `components/` contains dumb React components which depend on containers for data. **Container components care about how things work, while components care about how things look.**

### `server/`

As the name suggests, this folder contains development and production server configuration.



## Lib

### Reselect

Reselect is a library used for slicing your redux state and providing only the relevant sub-tree to a react component. It has three key features:

1. Computational power

   While performing a search operation, reselect will filter the original array and return only matching usernames. Redux state does not have to store a separate array of filtered usernames.

2. Memoization

   A selector will not compute a new result unless one of its arguments change. 

3. Composability

   You can combine multiple selectors. For example, one selector can filter usernames according to a search key and another selector can filter the already filtered array according to gender. 



### **Middleware**

Middlewares are third party libraries which intercept each redux action dispatched to the redux store and then... do stuff. 

For example,  [`redux-logger`](https://github.com/evgenyrodionov/redux-logger) middleware will listen to all the actions being dispatched to the store and print previous and next state in the browser console. It's helpful to track what happens in your app.

#### **Router middleware:**

Keeps your routes in sync with the redux `store`

#### Redux Saga

Background process that handles multiple actions simultaneously, communicates with redux store and react containers at the same time







