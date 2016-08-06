---
layout:     post
title:      "Angular Controller"
date:       2016-04-03 12:00:00
author:     "Shi"
---

# Responsbilitites:

1. Setup the scope so that data can be bound to the view (Coordinate view and model)
2. Receive interaction from the view, and handle it

## Basic controller

```javascript
angular.module('app').controller('scheduleCtrl',function($scope, schedule) {
  $scope.schedule = schedule;

  $scope.register = function(newClass) {
    $scope.schedule.register(newClass);
  }
});
```

```javascript

```

```javascript

```

```javascript

```

