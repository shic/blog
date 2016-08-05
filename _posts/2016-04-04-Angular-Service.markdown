---
layout:     post
title:      "Angular Service"
date:       2016-04-04 12:00:00
author:     "Shi"
---


# Service

## Responsbilities

1. Handle non-view logic
2. Commuincate with the server
3. Hold data & state


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
