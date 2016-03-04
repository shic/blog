---
layout:     post
title:      "AngularJS Basic"
subtitle:   "AngularJS study path"
date:       2015-10-10 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

<h2 class="section-heading">Services</h2>

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