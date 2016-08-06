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

- Service and Factory basically do the same thing 

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

Vantage to use provider is you can configuar it. 

Provider can create a service from a lower level


```javascript
var app = angular.module('app', []);


angular.module('app').controller('scheduleCtrl',function($scope, registration) {

  $scope.title = registration.title;
});

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

**$location , for interacting with the browser’s location, **

**$route , for switching views based on location (URL) changes**

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

	{{12.9 | currency | number:0 }}
displays: $13
