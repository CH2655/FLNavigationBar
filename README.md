# FLNavigationBar
一个用来统一管理导航栏转场以及当 push 或者 pop 的时候使动画效果更加顺滑的通用库，并且同时支持竖屏和横屏。能应对复杂的场景变化，又兼顾原生NavigationBar的使用习惯

## 效果图
| Feature |Demo||
|---|---|---|
|Color -> Color|![](https://github.com/ForterLi/ProjectResource/blob/master/FLNavigationBar/Screenshots/0000001.gif)|![](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1566398321230&di=d07d26c83a012b739b31e42b8f208ef1&imgtype=0&src=http%3A%2F%2Fcdn.fds.api.xiaomi.com%2Fb2c-bbs%2Fcn%2Fattachment%2F2539da2623a8bed2cb9c48f4575ad8c3.jpg)|
|Alone Bar -> Alone Bar|![](https://github.com/ForterLi/ProjectResource/blob/master/FLNavigationBar/Screenshots/0000002.gif)||
|Color -> Image Bar|![](https://github.com/ForterLi/ProjectResource/blob/master/FLNavigationBar/Screenshots/0000003.gif)||
|Hidden -> BlurEffectStyleLight|![](https://github.com/ForterLi/ProjectResource/blob/master/FLNavigationBar/Screenshots/0000004.gif)||


## 介绍

本库的设计理念是使用者只用关心当前 view controller 导航栏的背景样式
在当前 view controller的 UINavigationItem 中配置页面导航栏样式

## 使用说明
导航栏样式
```objc
typedef NS_ENUM(NSInteger, FLBarStyle) {
    FLBarStyleNone = 0,               // 公共样式
    FLBarStyleDefault = 0xff,         // 默认毛玻璃效果
    FLBarStyleColor,                  // 颜色
    FLBarStyleTransparent,            // 透明
    FLBarStyleHidden,                 // 隐藏
    FLBarStyleTranslucent,            // 毛玻璃效果可以修改样式
};

typedef NS_ENUM(NSInteger, FLBlurEffectStyle) {
    FLBlurEffectStyleNone = 0,
    FLBlurEffectStyleExtraLight,
    FLBlurEffectStyleLight,
    FLBlurEffectStyleDark
};
```

推荐在navigation conreoller 中配置导航栏默认样式，如果不配置默认默认为 FLBarStyleDefault 半透明样式
``` swift
    override func loadView() {
        super.loadView()
        self.barStyle = .color
        self.barBackgroundColor = UIColor.white
        self.barLineColor = UIColor.white
        self.barStyleUpdate()
    }
```
在每一个view controller 中配置单独配置每个页面的样式
```swift
    // MARK: - Life Cycle
    override func loadView() {
        super.loadView()
        self.navigationItem.yq_barStyle = .color
        self.navigationItem.yq_barLineColor = .red
        self.navigationItem.yq_barBackgroundColor = .yellow
    }
```

每一个view controller单独配置页面独有的 NavigationBar
```swift 
    override func viewDidLoad() {
        super.viewDidLoad()
        addAloneBarNavigationBar()
    }
    
    override func viewDidLayoutSubviews() {
        aloneBarViewDidLayoutSubviews()
    }
```
```swift
    // 当前Alone bar 与 UINavigationBar 一样，无法使用yq_barStyle、yq_barLineColor、yq_barBackgroundColor等扩展属性
    self.alone_barNavigationBar
    // 等价 self.navigationItem
    self.alone_navigationItem
```
## 安装

### CocoaPods

你可以用以下命令来安装最新版的 CocoaPods：

```bash
$ gem install cocoapods
```

在 `podfile` 中添加以下代码：

```ruby
pod 'FLNavigationBar'
```

然后在终端运行以下命令：

```bash
$ pod install
```
## 基本要求

- iOS 8.0+

## 许可证

FLNavigationBar 是基于 MIT 许可证下发布的，详情请参见 LICENSE。
