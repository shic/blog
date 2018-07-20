---
layout:     post
title:      "WeChat Mini Program Design"
date:       2016-10-25 13:00:00
author:     "Shi"
---



# Official Guide

## Dimentions

Screens width: 750rpx

# view

hover-class



#### flex

##### container

```java
display: flex;
flex-direction:row;
flex-wrap:wrap; //nowrap: wrap-reverse
flex-flow:row wrap //equals to : flex-direction:row; && flex-wrap:wrap; 
justify-content: center //main direction: flex-start (default); flex-end; space-around; space-between
align-items: center //corss direction: flex-start (default); flex-end; stretch; baseline: 以元素所含第一行文字底线对其
```

##### element


```java
flex-grow: 0; //% of increase of the element when there are extra space, the other element should also have this property default:0
flex-shrink:1; // when space not enough, % of decrese. default 1. 0 means this element not shrink, 10 means shrink 10 times respect others.
flex-basis: 200rpx; //bug 200px works. space that the element occupy 
flex: 2 0 200rpx;

order: 3 //position of this element in the container
align-self: flex-end;
```

相对定位 (相对于自己来定位)

```
position: relative;
left: 150rpx;
top: 50rpx
```

绝对定位（相对于最近一个已经定位的父级元素来定位）

```
position: absolute;
left: 150rpx;
top: 50rpx
```


# WeUI

https://github.com/Tencent/weui-wxss/



## Docs



https://developers.weixin.qq.com/miniprogram/design/index.html?t=2018626



## Github Example Code

https://github.com/CFETeam/weapp-demo-album



https://github.com/CFETeam/weapp-demo-session



https://github.com/Tencent/weui-wxss





## My Style Guide

### font-size

32rpx

40rpx
