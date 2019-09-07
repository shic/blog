---
layout:     post
title:      "iOS Development Fondamental"
date:       2016-08-03 12:00:00
author:     "Shi"
---



# ViewController Lifecycle

- init

- viewDidLoad

    - ViewController default view created
    - Create subviews here, we should put all view related initializations here

- viewWillAppear

    - subView will appear

- viewDidAppear

    - subView did appear

- viewWillDisappear

- viweDidDisappear

    

# UITabBarController

Used to controll Tab bar below

UITabBarController is used to manage (switch between) different ViewControllers

Contains all UIViewControllers needed and a UITabBar



UITabBarController should be created on app launch



- UITabBarController
    - viewControllers
    - UITabBar

Set tabBarItem

```
viewController1.tabBarItem.title = "";
viewController1.tabBarItem.image = UIImage...;
viewController1.tabBarItem.selectedImage = UIImage...;
```

# UINavigationController

Used to navigate and controll pages



- UINavigationController
    - viewControllers
    - UINavigationBar
        - backIndicatorImage
        - backBarButtonItem
            - image (left side)
            - title(right side)
        - title



Set navigationItem

```
viewController.navigationItem.title = "";
viewController.navigationItem.titleView = UIView...;
viewController.navigationItem.rightBarButtonItem = UIBarButtonItem...;
//Or 
viewController.navigationItem.rightBarButtonItems = [...];

viewController.navigationItem.leftBarButtonItem = UIBarButtonItem...;
//Or 
viewController.navigationItem.leftBarButtonItem = [...];


```

# UIWindow

If we use storyboard, system will create UIWindow for us



## Bottom tab does not change

- UIWindow
    - TabBarController
        - NavigationController1
            - ViewController
        - NavigationController2
            - ViewController

 

## Bottom tab changes

- UIWindow

    - NavigationController

        - TabBarController

            - ViewController1

            - ViewController2

```
UINavigationController navigationController;

navigationController.initWithRootViewController = tabBarController;

UIWindow window;
window.rootViewController = navigationController;
```



# Delegate

## Delegate creater

Offer a user some methods that can be implement

Use @optional/@required annotation to set if methods are optional or required

Offer delegate property

Run the methods in the right time

## Delegate user

Set `delegate = self` to received delegate methods

Implemente needed delegate methods



Used to handle some self defined actions

Es: should switch to a new viewController when clicked tab bar or should I start to play a video in the new viewController after finished tab bar switch, 



## How to do that?

Set myself as delegate receiver 

```
tabbarController.delegate = self;
```

Implement the method of tabbar (delegate)

```
shouldSelectViewController {
	return YES;
}

didSelectViewController {
	//play video
}
```



# UITableView

- UITableView
    - tableHeaderView
    - UITableViewCell
    - tableFooterView



```
UITableView tableView
view.addSubview(tableview)
```

required methods

```
numberOfRowsInSection->NSInteger

cellForRowAtIndexPath->UITableViewCell
```



# UIColletionView

## UICollectionViewLayout

- UICollecitonViewFlowLayout
    - minimumLineSpacing
    - minimumInteritemSpacing
    - itemSize (CGSizeMake)
    - indexPath



# UIScrollView

用于滚动展示 和图片Zoom

滚动展示：左右滑动展示不同板块

frame: scroll view的大小等属性

contentSize：内容大小

contentOffset：展示哪些内容（frame左上角到contentSize左上角的距离xy ）

常用属性

- UIScrollView
    - scrollEnabled
    - pagingEnabled
    - showHorizontalScrollIndicator
    - showVerticalScrollIndicator



常用delegate 方法

scrollViewDidScroll:开始滚动

scrollViewWillBeginDragging：开始拖拽

scrollViewDidEndDragging：结束拖拽



# UILabel

- UILabel
    - text
    - font
    - textColor
    - textAlignment
    - numberOfLines
    - lineBreakMode
        - NSLineBreakByClipping 根据宽度暴力截断
        - NSLineBreakByTruncatingMiddle 中间加...
        - NSLineBreakByTruncatingTail 最后加...
        - NSLineBreakByTruncatingHead 前面加...
    - sizeToFit 可变大小

# UIImage / UIImageView

UIImageView 展示 UIImage

- UIViewContentMode
    - ToFill 压缩图片到UIImageView的size
    - AspectFit 图片全展示
    - AspectFill 根据UIImageView切原始图片



# WKWebView

configuration: Cookie settings; Preference; Allow play video; JS inject ecc

loadRequest(NSURLRequest)

loadHTMLRequest

## WKNavigationDelegate

decidePolicyForNavigationAction : 是否加载请求

didFinishNavigation: 完成加载

didFailNavigation：加载失败

webViewWebContentProcessDidTerminate： crash回调（自动从新加载）





```
WKWebView webView = initWithFrame(CGRect)
addSubview(webView)
webView.loadRequest(NSURLRequest)
```





# Actions and Outlets

## outlet

from code to storyboard  (label)

Outlet is a property

## action

from storyboard to code  (if you want user interface element in your storyboard to cause something to happen in your code like button)

Action is a function

IBAction - stand for Interface Builder Action

# Key word Weak

Weak means we have only the ref of this object, we do not create it, do not control its lifecycle



# Xcode tips

## Suggestion:

Holding `Option Key`, then move mouse to where you want to get help

# Note

[Newsletter](https://iosdevweekly.com/)

