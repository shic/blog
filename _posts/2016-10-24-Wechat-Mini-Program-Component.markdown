---
layout:     post
title:      "WeChat Mini Program Component"
date:       2016-10-24 13:00:00
author:     "Shi"
---

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


