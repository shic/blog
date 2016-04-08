---
layout:     post
title:      "AngularJS Directive"
date:       2016-04-06 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# Directive

## Sample directive

#### Directive:


```
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
<div> { { personName } }</div>
<div> {{ personName }}</div>

```
	<div> {{ personName }}</div>
