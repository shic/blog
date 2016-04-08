---
layout:     post
title:      "AngularJS Directive"
date:       2016-04-05 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---


# Directive

## Sample directive

#### Directive:





#### template search-result.html

```
    <div> {{ personName }}</div>
    <div> {{ personObject.name }}</div>
    <div> {{ formattedAddressFunction({ aperson: personObject }) }} </div>
    <div> <ng-transclude></ng-transclude></div> //replace the transclude contenent here
    <small ng-transclude></small>
   

```

#### Use template in main html:

Use as Element 
```
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

```
    <div search-result> </div>

    <button ngbk-focus ng-click="clickFocused()">
                        I'm very focuse
    </button>
```

#### The main controller could be 

```

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



