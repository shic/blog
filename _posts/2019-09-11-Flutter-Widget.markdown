---
layout:     post
title:      "Flutter Widget"
date:       2019-09-11 12:00:00
author:     "Shi"

---



# Flutter Widget

# Widgets

## Text

```

Text(
  '用来显示一段特定样式的字符串，就比如Android里的TextView，或是iOS中的UILabel。',
  textAlign: TextAlign.center,//居中显示
  style: TextStyle(fontWeight: FontWeight.bold, fontSize: 20, color: Colors.red),//20号红色粗体展示
);
```



### 混合展示样式

```

TextStyle blackStyle = TextStyle(fontWeight: FontWeight.normal, fontSize: 20, color: Colors.black); //黑色样式

TextStyle redStyle = TextStyle(fontWeight: FontWeight.bold, fontSize: 20, color: Colors.red); //红色样式

Text.rich(
    TextSpan(
        children: <TextSpan>[
          TextSpan(text:'文本是视图系统中常见的控件，它用来显示一段特定样式的字符串，类似', style: redStyle), //第1个片段，红色样式 
          TextSpan(text:'Android', style: blackStyle), //第1个片段，黑色样式 
          TextSpan(text:'中的', style:redStyle), //第1个片段，红色样式 
          TextSpan(text:'TextView', style: blackStyle) //第1个片段，黑色样式 
        ]),
  textAlign: TextAlign.center,
);
```



## Image

加载本地资源图片，如 Image.asset(‘images/logo.png’)；

加载本地（File 文件）图片，如 Image.file(new File(’/storage/xxx/xxx/test.jpg’))；

加载网络图片，如 Image.network('http://xxx/xxx/test.gif') 。



填充模式 fit、拉伸模式 centerSlice、重复模式 repeat 等属性

### FadeInImage

FadeInImage 控件提供了图片占位的功能，并且支持在图片加载完成时淡入淡出的视觉效果。此外，由于 Image 支持 gif 格式，我们甚至还可以将一些炫酷的加载动画作为占位图。

```
FadeInImage.assetNetwork(
  placeholder: 'assets/loading.gif', //gif占位
  image: 'https://xxx/xxx/xxx.jpg',
  fit: BoxFit.cover, //图片拉伸模式
  width: 200,
  height: 200,
)
```



### CachedNetworkImage

https://pub.dev/packages/cached_network_image/



## Button

Flutter 提供了三个基本的按钮控件，即 FloatingActionButton、FlatButton 和 RaisedButton。

```
FloatingActionButton(onPressed: () => print('FloatingActionButton pressed'),child: Text('Btn'),);
FlatButton(onPressed: () => print('FlatButton pressed'),child: Text('Btn'),);
RaisedButton(onPressed: () => print('RaisedButton pressed'),child: Text('Btn'),);
```



```
FlatButton(
    color: Colors.yellow, //设置背景色为黄色
    shape:BeveledRectangleBorder(borderRadius: BorderRadius.circular(20.0)), //设置斜角矩形边框
    colorBrightness: Brightness.light, //确保文字按钮为深色
    onPressed: () => print('FlatButton pressed'), 
    child: Row(children: <Widget>[Icon(Icons.add), Text("Add")],)
)；
```



## ListView

### 构造函数 ListView.builder

适用于子 Widget 比较多的场景。这个构造函数有两个关键参数：

- itemBuilder，是列表项的创建方法。当列表滚动到相应位置时，ListView 会调用该方法创建对应的子 Widget
- itemCount，表示列表项的数量，如果为空，则表示 ListView 为无限列表。



```
ListView.builder(
    itemCount: 100, //元素个数
    itemExtent: 50.0, //列表项高度
    itemBuilder: (BuildContext context, int index) => ListTile(title: Text("title $index"), subtitle: Text("body $index"))
);
```

itemExtent 并不是一个必填参数。但对于定高的列表项元素，我强烈建议你提前设置好这个参数的值。因为如果这个参数为 null，ListView 会动态地根据子 Widget 创建完成的结果，决定自身的视图高度，以及子 Widget 在 ListView 中的相对位置。在滚动发生变化而列表项又很多时，这样的计算就会非常频繁。

### ListView.separated

与 ListView.builder 抽离出了子 Widget 的构建方法类似，ListView.separated 抽离出了分割线的创建方法 separatorBuilder，以便根据 index 设置不同样式的分割线。

```
//使用ListView.separated设置分割线
ListView.separated(
    itemCount: 100,
    separatorBuilder: (BuildContext context, int index) => index %2 ==0? Divider(color: Colors.green) : Divider(color: Colors.red),//index为偶数，创建绿色分割线；index为奇数，则创建红色分割线
    itemBuilder: (BuildContext context, int index) => ListTile(title: Text("title $index"), subtitle: Text("body $index"))//创建子Widget
)
```



## CustomScrollView

用来处理多个需要自定义滚动效果的 Widget。在 CustomScrollView 中，这些彼此独立的、可滚动的 Widget 被统称为 Sliver。

```
CustomScrollView(
  slivers: <Widget>[
    SliverAppBar(//SliverAppBar作为头图控件
      title: Text('CustomScrollView Demo'),//标题
      floating: true,//设置悬浮样式
      flexibleSpace: Image.network("https://xx.jpg",fit:BoxFit.cover),//设置悬浮头图背景
      expandedHeight: 300,//头图控件高度
    ),
    SliverList(//SliverList作为列表控件
      delegate: SliverChildBuilderDelegate(
            (context, index) => ListTile(title: Text('Item #$index')),//列表项创建方法
        childCount: 100,//列表元素个数
      ),
    ),
  ]);
```



