---
layout:     post
title:      "AngularJS Basic"
subtitle:   "AngularJS study path"
date:       2015-10-10 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---


#　Service

Service and Factory basically do the same thing



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

# Directive

## Sample directive

In javascript:

```javascript
myApp.directive("searchResult", function (){
	return{
		template:'<div></div>'
		templateUrl:'path/search-result.html'
		replace: 'true'
		// Isolate the scope, local scope binding
		scope:{
			personName:"@" // @ for text, one way binding 
			personObject:"=" // = for object,  two way binding 
		}
		
		link:
		 		
		restrict: 'AEC',//(A stand for Attribute; E for Element; C for Class; M for Commant), restrict this element to be used only when I use this in an element or attribute PS: default value is AE

	}
});


```
### template search-result.html

```
	<div> {{personName}}</div>
	<div> {{personObject.name}}</div>

```

### Use template in main html:

Element 
```
	//Pass a string
	<search-result person-name="{{ person.name}}"> </search-result>
	//Pass person.name from parent to variable persionName (Note : normalize of person-name)
		
	//Pass an object
	<search-result person-object="person"> </search-result>
	

```
or Attribute

```
	<div search-result> </div>

	<button ngbk-focus ng-click="clickFocused()">
                        I'm very focuse
	</button>
```

Usage


## Pipe

	<md-list-item ng-repeat="user in vm.users | filter:vm.searchText | orderBy: 'name'">

## Useful functions

### To upper case

	$scope.formattedName= $filter('uppercase')($scope.name);


# Controller

## Routing template 

``` 
$routeProvider.when('/some-route/:num', {
	templateUrl: 'some-url.html',
	controller: 'someCtrl'
})

myApp.controller('someCtrl', ['$scope', '$routeParams',
function($scope, $routeParams){
	$scope.num = $routeParams.num;
}])
```









# Component

Costome directive

```


```





























