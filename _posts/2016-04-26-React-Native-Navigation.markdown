---
layout:     post
title:      "Redux"
date:       2016-04-26 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# React Native Router Flux

### scene

type

Default is 'push'. 

replace 

tells navigator to replace current route with new route. 

actionSheet 

shows Action Sheet popup, you must pass callback as callback function, check Example for details. modal type inserts its 'component' after navigator component. It could be used for popup alerts as well for various needed processes before any navigator transitions (like login auth process).

switch 

is used for tab screens. 

reset 

is similar to replace except it unmounts the componets in the navigator stack. 

modal 

component could be dismissed by using Actions.dismiss() transitionToTop will reset router stack ['route.name'] and with animation, if route has sceneConfig. eg <Route name="login" schema="modal" component={Login} type="transitionToTop" />

https://github.com/aksonov/react-native-router-flux/blob/master/docs/API.md

https://github.com/aksonov/react-native-router-flux/blob/master/README2.md

