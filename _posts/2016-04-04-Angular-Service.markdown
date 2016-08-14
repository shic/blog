---
layout:     post
title:      "Angular Service"
date:       2016-04-04 12:00:00
author:     "Shi"
---


# Service

Service is a singlonton, once you create it, you can not change it

## Responsbilities

1. Handle non-view logic
2. Commuincate with the server
3. Hold data & state
4. Handle business logic


## Ways to create a service

- Value

1. Hold current state, any controller that want to access the state can include this service and show the same data

```javascript
app.value('schedule', {
  classes: [],
  addClass: function(newClass) {
    for(var i=0; i < this.classes.length; i++) {
      if(this.classes[i] === newClass) {
        return;
      }
    }
    this.classes.push(newClass);
  },
  dropClass: function(classToDrop) {
    for(var i=0; i < this.classes.length; i++) {
      if(this.classes[i] === classToDrop) {
        this.classes.splice(i, 1);
      }
    }
  }
})

app.controller('registrationCtrl',function($scope, schedule) {
  $scope.availableClasses = [{name:"Chemistry"},{name:"Physics"},{name:"History"},{name:"Biology"},]
  $scope.schedule = schedule;
});
```

2. Use as utils

```javascript
app.value('calculateGPA', function(title, credits, department, instructors) {
	//Do some calculation
    return '4.0';
})
```

- By service function (Bad way)

```javascript
angular.module('app').service('classRegistration',function() {
  return {
    title: 'Service form service'
  }
});

//Or in real case
app.service('classRegistration',function($http, policies) {
  return {
    register: function(newClass, student) {
      if(policies.canRegisterStudent(newClass, student)) {
        // implementation
      }
    }
  }
});
```

- Factory

Service and Factory basically do the same thing 

Has a receive function as the second parameter, it execute that function and caches the result, then return it

```javascript
function Course(title, credits, department, instructorIds, id) {
  this.title = title;
  this.credits = credits;
  this.department = department;
  this.instructorIds = instructorIds;
  this.id = id;
}
Course.prototype.displayName = function() {
  // code
}
// other class methods

app.factory('courseFactory', { function(title, credits, department, instructors) {
    var instructorIds = [];
    for(var i=0; i < instructors.length; i++) {
      instructorIds.push(instructors[i].id);
    }
    return new Course(title, credits, department, instructorIds, -1);
  }
})
//OR
app.value('courseFactory', {
  createCourse: function(title, credits, department, instructors) {
    var instructorIds = [];
    for(var i=0; i < instructors.length; i++) {
      instructorIds.push(instructors[i].id);
    }
    return new Course(title, credits, department, instructorIds, -1);
  }
})

app.controller('newCourseCtrl',function($scope, catalog, courseFactory) {
  $scope.register = function() {
    var newCourse = courseFactory.createCourse($scope.title, $scope.credits, $scope.department, $scope.instructors);
    catalog.add(newCourse);
  }
});
```

- Provider

Vantage to use provider is you can configuar it. (You can config your app once only)

Provider can create a service from a lower level

```javascript
var app = angular.module('app', []);

angular.module('app').controller('scheduleCtrl',function($scope, registration) {

  $scope.title = registration.title;
});
//Create config func which receive $provide parameter and call $get function
app.config(function($provide) {
  $provide.provider('registration', function() {
    var type;
    return {
      setType: function(value) {
        type = value;
      },
      $get: function() {
        return {
          title: 'Service from Provider ' + type
        }
      }
    }
  })
})

app.config(function(registrationProvider) {
  registrationProvider.setType('Angular');
})

```

# Angular default services

## $interval

### $interval(fn, delay, [count], [invokeApply], [Pass]);

- fn	function()	A function that should be called repeatedly.
- delay	number	Number of milliseconds between each function call.
- count	number	Number of times to repeat. If not set, or 0, will repeat indefinitely. (default: 0)

Ref: https://docs.angularjs.org/api/ng/service/$interval

## $watch

