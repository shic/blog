---
layout:     post
title:      "AngularJS Directive"
date:       2016-04-06 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---
{% raw %}

# Directive

## Sample directive

#### Directive:


```javascript
myApp.directive("searchResult", function (){
    return{
        template:'<div></div>',
        templateUrl:'path/search-result.html',
        controller: 'SearchCtrl',
        controllerAs: 'vm',
        replace: 'true',
        // Isolate the scope, local scope binding
        scope:{
            personName:"@" // @ for text, one way binding 
            personObject:"=" // = for object,  two way binding
            formattedAddressFunction:"&" // & for function 
        },
        transclude:true,
        //Link is a useful short version of compile-post 
        link: function(scope, elements, attrs){
            //Aready generated html; Do some modification here 
            if(scope.personObject.name == "Jane Doe"){
                elements.removeAttr('class');
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

{% endraw %}



