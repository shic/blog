---
layout:     post
title:      "Angular Directive"
date:       2016-04-06 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---
{% raw %}

# Directive

## Responsbilities

1. Manipulate DOM
2. Receive view events: translating view events into calls on the scope

## Naming

Prefix your directive like "up"(upSearchResult) to avoid name collision

## Purpose

- Widget


- DOM Events
ng-click

- Functionality
ng-show

## Sample directive 1

#### Directive:

```javascript
myApp.directive("searchResult", function (){
    return{
        template:'<div></div>',
        templateUrl:'path/search-result.html',
        controller: 'SearchCtrl',
        controllerAs: 'vm',
        replace: 'true', // Replace all the properties in this tag (default is false) e.g. http://plnkr.co/edit/uQGHI1?p=preview 
        // Isolate the scope, local scope binding
        // If you delete this, this directive will share the parent's scope
        scope:{
            personName:"@" // @ for text, one way binding 
            personObject:"=" // = for object,  two way binding
            formattedAddressFunction:"&" // & for function 
        },
        transclude:true,
        
        //Include the parent directive
        require:'^nameOfParentDirective'
                
        //Link is a useful short version of compile-post (Put some function here for the directive to use)
        link: function(scope, elements, attrs, ctrl){//add controller of the parent directive as the last parameter
            scope.viewClassDetail = function(classToView){
                //do something
            }
        }

        compile: function(elem,attrs){
            console.log('Compiling...');
            //Edit html created
            elem.removeAttr('class');//remove classes in html
            return{
                pre:function(scope, elements, attrs){
                    //Avoid to use pre link! The date is 
                }

                post:function(scope, elements, attrs){
                    //Aready generated html; Do some modification here 
                    if(scope.personObject.name == "Jane Doe"){
                        elements.removeAttr('class');
                    }

                }

            }
        }
                
        restrict: 'AEC',//(A stand for Attribute; E for Element; C for Class; M for Commant), restrict this element to be used only when I use this in an element or attribute PS: default value is AE

    }
});
```

#### template search-result.html

```html
    <div> {{ personName }}</div>
    <div> {{ personObject.name }}</div>
    <div> {{ formattedAddressFunction({ aperson: personObject }) }} </div>
    <div> <ng-transclude></ng-transclude></div> //replace the transclude contenent here
    <small ng-transclude></small>
   

```

#### Use template in main html:

Use as Element 

```html
    //Pass a string
    <search-result person-name="{{ person.name}}"> 
        Search results may not be valid.
    </search-result>    //Pass person.name from parent to variable personName (Note : normalize of person-name)
        
    //Pass an object
    <search-result person-object="person"> </search-result>
    
    //Pass a function 
    //the parameter here aperson is a simbolic parameter, it should be specified in template; we should pass Object Map (person-object="person") instead of pure object.
    <search-result person-object="person" formatted-address-function="formattedAddress(aperson)"></search-result>


```
or as Attribute

```html
<div search-result> </div>
<button ngbk-focus ng-click="clickFocused()">
    I'm very focuse
</button>
```

#### The main controller could be 

```javascript
myApp.controller('mainController', ['$scope', '$log', function($scope, $log) {
    
    $scope.person = {
        name: 'John Doe',
        address: '555 Main St.',
        city: 'New York',
        state: 'NY',
        zip: '11111'
    }
    
    $scope.formattedAddress = function(person) {
      
        return person.address + ', ' + person.city + ', ' + person.state + ' ' + person.zip;
        
    };
    
}]);

``` 

## Sample directive 2 (Real case usage)
### JS