### $scope.$watch(watchExpression, [listener], [objectEquality]); 
- watchExpression, can be either a string expression or afunction. If the watchExpression value changes, the listener is invoked.
- listener takes a function which is invoked with three parameters namely newValue, oldValue, and the current scope. This is where we write logic to respond to the changes.

```javascript
function(n,o){console.log('Data changed!');

//Or
function (nVal) {
    if (nVal == $scope.currentExercise.duration) {
        var next = getNextExercise($scope.currentExercise);
	}
}
```

- objectEquality (default is set to false): 
	-false: the framework is not tracking internal object changes


## $location
for interacting with the browser’s location

## $route

for switching views based on location (URL) changes

	var someModule = angular.module('someModule', [...module dependencies...])
	someModule.config(function($routeProvider) {
		$routeProvider.
			when('url', {controller:aController, templateUrl:'/path/to/tempate'}).
			when(...other mappings for your app...).
	...
			otherwise(...what to do if nothing else matches...);
	)};


**$http , for communicating with servers.**


<h2>  Formatting with Filters</h2>

	{{12.9 | currency | number:0 }} //Output: $13


## Commminicating between Component

### Communicating with Events

```javascript
var app = angular.module('app', []);

app.controller('scCatalogCtrl', function($scope, catalog, $rootScope) {
  $scope.catalog = catalog;

  $scope.registerCourse = function(course) {
    $rootScope.$broadcast("course:registered", course); // $broadcast: Raise the event and send it downward to all child scope, so "scCatalogCtrl" can not raise event for "scScheduleCtrl", so we should bring in a dependency "$rootScope", then call "$broadcast"
    //$emit raises the event and send it up the scope chain
    course.registered = true;
  }

});

app.controller('scScheduleCtrl', function($scope, schedule) {
  $scope.schedule = schedule;

  $scope.$on('course:registered', function(event, course) { //Listen to the event with $on, the first param should be "event", add other params after 
    schedule.push({id: course.id, name: course.name, credits: course.credits});
  })
});

app.controller('scRegistrationCtrl',function($scope, toastr) {

  $scope.notify = function(msg) {
    toastr.success(msg);
    console.log(msg);
  }

  $scope.$on('course:registered', function(event, course) {
    $scope.notify('You have registered for ' + course.name);
  })

});
```
### Communicating with Service

```javascript
var app = angular.module('app', []);

app.factory('notifier', function(toastr) {
  return {
    notify: function(msg) {
      toastr.success(msg);
      console.log(msg);
    }
  }
});

app.factory('registration', function(schedule) {
  return {
    registerCourse: function(course) {
      schedule.push({id: course.id, name: course.name, credits: course.credits});
      course.registered = true;
    }
  }
})

app.controller('scCatalogCtrl', function($scope, catalog, registration, notifier) {
  $scope.catalog = catalog;

  $scope.registerCourse = function(course) {
    registration.registerCourse(course);
    notifier.notify('You have registered for ' + course.name);
  }

});

app.controller('scScheduleCtrl', function($scope, schedule) {
  $scope.schedule = schedule;
});

app.controller('scRegistrationCtrl',function($scope) {

});
```

## Promise

With a promise library, callbacks can be converted into:

```javascript
   Q.fcall(promisedStep1)
   .then(promisedStep2)
   .then(promisedStep3)
   .then(promisedStep4)
   .then(function (value4) {
       // Do something with value4
   })
   .catch(function (error) {
       // Handle any error from all above steps
}) .done();
```

Instead of using $watch service, sometimes it's better to use promise

```javascript
var startExercise = function (exercisePlan) {
        $scope.currentExercise = exercisePlan;
        $scope.currentExerciseDuration = 0;
        $interval(function () {
		++$scope.currentExerciseDuration;
	}, 1000, $scope.currentExercise.duration)
	//Use then when interval returns a promise
	.then(function () {
	            var next = getNextExercise(exercisePlan);
	            if (next) {
	                startExercise(next);
	            } else {
	                console.log("Workout complete!")
	            }
	});
};

```

