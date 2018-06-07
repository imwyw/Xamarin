<!-- TOC -->

- [控制器](#控制器)
    - [导航控制器](#导航控制器)
        - [Nav基本](#nav基本)
        - [Nav实现切换](#nav实现切换)

<!-- /TOC -->

# 控制器
## 导航控制器

### Nav基本
从“新建解决方案”对话框中，选择“iOS”>“应用”>“单视图应用程序”模板，确保选择了 C#。

新建项目名称为【NavDemo】，并添加视图控制器，名称为【MainViewController.cs】，如下：

![](..\assets\cont\nav_new_viewcont.png)

项目会添加对应的cs文件和xib文件，接下来主要修改AppDelegate代理文件。

![](..\assets\cont\nav_edit_appdel.png)

AppDelegate为整个应用的一个代理，提供程序启动、退出等类似监控的接口。 

修改【AppDelegate.cs】中FinishedLaunching方法，使应用程序从刚刚添加的View进行启动。

```cs
public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
{
    // Override point for customization after application launch.
    // If not required for your application you can safely delete this method

    Window = new UIWindow(UIScreen.MainScreen.Bounds);
    MainViewController mainViewCon = new MainViewController();
    mainViewCon.Title = "首页";
    UINavigationController nav = new UINavigationController(mainViewCon);
    Window.RootViewController = nav;
    Window.MakeKeyAndVisible();

    return true;
}
```

修改【MainViewController.cs】文件ViewDidLoad方法，修改View的背景色：
```cs
public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    View.BackgroundColor = UIColor.LightGray;
}
```

应用程序从MainViewController启动，运行结果：

![](..\assets\cont\nav_res_1.png)

### Nav实现切换
导航控制器提供了一种简单的途径，可以让用户在多个数据视图中导航，以及可以回到起点。

在上例的基础上继续添加两个视图控制器，分别为【ViewController1.cs】和【ViewController2.cs】，如图：

![](..\assets\cont\nav_new_viewcont_2.png)

最终显示效果如下，可以实现在多个视图间进行导航

![](..\assets\cont\nav2_res1.png)
![](..\assets\cont\nav2_res2.png)
![](..\assets\cont\nav2_res3.png)

1.修改【MainViewController.cs】文件，添加两个按钮，代码如下：
```cs
public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    //设置背景色
    View.BackgroundColor = UIColor.LightGray;

    //跳转FirstView按钮
    UIButton btn1 = new UIButton(UIButtonType.InfoLight);
    btn1.SetTitle("First View", UIControlState.Normal);
    btn1.Frame = new CGRect(100, 100, 150, 40);
    View.AddSubview(btn1);

    //跳转SecondView按钮
    UIButton btn2 = new UIButton(UIButtonType.InfoLight);
    btn2.SetTitle("Second View", UIControlState.Normal);
    btn2.Frame = new CGRect(100, 150, 150, 40);
    View.AddSubview(btn2);

    //添加监听
    btn1.TouchUpInside += (sender, e) =>
    {
        ViewController1 v1 = new ViewController1();
        v1.Title = "First View";
        this.NavigationController.PushViewController(v1, true);
    };

    //添加监听
    btn2.TouchUpInside += (sender, e) =>
    {
        ViewController2 v2 = new ViewController2();
        v2.Title = "Second View";
        this.NavigationController.PushViewController(v2, true);
    };
}
```

2.修改【ViewController1.cs】文件的ViewDidLoad方法，如下：
```cs
public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    View.BackgroundColor = UIColor.Green;

    //屏幕宽高
    nfloat width = UIScreen.MainScreen.Bounds.Width;
    nfloat height = UIScreen.MainScreen.Bounds.Height;

    UILabel label = new UILabel();
    label.Frame = new CGRect(100, 200, width - 200, 90);
    label.Text = "First View";
    label.TextAlignment = UITextAlignment.Center;
    label.Font = UIFont.SystemFontOfSize(37);
    View.AddSubview(label);

    UIButton btnBack = new UIButton();
    btnBack.SetTitle("返回", UIControlState.Normal);
    btnBack.Font = UIFont.SystemFontOfSize(18);
    btnBack.SetTitleColor(UIColor.Blue, UIControlState.Normal);
    btnBack.Frame = new CGRect(width - 100, height - 50, 100, 50);
    View.AddSubview(btnBack);

    btnBack.TouchUpInside += (sender, e) =>
    {
        this.NavigationController.PopToRootViewController(true);
    };
}
```

3.修改【ViewController2.cs】文件的ViewDidLoad方法，如下：
```cs
public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    View.BackgroundColor = UIColor.Purple;

    nfloat width = UIScreen.MainScreen.Bounds.Width;
    nfloat height = UIScreen.MainScreen.Bounds.Height;

    UILabel label = new UILabel();
    label.Text = "Second View";
    label.Font = UIFont.SystemFontOfSize(37);
    label.TextAlignment = UITextAlignment.Center;
    label.Frame = new CGRect(100, 200, width - 200, 90);
    View.AddSubview(label);

    UIButton btnBack = new UIButton();
    btnBack.SetTitle("返回", UIControlState.Normal);
    btnBack.Font = UIFont.SystemFontOfSize(18);
    btnBack.SetTitleColor(UIColor.Blue, UIControlState.Normal);
    btnBack.Frame = new CGRect(width - 100, height - 50, 100, 50);
    View.AddSubview(btnBack);

    btnBack.TouchUpInside += (sender, e) =>
    {
        this.NavigationController.PopToRootViewController(true);
    };
}
```