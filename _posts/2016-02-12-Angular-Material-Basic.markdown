---
layout:     post
title:      "AngularJS Basic"
subtitle:   "AngularJS study path"
date:       2015-10-10 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

<h1 class="section-heading">Angular Material 1.0.6</h1>

<h2>  Child Alignment</h2>
<h3>  Row</h3>
  layout-align=" horizontal vertical" 

>layout="row"       layout-align="center center" 

   AAA

>layout="row"       layout-align="space-around center"

_A_A_A__

>layout="row"       layout-align="space-between center"

A_A_A

<h3> Column</h3>
  
layout-align="vertical horizontal" 

>layout="row"       layout-align="center center" 

>layout="row"       layout-align="space-around center"


|
A
|
A
|

>layout="row"       layout-align="space-between center"



A
|
A

**All property:**
start (default)
center
end
space-around
space-between

More info: [Child Alignment
](https://material.angularjs.org/latest/layout/alignment) 

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

<h2>  Directive </h2>

	var appModule = angular.module('app', []);
	appModule.directive('ngbkFocus', function() {
	return {
	link: function(scope, element, attrs, controller) {
	element[0].focus();
	}
	};
	});

Usage

	<button ngbk-focus ng-click="clickFocused()">
                        I'm very focuse
	</button>