---
layout:     post
title:      "WeChat Mini Program Development"
date:       2016-10-27 13:00:00
author:     "Shi"
---



# Introduction

小程序开发指南

https://developers.weixin.qq.com/ebook?action=get_post_info&token=935589521&volumn=1&lang=zh_CN&book=miniprogram&docid=0008aeea9a8978ab0086a685851c0a



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

##wx:for

https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxml/list.html

### wx:key

如果列表中项目的位置会动态改变或者有新的项目添加到列表中，并且希望列表中的项目保持自己的特征和状态（如 `<input/>` 中的输入内容，`<switch/>` 的选中状态），需要使用 `wx:key` 来指定列表中项目的唯一的标识符。

`wx:key` 的值以两种形式提供

1. 字符串，代表在 for 循环的 array 中 item 的某个 property，该 property 的值需要是列表中唯一的字符串或数字，且不能动态改变。
2. 保留关键字 `*this` 代表在 for 循环中的 item 本身，这种表示需要 item 本身是一个唯一的字符串或者数字，如：

 

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

https://developers.weixin.qq.com/miniprogram/dev/api/share.html

# onPullDownRefresh

https://developers.weixin.qq.com/miniprogram/dev/api/pulldown.html

# 客服

https://developers.weixin.qq.com/miniprogram/introduction/custom.html

https://mpkf.weixin.qq.com/

# 模版消息

https://developers.weixin.qq.com/miniprogram/dev/api/notice.html



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






# 总结

https://github.com/justjavac/awesome-wechat-weapp



http://www.wxapp-union.com/article-964-1.html

http://blog.jobbole.com/106098/
