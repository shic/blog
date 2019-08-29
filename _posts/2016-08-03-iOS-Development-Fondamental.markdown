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



## Delegate user

Set 



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





# Xcode tips

## Suggestion:

Holding `Option Key`, then move mouse to where you want to get help

# Note

[Newsletter](https://iosdevweekly.com/)