## ScrollController 与 ScrollNotification

### ScrollController

与 ListView 绑定，进行滚动信息的监听，进行相应的滚动控制

首先，我们在 State 的初始化方法里，创建了 ScrollController，并通过 _controller.addListener 注册了滚动监听方法回调，根据当前视图的滚动位置，判断当前是否需要展示“Top”按钮。随后，在视图构建方法 build 中，我们将 ScrollController 对象与 ListView 进行了关联，并且在 RaisedButton 中注册了对应的回调方法，可以在点击按钮时通过 _controller.animateTo 方法返回列表顶部。最后，在 State 的销毁方法中，我们对 ScrollController 进行了资源释放。



### ScrollNotification

通过将 ListView 纳入子 Widget，实现滚动事件的获取。

# 传递数据

对于数据的跨层传递，Flutter 还提供了三种方案：InheritedWidget、Notification 和 EventBus。

## InheritedWidget

InheritedWidget 的数据流动方式是从父 Widget 到子 Widget 逐层传递

对于视图层级比较深的 UI 样式，直接通过属性传值的方式会导致很多中间层增加冗余属性，而使用 InheritedWidget 可以实现子 Widget 跨层共享父 Widget 的属性。需要注意的是，InheritedWidget 中的属性在子 Widget 中只能读，如果有修改的场景，我们需要把它和 StatefulWidget 中的 State 配套使用。

### 使用方法

首先，为了使用 InheritedWidget，我们定义了一个继承自它的新类 CountContainer。

然后，我们将计数器状态 count 属性放到 CountContainer 中，并提供了一个 of 方法方便其子 Widget 在 Widget 树中找到它。

最后，我们重写了 updateShouldNotify 方法，这个方法会在 Flutter 判断 InheritedWidget 是否需要重建，从而通知下层观察者组件更新数据时被调用到。在这里，我们直接判断 count 是否相等即可。

```dart
class CountContainer extends InheritedWidget {
  //方便其子Widget在Widget树中找到它
  static CountContainer of(BuildContext context) => context.inheritFromWidgetOfExactType(CountContainer) as CountContainer;
  
  final int count;

  CountContainer({
    Key key,
    @required this.count,
    @required Widget child,
  }): super(key: key, child: child);

  // 判断是否需要更新
  @override
  bool updateShouldNotify(CountContainer oldWidget) => count != oldWidget.count;
}
```

我们使用 CountContainer 作为根节点，并用 0 初始化 count。随后在其子 Widget Counter 中，我们通过 InheritedCountContainer.of 方法找到它，获取计数状态 count 并展示：

```dart
class _MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
   //将CountContainer作为根节点，并使用0作为初始化count
    return CountContainer(
      count: 0,
      child: Counter()
    );
  }
}

class Counter extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    //获取InheritedWidget节点
    CountContainer state = CountContainer.of(context);
    return Scaffold(
      appBar: AppBar(title: Text("InheritedWidget demo")),
      body: Text(
        'You have pushed the button this many times: ${state.count}',
      ),
    );
}
```



## Notification

数据流动方式是从子 Widget 向上传递至父 Widget。这样的数据传递机制适用于子 Widget 状态变更，发送通知上报的场景。

Notification，这种由下到上传递数据的跨层共享机制。我们可以使用 NotificationListener，在父 Widget 监听来自子 Widget 的事件。

如果想要实现自定义通知，我们首先需要继承 Notification 类。Notification 类提供了 dispatch 方法，可以让我们沿着 context 对应的 Element 节点树向上逐层发送通知。

### 使用方法

子 Widget 是一个按钮，在点击时会发送通知

```dart

class CustomNotification extends Notification {
  CustomNotification(this.msg);
  final String msg;
}

//抽离出一个子Widget用来发通知
class CustomChild extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return RaisedButton(
      //按钮点击时分发通知
      onPressed: () => CustomNotification("Hi").dispatch(context),
      child: Text("Fire Notification"),
    );
  }
}
```

父 Widget 中，我们监听了这个通知，一旦收到通知，就会触发界面刷新，展示收到的通知信息：

```dart

class _MyHomePageState extends State<MyHomePage> {
  String _msg = "通知：";
  @override
  Widget build(BuildContext context) {
    //监听通知
    return NotificationListener<CustomNotification>(
        onNotification: (notification) {
          setState(() {_msg += notification.msg+"  ";});//收到子Widget通知，更新msg
        },
        child:Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[Text(_msg),CustomChild()],//将子Widget加入到视图树中
        )
    );
  }
}
```

## EventBus

EventBus 是一个第三方插件

无论是 InheritedWidget 还是 Notificaiton，它们的使用场景都需要依靠 Widget 树，也就意味着只能在有父子关系的 Widget 之间进行数据共享。但是，组件间数据传递还有一种常见场景：这些组件间不存在父子关系。这时，事件总线 EventBus 就登场了。

当发布者触发事件时，订阅者和发布者之间可以通过事件进行交互。发布者和订阅者之间无需有父子关系，甚至非 Widget 对象也可以发布 / 订阅。



# Note





# Book