```javascript
var app = angular.module('app', []);

app.value('scFollowedInstructors', []);

app.controller('scInstructorsCtrl', function($scope, scFollowedInstructors) {
  $scope.followedInstCount = scFollowedInstructors.length;

  this.followInstructor = function(instructor) {
    scFollowedInstructors.push(instructor);
    $scope.followedInstCount = scFollowedInstructors.length;
  }
});

app.directive('scInstructors', function() {
  return {
    restrict: 'E',
    replace: true,
    template: '<div class="well sidebar-nav">' +
        '<h3>Instructors ({{followedInstCount}} followed)</h3>' +
        '<div class="row" ng-repeat="instructor in instructorList">' +
        '<div class="col-md-6">{{instructor.name}}</div>' +
        '<div class="col-md-6"><sc-follow-instructor instructor-to-follow="instructor" /></div>' + //Pass "instructor-to-follow" to the scope here
        '</div>' +
        '</div>',
    controller: 'scInstructorsCtrl'
  }
});

app.directive('scFollowInstructor', function(/*scFollowedInstructors*/) {
  return {
    restrict: 'E',
    replace: true,
    template: '<div class="instructor-follow-button"><button ng-click="followInstructor()" class="btn btn-info btn-xs">Follow</button></div>',
    scope: {
      instructorToFollow: '='
    },
    require: '^scInstructors',
    link: function(scope, element, attrs, ctrl) { // Added the last param "ctrl" because we include the parent directive with "require: '^scInstructors'"
      scope.followInstructor = function() {
        ctrl.followInstructor(scope.instructorToFollow); 
        //the function "followInstructor" is in "scInstructorsCtrl"; 
        //the param "scope.instructor" is defined in " instructor: '=' "
        element.css('display', 'none');
      }
    }
  }
});

angular.module('app').controller('scheduleCtrl',function($scope) {
  $scope.instructorList = [
    {id: 1, name: 'Professor Snape'},
    {id: 2, name: 'Provessor McGonagall'},
    {id: 3, name: 'Professor Dumbledore'}
  ]
});
```

## Sample directive 3 (Real case usage)
```javascript
var app = angular.module('app', []);

app.value('scFollowedInstructors', []);


app.controller('scInstructorsCtrl', function($scope, scFollowedInstructors) {
  $scope.scFollowedInstructors = scFollowedInstructors;
});

app.directive('scInstructors', function() {
  return {
    restrict: 'E',
    replace: true,
    templateUrl: 'scInstructors.html',
    controller: 'scInstructorsCtrl'
  }
});

app.directive('scFollowInstructor', function(scFollowedInstructors) {
  return {
    restrict: 'E',
    replace: true,
    templateUrl: 'scFollowInstructor.html',
    scope: {
      instructorToFollow: '='
    },
    link: function(scope, element, attrs, ctrl) {
      scope.followed = function() {
        return scFollowedInstructors.indexOf(scope.instructorToFollow) > -1;
      }
      scope.followInstructor = function() {
        scFollowedInstructors.push(scope.instructorToFollow);
      }
      scope.unFollowInstructor = function() {
        scFollowedInstructors.splice(scFollowedInstructors.indexOf(scope.instructorToFollow), 1);
      }
    }
  }
});

angular.module('app').controller('scheduleCtrl',function($scope) {
  $scope.instructorList = [
    {id: 1, name: 'Professor Snape'},
    {id: 2, name: 'Provessor McGonagall'},
    {id: 3, name: 'Professor Dumbledore'}
  ]
});
```
### instructors
```html
<div class="well sidebar-nav">
  <h3>Instructors ({{scFollowedInstructors.length}} followed)</h3>
  <div class="row" ng-repeat="instructor in instructorList">
    <div class="col-md-6">{{instructor.name}}</div>
    <div class="col-md-6"><sc-follow-instructor instructor-to-follow="instructor" /></div>
  </div>
</div>
```
scFollowInstructor.html

```html
<div class="instructor-follow-button">
  <button ng-show="followed()" ng-click="unFollowInstructor()" class="btn btn-info btn-xs">Unfollow</button>
  <button ng-hide="followed()" ng-click="followInstructor()" class="btn btn-info btn-xs">Follow</button>
</div>

```

{% endraw %}



