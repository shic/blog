---
layout:     post
title:      "Angular View"
date:       2016-04-01 12:00:00
author:     "Shi"
---
# Avoid FOUC in views

Contents before view rendered

1. Add css code:

```css
[ng\:cloak], [ng-cloak], [data-ng-cloak], [x-ng-cloak], .ng-cloak, .x-ng-cloak {
  display: none !important;
}
```
2. Added directive in body
```html
<body ng-app="uper" onload="onload" ng-cloak="">
```
## Add loader

Since we are waiting for Angular to laod, so anything with ngHide attribute won't be hidden until Angular processes
```html

<body ng-app="uper" onload="onload">

<img src="images/logo-with-text.png" ng-hide="true">
<!-- Add your site or application content here -->
<div layout="column" layout-align="start center" layout-fill ng-cloak>
     <div id="header" ng-include="'views/header.html'" layout="row" layout-align="center center"></div>

     <div ng-view="" id="content" layout="column" layout-align="start center" flex></div>

     <div id="footer"></div>
</div>
```


