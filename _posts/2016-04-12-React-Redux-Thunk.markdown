---
layout:     post
title:      "React Redux Thunk"
date:       2016-04-11 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# *Redux Thunk*

https://codepen.io/stowball/post/a-dummy-s-guide-to-redux-and-thunk-in-react



`npm install --save redux-thunk`

To handle async action creators. 



Action Creator must **return a function** instead of action, this function will be called automatically with 'dispatch'. 



step by step

1. Action creator called 
2. Action creator returns a function
3. Redux thunk sees that we returned  a funcion and calls it with dispatch 
4. Wait for the async request to complete
5. Request conpleted,  .then function of the async request runs. 
6. Redux thunk now dispatch our action


