<!-- TOC -->

- [控制器](#控制器)
    - [导航控制器](#导航控制器)

<!-- /TOC -->

# 控制器
## 导航控制器

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

