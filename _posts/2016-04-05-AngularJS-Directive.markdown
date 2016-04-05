---
layout:     post
title:      "Angular Directive"
date:       2015-04-05 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---


# Directive

## Sample directive

#### Directive:

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
            formattedAddressFunction:"&" // & for function 
        }
        
        compile: function(elem,attrs){
            console.log('Compiling...');
            //Edit html created
            elem.removeAttr('class');//remove classes in html
            return{
                pre:function(scope, elements, attrs){
                    //Avoid to use pre link! The date is 
                }

                post:function(elem,attrs){
                    //Aready generated html; Do some modification here 
                    if(scope){

                    }

                }

            }
        }
        link:
                
        restrict: 'AEC',//(A stand for Attribute; E for Element; C for Class; M for Commant), restrict this element to be used only when I use this in an element or attribute PS: default value is AE

    }
});


```
#### template search-result.html

```
    <div> {{ personName }}</div>
    <div> {{ personObject.name }}</div>
    <div> {{ formattedAddressFunction({ aperson: personObject }) }}</div>
   

```

#### Use template in main html:

Use as Element 
```
    //Pass a string
    <search-result person-name="{{ person.name}}"> </search-result>
    //Pass person.name from parent to variable persionName (Note : normalize of person-name)
        
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



