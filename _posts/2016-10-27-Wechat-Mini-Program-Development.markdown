---
layout:     post
title:      "WeChat Mini Program Development"
date:       2016-10-27 13:00:00
author:     "Shi"
---



# Lifecycle

## [App](https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/app.html)

### App lifecycle

```javascript
  onLaunch: function () {
    console.log('App Launch')
  },
  onShow: function () {
    console.log('App Show')
  },
  onHide: function () {
    console.log('App Hide')
  },

```

In app.js define globalData and global functions that can be used in every pages.

## [Page](https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/page.html)

### Page lifecycle

Page

```javascript
  onLoad: function(){},

  onShow:function(){},

  onReady:function(){},

  onHide:function(){},

  onUnload:function(){},
  
```

goto page2 call onHide

back from page2 call page1 onShow and page2 onUnload



# Lib

## 



# Page switch

### Ways

1. navigateTo

   display back button

   ```javascript
   wx.navigateTo(
   	url:"../logs/logs"
   )
   ```

   ```
   <navigate url="../logs/logs?id=100&title="this is a title">
   	<view/>
   </navigate>
   ```

   ​

2. redirectTo

   destory the previous page

   ```
   wx.redirectTo(
   	url:"../logs/logs"
   )
   ```

   ```
   <navigate url="../logs/logs?id=100" redirect>
   	<view/>
   </navigate>
   ```

   ​

3. navigation bar 

   hide page1

4. back 

   back will destory the current page by call onUnload

5. ​

   ​

### Pass data 

```
url:"../logs/logs?id=1"
  
 onLoad: function (options) {
    console.log(options.id)
 }
```


# Share

https://developers.weixin.qq.com/miniprogram/dev/api/qrcode.html



# Framework



https://github.com/Meituan-Dianping/mpvue



# WXS

https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxs/



# Tips：

## prevent page scroll

add `"disableScroll": true` to: pages->pageName.json



# [组件化编程](https://link.juejin.im/?target=https%3A%2F%2Fdevelopers.weixin.qq.com%2Fminiprogram%2Fdev%2Fframework%2Fcustom-component%2F)

从小程序基础库版本 [1.6.3](https://developers.weixin.qq.com/miniprogram/dev/framework/compatibility.html) 开始，小程序支持简洁的组件化编程。

https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/



# Components

## Click event

- bindtap

  会触发底层(下面几层) click event

  

  ```
  <view bindtap="viewClick2">
  ```

- catchtap

  不会触发底层(下面几层) click event

  ```
  <view catchtap="viewClick2">
  ```

  

- longPress

  

### event 包含了 currentTarget （绑定了事件的组件） 和 target（触发的组件）

#### currentTarget: dataset (包含了传入的data)

```javascript
<view bindtap="viewClick1" id="view1" data-title="news title" data-id="100">
    view 1
    <view bindtap="viewClick2">
        view 2
    </view>
</view>
  
  viewClick1: function(){
    console.log("view 1 click")
    event.dataset.title //news title
    event.dataset.id //100
  },
  
```



### Input

```
 type：text, number, idcard, digit
 
 userNameInput : function (event){
    this.setData({userName:event.detail.value})
  },
            
  <view><input bindinput="userNameInput" /></view>

```

### picker

**mode = selector**

**mode = time**

**mode = date**

### form

表单，将组件内的用户输入提交。

```
<switch/> <input/> <checkbox/> <slider/> <radio/> <picker/>

```



###  button

```
  size: default, mini
  type: primary, default, warn
  form-type：submit, reset
  <button class="login-btn" bindtap="loginBtnClick">登录</button>
  
  loginBtnClick:function (){
    // 用户名和密码验证的过程
    app.globalData.userInfo = {userName:this.data.userName,password:this.data.password}
    wx.redirectTo({url:"../home/home"})
  },

```

## swiper

This is an image slider

```
indicator-dots="true"
autoplay="true"
interval="3000" //显示时间
duration="1000" //滑动时间

<swiper indicator-dots="{{indicatorDots}}"
  autoplay="{{autoplay}}" interval="{{interval}}" duration="{{duration}}">
  <block wx:for="{{imgUrls}}">
    <swiper-item>
      <image src="{{item}}" class="slide-image" width="355" height="150"/>
    </swiper-item>
  </block>
</swiper>
```

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



# scroll-view

```java
scroll-y="true" 
upper-threshold="50"//distance to call the event
scroll-top="{{scrollTop}}" // goto some position

使用竖向滚动时，需要给<scroll-view/>一个固定高度，通过 WXSS 设置 height。

<scroll-view scroll-y="true" style="height: 200px;" bindscrolltoupper="scrolltoupper" bindscrolltolower="scrolltolower" bindscroll="scroll" scroll-into-view="{{toView}}" scroll-top="{{scrollTop}}">
    <view id="green" class="scroll-view-item bc_green"></view>
    <view id="red"  class="scroll-view-item bc_red"></view>
    <view id="yellow" class="scroll-view-item bc_yellow"></view>
    <view id="blue" class="scroll-view-item bc_blue"></view>
</scroll-view>

Page({
  data: {
    toView: 'red',
    scrollTop: 100
  },
  scrolltoupper: function(e) {
    console.log(e)
  },
  scrolltolower: function(e) {
    console.log(e)
  },
  scroll: function(e) {
    console.log(e)
  },
  tap: function(e) {
    for (var i = 0; i < order.length; ++i) {
      if (order[i] === this.data.toView) {
        this.setData({
          toView: order[i + 1]
        })
        break
      }
    }
  },
  tapMove: function(e) {
    this.setData({
      scrollTop: this.data.scrollTop + 10
    })
  }
})
```

### icon

```
    iconType: [
      'success', 'info', 'warn', 'waiting', 'safe_success', 'safe_warn',
      'success_circle', 'success_no_circle', 'waiting_circle', 'circle', 'download',
      'info_circle', 'cancel', 'search', 'clear'
    ]
    
<icon type="success" size="{{item}}" color:"green"/>

```

### progress

```
<progress percent="20" show-info active/>
```





# 总结

https://github.com/justjavac/awesome-wechat-weapp



http://www.wxapp-union.com/article-964-1.html

http://blog.jobbole.com/106098/
