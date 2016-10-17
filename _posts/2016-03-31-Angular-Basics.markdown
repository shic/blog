---
layout:     post
title:      "Angular Basics"
date:       2016-03-31 12:00:00
author:     "Shi"
---

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




