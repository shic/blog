---
layout:     post
title:      "Redux"
date:       2016-04-26 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# React Native Router Flux

        <Router>
            <Stack key="root">
                <Scene
                    key='login'
                    component={LoginForm}
                    title='Login'
                />
    
                <Scene
                    initial
                    key='employeeList'
                    component={EmployeeList}
                    title='Employees'
                />
            </Stack>
        </Router>
# Router



# Scene

How we organize the page. Router flux has a nav bar

key

component 

title

initial

## type

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



### Scene nesting

We you go between them, you will get automatically back button

```
<Scene key='main'>
	<Scene key='employeeLis' component={EmployeeList} />
	<Scene component={EmployeeDetail}/>
</Scene>
```

We can not goto the nested scene directly by call `Action.employeeList()`, we can only goes to parent scene calling  `Action.main()`,



### NavBar

Add `onRight and rightTitle` property to the Scene to show the right button on header

