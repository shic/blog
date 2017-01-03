---
layout:     post
title:      "WeChat Mini Program Development"
date:       2016-10-27 13:00:00
author:     "Shi"
---



# Lifecycle

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

### Page lifecycle

```javascript
  onLoad: function(){},

  onShow:function(){},

  onReady:function(){},

  onHide:function(){},

  onUnload:function(){},
  
```

goto page2 call onHide

back from page2 call page1 onShow and page2 onUnload

## Page switch

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



## Click event

- bindtap

  会触发底层 click event

  ```
  <view bindtap="viewClick2">
  ```

- catchtap

  不会触发底层 click event

  ```
  <view catchtap="viewClick2">
  ```

  ​

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





# 总结

https://github.com/justjavac/awesome-wechat-weapp



http://www.wxapp-union.com/article-964-1.html

http://blog.jobbole.com/106098/