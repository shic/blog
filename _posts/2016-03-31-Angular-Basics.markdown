---
layout:     post
title:      "Angular Basics"
date:       2016-03-31 12:00:00
author:     "Shi"
---

# Develop environment

sudo npm install -g bower gulp karma-cli nodemon

1. bower: Package manager to load things like Angular
2. gulp: Test automation system
3. karma-cli: test 
4. nodemon: restart node everytime change file

## Sample Code

[Sample John Papa](https://github.com/johnpapa/ng-demos)



# Add a New API Call

## Service

```javascript
/*from app/scripts/services.js*/
    this.getWarehouseClientOrders = function(warehouseId,from,to){

        var promise = $http({
            url: server+'/warehouses/orders/clients/get',
            method: "POST",
            data:{
                auth:$rootScope.data.auth,
                warehouseId:warehouseId,
                from: from,
                to: to,
                orderIds:[]??? why add blank orderIds
            }
        });

        return promise;
    };
```

## Controller

```javascript
/*from app/warehouse/order-list/warehouse-order-list.js*/
        $scope.loadClientOrders = function () {

            APIService.getWarehouseClientOrders($rootScope.data.warehouse.id, [], $scope.from.getTime(), $scope.to.getTime()).then(
                function onSuccess(data) {
                    console.log(data.data);
                    $rootScope.data.clientOrders = data.data.orders;
                },
                function onError(data) {
                    $rootScope.showAPIError(data);
                });

        }

        return promise;
    };
```



# Notes

https://github.com/mariusbanea?utf8=%E2%9C%93&tab=repositories&q=angular&type=&language=

openerp 7
https://www.odoo.com
