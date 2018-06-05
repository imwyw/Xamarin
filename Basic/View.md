<!-- TOC -->

- [用户界面](#)
    - [视图](#)
        - [常用视图](#)
        - [View](#view)
        - [按钮](#)

<!-- /TOC -->

# 用户界面
## 视图
### 常用视图

视图 | 功能
---|---
UIView | 一个容器，是大部分用户界面控件的基本对象
UIButton | 按钮
UILabel | 标签，用于显示文本
UIImageView | 图像，用于显示图像
UITextField | 文本框，单行文本
UITextView | 文本，多行文本
UIScrollView | 滚动视图
UIPageView | 页面，不同页面的导航功能
UIAlertView | 警告，显示弹框

### View
创建新的单视图项目，从工具箱添加View控件到storyboard

![](..\assets\ui\ui-view-1.png)

视图默认为白色，模拟器中调试是看不到效果的，可以修改Background

![](..\assets\ui\ui-view-2.png)

在模拟器中调试效果如下：

![](..\assets\ui\ui-view-Simulator-1.png)

除了以上通过工具箱拖动控件的方式以外，我们还可以通过代码的方式进行View的添加设置。

首先删除上一步操作中添加的Background为黑色的空白view，如下：

![](..\assets\ui\ui-view-remove-1.png)

在ViewController中修改ViewDidLoad方法，如下：

```cs
public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.
    // Rectangle需要添加引用 using System.Drawing;

    UIView vv1 = new UIView();//实例化创建UIView对象
    vv1.Frame = new RectangleF(20, 20, 300, 200);//设置该view对象的位置
    vv1.BackgroundColor = UIColor.Blue;//设置背景颜色
    this.View.AddSubview(vv1);//此步不可省略，将当期视图对象添加到页面中，否则无法显示

    UIView vv2 = new UIView();
    vv2.Frame = new RectangleF(20, 240, 300, 200);
    vv2.BackgroundColor = UIColor.Orange;
    this.View.AddSubview(vv2);
}
```

调试后显示结果为：

![](..\assets\ui\ui_view_code_new.png)

### 按钮
按钮拖拽很简单，不再介绍。

通过代码进行添加：

```cs
public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    UIButton btn = new UIButton(UIButtonType.System);
    btn.SetTitle("测试按钮", UIControlState.Normal);
    btn.Frame = new Rectangle(120, 260, 80, 50);
    btn.BackgroundColor = UIColor.DarkGray;
    this.View.AddSubview(btn);
}
```


