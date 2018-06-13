<!-- TOC -->

- [用户界面](#用户界面)
    - [视图](#视图)
        - [常用视图](#常用视图)
        - [UIView](#uiview)
            - [工具拖拽](#工具拖拽)
            - [代码进行添加设置](#代码进行添加设置)
        - [UIButton](#uibutton)
            - [工具箱拖拽](#工具箱拖拽)
            - [通过代码进行维护](#通过代码进行维护)
            - [按钮的响应](#按钮的响应)
        - [UIImageView](#uiimageview)
            - [基本](#基本)
            - [ContentMode显示模式](#contentmode显示模式)
        - [UILabel](#uilabel)
        - [结合UITextField实现登陆框](#结合uitextfield实现登陆框)
        - [键盘UIKeyboardType](#键盘uikeyboardtype)
            - [类型](#类型)
            - [显示键盘改变输入视图位置](#显示键盘改变输入视图位置)
        - [进度条UIProgressView](#进度条uiprogressview)
        - [滚动视图UIScrollView](#滚动视图uiscrollview)
            - [滚动](#滚动)
            - [滚动事件](#滚动事件)
        - [页面控件UIPageControl](#页面控件uipagecontrol)
        - [警告UIAlertView](#警告uialertview)
            - [title](#title)
            - [button](#button)
            - [button-click](#button-click)
        - [UITableView](#uitableview)
            - [简单实例](#简单实例)
            - [设置Table](#设置table)
            - [Table风格](#table风格)
        - [一次修改相同的视图](#一次修改相同的视图)

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

### UIView
#### 工具拖拽
创建新的单视图项目，从工具箱添加View控件到storyboard

![](..\assets\ui\ui-view-1.png)

视图默认为白色，模拟器中调试是看不到效果的，可以修改Background

![](..\assets\ui\ui-view-2.png)

在模拟器中调试效果如下：

![](..\assets\ui\ui-view-Simulator-1.png)

#### 代码进行添加设置
除了以上通过工具箱拖动控件的方式以外，我们还可以通过代码的方式进行View的添加设置。

首先删除上一步操作中添加的Background为黑色的空白view，如下：

![](..\assets\ui\ui-view-remove-1.png)

在ViewController中修改ViewDidLoad方法，如下：

```cs
public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    UIView vv1 = new UIView();//实例化创建UIView对象
    vv1.Frame = new CGRect(20, 20, 300, 200);//设置该view对象的位置
    vv1.BackgroundColor = UIColor.Blue;//设置背景颜色
    this.View.AddSubview(vv1);//此步不可省略，将当期视图对象添加到页面中，否则无法显示

    UIView vv2 = new UIView();
    vv2.Frame = new CGRect(20, 240, 300, 200);
    vv2.BackgroundColor = UIColor.Orange;
    this.View.AddSubview(vv2);
}
```

调试后显示结果为：

![](..\assets\ui\ui_view_code_new.png)

### UIButton
#### 工具箱拖拽
按钮拖拽很简单，直接拖拽设置即可。


#### 通过代码进行维护
通过代码进行添加一个按钮如下：

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

#### 按钮的响应
通过代码添加按钮，并添加按钮监听，处理对视图View颜色的切换：

```cs
//改变颜色按钮
UIButton btnChangeColor;

//颜色标记
bool isYellow;

public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    CreateButton();
}

/// <summary>
/// 创建按钮方法
/// </summary>
private void CreateButton()
{
    CGRect viewFrame = View.Frame;
    CGRect buttonFrame = new CGRect(10f, viewFrame.Bottom - 200f, viewFrame.Width - 20f, 50f);
    btnChangeColor = UIButton.FromType(UIButtonType.System);
    btnChangeColor.Frame = buttonFrame;

    btnChangeColor.SetTitle("触碰以改变视图颜色", UIControlState.Normal);
    btnChangeColor.SetTitle("改变中。。。", UIControlState.Highlighted);

    //实现响应
    btnChangeColor.TouchUpInside += BtnChangeColor_TouchUpInside;
    View.AddSubview(btnChangeColor);
}

/// <summary>
/// 按钮事件，即实现颜色的变换
/// </summary>
/// <param name="sender">Sender.</param>
/// <param name="e">E.</param>
void BtnChangeColor_TouchUpInside(object sender, EventArgs e)
{
    if (isYellow)
    {
        View.BackgroundColor = UIColor.LightGray;
        isYellow = false;
    }
    else
    {
        View.BackgroundColor = UIColor.Yellow;
        isYellow = true;
    }
}
```

### UIImageView
#### 基本
首先需要添加资源到项目中：

![](..\assets\ui\ui_image_add.png)

![](..\assets\ui\ui_image_add1.png)

通过代码进行设置图片：

![](..\assets\ui\ui_image_res1.png)

```cs
public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    //图像视图实例化
    UIImageView imageView = new UIImageView();
    //设置位置和大小
    imageView.Frame = new CGRect(0, 0, View.Frame.Width, View.Frame.Height);
    //内容模式
    imageView.ContentMode = UIViewContentMode.ScaleToFill;
    //设置图片，路径以Resources为基路径
    imageView.Image = UIImage.FromFile("3.jpg");

    View.AddSubview(imageView);
}
```

模拟器中调试结果为：

![](..\assets\ui\ui_image_simu1.png)

#### ContentMode显示模式
显示模式有很多种，常用的有三种：
* ScaleToFill:默认，显示全部尺寸，会对图像进行拉伸；
* ScaleAspectFit：保证图像比例，有可能会造成部分空白；
* ScaleAspectFill：保证图像比例不变，即按比例进行拉伸；

可以在上例中进行不同设置的尝试。

### UILabel
```cs
UILabel lbl = new UILabel();
lbl.Frame = new CGRect(20, 10, View.Frame.Width - 40, 100);
lbl.Text = "天王盖地虎，小鸡炖蘑菇";
lbl.TextColor = UIColor.Orange;

View.AddSubview(lbl);
```

### 结合UITextField实现登陆框
模拟器调试效果如下：

![](..\assets\ui\ui_text_login_simu1.png)

用户界面通过代码实现：
```cs
public partial class ViewController : UIViewController
{
    protected ViewController(IntPtr handle) : base(handle)
    {
        // Note: this .ctor should not contain any initialization logic.
    }

    UITextField txtID;
    UITextField txtPwd;
    UILabel lbl;
    UIButton btn;

    public override void ViewDidLoad()
    {
        base.ViewDidLoad();
        // Perform any additional setup after loading the view, typically from a nib.

        CreateAndInit();
    }

    private void CreateAndInit()
    {
        //计算文本框宽高
        double wid = View.Frame.Width - 100;

        //添加提示标签
        lbl = new UILabel();
        lbl.Frame = new CGRect(50, 260, wid, 50);
        View.AddSubview(lbl);

        //添加账号文本框
        txtID = new UITextField();
        //设置边框类型
        txtID.BorderStyle = UITextBorderStyle.RoundedRect;
        txtID.Frame = new CGRect(50, 150, wid, 40);
        txtID.Placeholder = "账号";
        View.AddSubview(txtID);

        //添加密码文本框
        txtPwd = new UITextField();
        txtPwd.BorderStyle = UITextBorderStyle.RoundedRect;
        txtPwd.Frame = new CGRect(50, 200, wid, 40);
        txtPwd.Placeholder = "密码";
        //密码文本框用，文本内容隐藏
        txtPwd.SecureTextEntry = true;
        View.AddSubview(txtPwd);

        //添加按钮
        btn = new UIButton();
        btn.Frame = new CGRect(50, 320, wid, 40);
        btn.Layer.CornerRadius = 3;//设置按钮为圆角，半径一般为3
        btn.SetTitle("登陆", UIControlState.Normal);
        btn.SetTitleColor(UIColor.White, UIControlState.Normal);
        btn.BackgroundColor = UIColor.Purple;
        View.AddSubview(btn);

        //添加按钮监听事件
        btn.TouchUpInside += Btn_TouchUpInside;
    }

    void Btn_TouchUpInside(object sender, EventArgs e)
    {
        if (string.IsNullOrEmpty(txtID.Text) || string.IsNullOrEmpty(txtPwd.Text))
        {
            lbl.Hidden = false;
            lbl.Text = "账号或密码不允许为空";
            lbl.TextColor = UIColor.Orange;
        }
        else
        {
            lbl.Hidden = true;
        }
    }

    public override void DidReceiveMemoryWarning()
    {
        base.DidReceiveMemoryWarning();
        // Release any cached data, images, etc that aren't in use.
    }
}
```

### 键盘UIKeyboardType

```cs
UITextField txt = new UITextField();
//修改键盘类型
txt.KeyboardType = UIKeyboardType.KeyboardTypeDefault;
```

#### 类型
1.Default

![](..\assets\ui\UIKeyboardTypeDefault.png)

2.ASCIICapable

![](..\assets\ui\UIKeyboardTypeASCIICapable.png)

3.NumbersAndPunctuation

![](..\assets\ui\UIKeyboardTypeNumbersAndPunctuation.png)

4.URL

![](..\assets\ui\UIKeyboardTypeURL.png)

5.NumberPad

![](..\assets\ui\UIKeyboardTypeNumberPad.png)

6.PhonePad

![](..\assets\ui\UIKeyboardTypePhonePad.png)

7.NamePhonePad

![](..\assets\ui\UIKeyboardTypeNamePhonePad.png)

8.EmailAddress

![](..\assets\ui\UIKeyboardTypeEmailAddress.png)

9.DecimalPad

![](..\assets\ui\UIKeyboardTypeDecimalPad.png)

10.Twitter

![](..\assets\ui\UIKeyboardTypeTwitter.png)

11.WebSearch

![](..\assets\ui\UIKeyboardTypeWebSearch.png)

12.Alphabet == ASCIICapable

![](..\assets\ui\UIKeyboardTypeAlphabet.png)

#### 显示键盘改变输入视图位置

添加TextField，需要注意文本框位置偏下，这样弹出键盘需要做特殊处理：

![](..\assets\ui\ui_keyboard_hide.png)
![](..\assets\ui\ui_keyboard_show.png)

```cs
//需要using Foundation;
NSObject kbdWillShow, kbdDidHide;

public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    CreateAndInit();
}

private void CreateAndInit()
{
    //调整View背景色，否则看不出来文本框
    View.BackgroundColor = UIColor.LightGray;

    UITextField emailField = new UITextField();
    emailField.Frame = new CGRect(20, View.Frame.Height - 50, View.Frame.Width - 50, 30);
    emailField.KeyboardType = UIKeyboardType.EmailAddress;
    emailField.Text = "hello world";
    emailField.BackgroundColor = UIColor.White;
    View.AddSubview(emailField);

    //键盘将要显示时
    kbdWillShow = UIKeyboard.Notifications.ObserveWillShow((s, e) =>
    {
        CGRect kbdBounds = e.FrameEnd;
        CGRect txtFrame = emailField.Frame;
        txtFrame.Y -= kbdBounds.Height;
        emailField.Frame = txtFrame;
    });

    //键盘将要隐藏时
    kbdDidHide = UIKeyboard.Notifications.ObserveDidHide((s, e) =>
    {
        CGRect kbdBounds = e.FrameEnd;
        CGRect txtFrame = emailField.Frame;
        txtFrame.Y += kbdBounds.Height;
        emailField.Frame = txtFrame;
    });

    //键盘上的return
    emailField.ShouldReturn = delegate(UITextField txtField) {
        return txtField.ResignFirstResponder();
    };
}
```

### 进度条UIProgressView

![](..\assets\ui\ui_progress_start.png)

```cs
UIProgressView progressView;
UILabel lblStatus;
UIButton btnStart;
float increment = 0f;

public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    CreateAndInit();
}

private void CreateAndInit()
{
    lblStatus = new UILabel();
    lblStatus.Frame = new CGRect(50, 50, View.Frame.Width - 100, 30);
    lblStatus.Text = "current value:";
    View.AddSubview(lblStatus);

    btnStart = new UIButton();
    btnStart.Frame = new CGRect(50, View.Frame.Height - 300, View.Frame.Width - 100, 40);
    btnStart.SetTitle("Tap To Start Progress...", UIControlState.Normal);
    btnStart.SetTitle("Progressing...", UIControlState.Disabled);
    btnStart.SetTitleColor(UIColor.Black, UIControlState.Normal);
    btnStart.SetTitleColor(UIColor.LightGray, UIControlState.Disabled);
    View.AddSubview(btnStart);

    progressView = new UIProgressView(new CGRect(50, 200, View.Frame.Width - 100, 50));
    progressView.Progress = 0;
    increment = 1f / 100f;
    View.AddSubview(progressView);

    //添加事件监听
    btnStart.TouchUpInside += delegate
    {
        btnStart.Enabled = false;
        progressView.Progress = 0f;
        Task.Factory.StartNew(this.StartProgress);
    };
}

/// <summary>
/// 进度条加载事件
/// </summary>
private void StartProgress()
{
    float currentProgress = 0f;
    while (currentProgress < 1f)
    {
        Thread.Sleep(200);
        this.InvokeOnMainThread(delegate
        {
            progressView.Progress += increment;
            currentProgress = progressView.Progress;
            lblStatus.Text = string.Format("Current value: {0}", Math.Round(progressView.Progress, 2));
            if (currentProgress >= 1f)
            {
                lblStatus.Text = "Progress completed!";
                btnStart.Enabled = true;
            }
        });
    }
}

```

### 滚动视图UIScrollView
1. UIScrollView是滚动的view，UIView本身不能滚动，子类UIScrollview拓展了滚动方面的功能。
2. UIScrollView是所有滚动视图的基类。以后的UITableView，UITextView等视图都是继承于该类。

使用场景：显示不下（单张大图）；内容太多（图文混排）；滚动头条（图片）；相册等

#### 滚动

![](..\assets\ui\ui_scrollview_1.png)

```cs
UIImageView imgView;
UIScrollView scrlView;

public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    CreateAndInit();
}

private void CreateAndInit()
{
    imgView = new UIImageView(UIImage.FromFile("3.jpg"));
    scrlView = new UIScrollView();
    scrlView.Frame = new CGRect(0, 0, View.Frame.Width, View.Frame.Height);
    scrlView.ContentSize = imgView.Image.Size;
    scrlView.ContentOffset = new CGPoint(200f, 50f);

    scrlView.PagingEnabled = true;
    scrlView.MinimumZoomScale = 0.25f;//缩小的最小比例
    scrlView.MaximumZoomScale = 2f;//放大的最大比例

    scrlView.ViewForZoomingInScrollView = delegate (UIScrollView scroll)
    {
        return this.imgView;
    };
    scrlView.ZoomScale = 1f;//比例变化
    scrlView.IndicatorStyle = UIScrollViewIndicatorStyle.Black;//滚动指示器风格

    scrlView.AddSubview(imgView);
    View.AddSubview(scrlView);
}
```

#### 滚动事件

![](..\assets\ui\ui_scroll_view2.png)

```cs
public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    CreateAndInit();
}

private void CreateAndInit()
{
    UIScrollView scrView = new UIScrollView();
    scrView.Frame = new CGRect(0, 0, View.Frame.Width, View.Frame.Height);
    scrView.ContentSize = new CGSize(View.Frame.Width, 2000);
    View.AddSubview(scrView);

    scrView.Scrolled += delegate
    {
        Console.WriteLine("开始滚动。。。");
    };
    scrView.DecelerationEnded += delegate
    {
        Console.WriteLine("滚动结束。。。");
    };

    //为滚动视图添加标签
    int y = 10;
    for (int i = 0; i < 21; i++)
    {
        UILabel lbl = new UILabel();
        lbl.Frame = new CGRect(0, y, View.Frame.Width, 50);
        lbl.BackgroundColor = UIColor.FromRGB(249, 205, 169);
        lbl.Text = string.Format("{0}", i);
        scrView.AddSubview(lbl);
        y += 100;
    }
}
```

### 页面控件UIPageControl

![](..\assets\ui\ui_pagecontrol_1.png)

```cs
using System;
using System.Threading;
using System.Threading.Tasks;
using CoreGraphics;
using Foundation;
using UIKit;

namespace Single
{
    public partial class ViewController : UIViewController
    {
        protected ViewController(IntPtr handle) : base(handle)
        {
            // Note: this .ctor should not contain any initialization logic.
        }

        UIImageView page1;
        UIImageView page2;
        UIImageView page3;
        UIScrollView scrollView;
        UIPageControl pageControl;

        public override void ViewDidLoad()
        {
            base.ViewDidLoad();
            // Perform any additional setup after loading the view, typically from a nib.

            CreateAndInit();
        }

        private void CreateAndInit()
        {
            scrollView = new UIScrollView();
            scrollView.Frame = new CGRect(0, 0, View.Frame.Width, View.Frame.Height);
            scrollView.DecelerationEnded += ScrollView_DecelerationEnded;

            pageControl = new UIPageControl();
            pageControl.Frame = new CGRect(0, 540, View.Frame.Width, 40);
            pageControl.Pages = 3;
            pageControl.ValueChanged += PageControl_ValueChanged;
            scrollView.Scrolled += delegate
            {
                //Console.WriteLine("Scrolled!");
            };
            scrollView.PagingEnabled = true;
            CGRect pageFrame = scrollView.Frame;
            scrollView.ContentSize = new CGSize(pageFrame.Width * 3, pageFrame.Height);

            page1 = new UIImageView(pageFrame);
            page1.ContentMode = UIViewContentMode.ScaleAspectFit;
            page1.Image = UIImage.FromFile("1.jpg");
            pageFrame.X += this.scrollView.Frame.Width;

            page2 = new UIImageView(pageFrame);
            page2.ContentMode = UIViewContentMode.ScaleAspectFit;
            page2.Image = UIImage.FromFile("3.jpg");
            pageFrame.X += this.scrollView.Frame.Width;

            page3 = new UIImageView(pageFrame);
            page3.ContentMode = UIViewContentMode.ScaleAspectFit;
            page3.Image = UIImage.FromFile("4.jpg");
            pageFrame.X += this.scrollView.Frame.Width;

            scrollView.AddSubview(page1);
            scrollView.AddSubview(page2);
            scrollView.AddSubview(page3);

            View.AddSubview(scrollView);
            View.AddSubview(pageControl);
        }

        /// <summary>
        /// Scrolls the view deceleration ended.
        /// 滚动视图结束时，根据滚动视图位置判断是哪一张图片
        /// </summary>
        /// <param name="sender">Sender.</param>
        /// <param name="e">E.</param>
        void ScrollView_DecelerationEnded(object sender, EventArgs e)
        {
            nfloat x1 = page1.Frame.X;
            nfloat x2 = page2.Frame.X;
            nfloat x = scrollView.ContentOffset.X;

            if (x == x1)
            {
                this.pageControl.CurrentPage = 0;
            }
            else if (x == x2)
            {
                this.pageControl.CurrentPage = 1;
            }
            else
            {
                this.pageControl.CurrentPage = 2;
            }
        }

        /// <summary>
        /// Pages the control value changed.
        /// 点击分页小点时才触发
        /// </summary>
        /// <param name="sender">Sender.</param>
        /// <param name="e">E.</param>
        void PageControl_ValueChanged(object sender, EventArgs e)
        {
            CGPoint contentOffset = scrollView.ContentOffset;
            switch (pageControl.CurrentPage)
            {
                case 0:
                    contentOffset.X = page1.Frame.X;
                    scrollView.SetContentOffset(contentOffset, true);
                    break;
                case 1:
                    contentOffset.X = page2.Frame.X;
                    scrollView.SetContentOffset(contentOffset, true);
                    break;
                case 2:
                    contentOffset.X = page3.Frame.X;
                    scrollView.SetContentOffset(contentOffset, true);
                    break;
                default:
                    break;
            }
        }

        public override void DidReceiveMemoryWarning()
        {
            base.DidReceiveMemoryWarning();
            // Release any cached data, images, etc that aren't in use.
        }
    }
}

```


### 警告UIAlertView
#### title

![](..\assets\ui\ui_alert_msg.png)

```cs
public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    UIAlertView altView = new UIAlertView();
    altView.Title = "提示";
    altView.Message = "电量不足";
    altView.Show();
}
```

#### button

![](..\assets\ui\ui_alert_button.png)

```cs
public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    UIAlertView altView = new UIAlertView();
    altView.Title = "谢谢";
    altView.Message = "亲如果你对我们的商品满意，清点亮五颗星";
    altView.AddButton("前往评论");
    altView.AddButton("暂不评论");
    altView.AddButton("残忍拒绝");
    altView.Show();
}
```

#### button-click

![](..\assets\ui\ui_alert_button_click.png)

```cs
UIButton btnShowAler;

public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    btnShowAler = new UIButton();
    btnShowAler.Frame = new CGRect(100, 300, 110, 30);
    btnShowAler.SetTitle("Show Alert", UIControlState.Normal);
    btnShowAler.SetTitleColor(UIColor.Black, UIControlState.Normal);
    View.AddSubview(btnShowAler);
    btnShowAler.TouchUpInside += (sender, e) =>
    {
        ShowAlert("Alert Message", "Tap OK or Cancel");
    };
}

private void ShowAlert(string title, string message)
{
    UIAlertView altView = new UIAlertView();
    altView.Title = title;
    altView.Message = message;

    altView.AddButton("OK");
    altView.AddButton("Cancel");
    //事件响应
    altView.Dismissed += (sender, e) =>
    {
        if (e.ButtonIndex == 0)
        {
            btnShowAler.SetTitle("OK!", UIControlState.Normal);
        }
        else
        {
            btnShowAler.SetTitle("Cancelled!", UIControlState.Normal);
        }
    };
    altView.Show();
}
```

### UITableView
#### 简单实例
创建一个新的Single View Application

修改【ViewController.cs】文件中方法ViewDidLoad：
```cs
public partial class ViewController : UIViewController
{
    protected ViewController(IntPtr handle) : base(handle)
    {
        // Note: this .ctor should not contain any initialization logic.
    }

    //定义泛型集合，测试球队数据
    List<string> premTeams = new List<string>() { "LIVERPOOL", "EVERTON", "ARSENAL",
        "SRANSEA", "CARDIFF", "NECASTIE", "ABRAHAM", "ALEXANDERNAL", "ANTOINE", "ARMSTRONG", "BARTHOLOMEW" };

    public override void ViewDidLoad()
    {
        base.ViewDidLoad();
        // Perform any additional setup after loading the view, typically from a nib.

        //定义tableview
        UITableView tableView = new UITableView();
        tableView.Frame = new CoreGraphics.CGRect(0, 20, View.Frame.Width, View.Frame.Height - 20);
        tableView.Source = new MyViewSource(premTeams);//设置tableview的数据源

        View.AddSubview(tableView);
    }

    public override void DidReceiveMemoryWarning()
    {
        base.DidReceiveMemoryWarning();
        // Release any cached data, images, etc that aren't in use.
    }
}

/// <summary>
/// 构造自定义UITableViewSource类
/// </summary>
public class MyViewSource : UITableViewSource
{
    List<string> dupPremTeams;

    /// <summary>
    /// Initializes a new instance of the <see cref="T:TableViewDemo.MyViewSource"/> class.
    /// 自定义构造函数
    /// </summary>
    /// <param name="prems">Prems.</param>
    public MyViewSource(List<string> prems)
    {
        dupPremTeams = prems;
    }

    /// <summary>
    /// Gets the cell.
    /// 重写获取单元格方法
    /// </summary>
    /// <returns>The cell.</returns>
    /// <param name="tableView">Table view.</param>
    /// <param name="indexPath">Index path.</param>
    public override UITableViewCell GetCell(UITableView tableView, NSIndexPath indexPath)
    {
        UITableViewCell cell = new UITableViewCell();
        cell.TextLabel.Text = dupPremTeams[indexPath.Row];
        return cell;
    }

    /// <summary>
    /// Rowses the in section.
    /// 重写一节中有多少行方法
    /// </summary>
    /// <returns>The in section.</returns>
    /// <param name="tableview">Tableview.</param>
    /// <param name="section">Section.</param>
    public override nint RowsInSection(UITableView tableview, nint section)
    {
        return this.dupPremTeams.Count;
    }
}
```

显示效果如下：
![](..\assets\ui_adv\ui_table_res_1.png)

#### 设置Table
可以通过重写UITableViewSource中提供的方法，修改TableView的样式，如下：

![](..\assets\ui_adv\ui_table_res_2.png)

```cs
/// <summary>
/// 构造自定义UITableViewSource类
/// </summary>
public class MyViewSource : UITableViewSource
{
    List<string> dupPremTeams;

    /// <summary>
    /// Initializes a new instance of the <see cref="T:TableViewDemo.MyViewSource"/> class.
    /// 自定义构造函数
    /// </summary>
    /// <param name="prems">Prems.</param>
    public MyViewSource(List<string> prems)
    {
        dupPremTeams = prems;
    }

    /// <summary>
    /// Gets the cell.
    /// 重写获取单元格方法
    /// </summary>
    /// <returns>The cell.</returns>
    /// <param name="tableView">Table view.</param>
    /// <param name="indexPath">Index path.</param>
    public override UITableViewCell GetCell(UITableView tableView, NSIndexPath indexPath)
    {
        UITableViewCell cell = new UITableViewCell();
        //设置单元格文字
        cell.TextLabel.Text = dupPremTeams[indexPath.Row];
        //设置单元格图片
        cell.ImageView.Image = UIImage.FromFile("1.jpg");
        return cell;
    }

    //添加页眉
    public override string TitleForHeader(UITableView tableView, nint section)
    {
        return "球队";
    }

    //添加页脚
    public override string TitleForFooter(UITableView tableView, nint section)
    {
        return "表尾";
    }

    //设置页眉行高
    public override nfloat GetHeightForHeader(UITableView tableView, nint section)
    {
        return 30;
    }

    //设置页脚行高
    public override nfloat GetHeightForFooter(UITableView tableView, nint section)
    {
        return 25;
    }

    /// <summary>
    /// Rowses the in section.
    /// 重写一节中有多少行方法
    /// </summary>
    /// <returns>The in section.</returns>
    /// <param name="tableview">Tableview.</param>
    /// <param name="section">Section.</param>
    public override nint RowsInSection(UITableView tableview, nint section)
    {
        return this.dupPremTeams.Count;
    }
}
```

#### Table风格
设置不同的section以区分内容：

![](..\assets\ui_adv\ui_table_res_2.png)

```cs
public partial class ViewController : UIViewController
{
    protected ViewController(IntPtr handle) : base(handle)
    {
        // Note: this .ctor should not contain any initialization logic.
    }

    List<string> titleTeams = new List<string>() { "衣服", "包包", "配饰" };
    List<string> premTeams1 = new List<string>() { "薄外套", "防晒衣", "雪纺", "T恤", "衬衫" };
    List<string> premTeams2 = new List<string>() { "双肩包", "编织包", "复古包", "斜挎包", "钱包", "手提包" };
    List<string> premTeams3 = new List<string>() { "项链", "脚链", "戒指", "手镯", "佛珠手串", "毛衣链", "耳饰", "手链" };

    public override void ViewDidLoad()
    {
        base.ViewDidLoad();
        // Perform any additional setup after loading the view, typically from a nib.

        UITableView tableView = new UITableView();
        tableView.Frame = new CoreGraphics.CGRect(0, 0, UIScreen.MainScreen.Bounds.Width
                                                    , UIScreen.MainScreen.Bounds.Height);
        tableView.Source = new MyViewSource(premTeams1, premTeams2, premTeams3, titleTeams);

        View.AddSubview(tableView);
    }

    public override void DidReceiveMemoryWarning()
    {
        base.DidReceiveMemoryWarning();
        // Release any cached data, images, etc that aren't in use.
    }
}

/// <summary>
/// 构造自定义UITableViewSource类
/// </summary>
public class MyViewSource : UITableViewSource
{
    List<string> dupTitleTeams;
    List<string> dupPremTeams1;
    List<string> dupPremTeams2;
    List<string> dupPremTeams3;

    /// <summary>
    /// Initializes a new instance of the <see cref="T:TableViewDemo.MyViewSource"/> class.
    /// 自定义构造方法
    /// </summary>
    /// <param name="prems1">Prems1.</param>
    /// <param name="prems2">Prems2.</param>
    /// <param name="prems3">Prems3.</param>
    /// <param name="title">Title.</param>
    public MyViewSource(List<string> prems1, List<string> prems2, List<string> prems3, List<string> title)
    {
        dupTitleTeams = title;
        dupPremTeams1 = prems1;
        dupPremTeams2 = prems2;
        dupPremTeams3 = prems3;
    }

    /// <summary>
    /// Numbers the of sections.
    /// 节数设置
    /// </summary>
    /// <returns>The of sections.</returns>
    /// <param name="tableView">Table view.</param>
    public override nint NumberOfSections(UITableView tableView)
    {
        return 3;
    }

    public override UITableViewCell GetCell(UITableView tableView, NSIndexPath indexPath)
    {
        UITableViewCell cell = new UITableViewCell();
        switch (indexPath.Section)
        {
            case 0:
                cell.TextLabel.Text = dupPremTeams1[indexPath.Row];
                break;
            case 1:
                cell.TextLabel.Text = dupPremTeams2[indexPath.Row];
                break;
            case 2:
                cell.TextLabel.Text = dupPremTeams3[indexPath.Row];
                break;

            default:
                break;
        }
        return cell;
    }

    public override nint RowsInSection(UITableView tableview, nint section)
    {
        switch (section)
        {
            case 0:
                return dupPremTeams1.Count;
            case 1:
                return dupPremTeams2.Count;
            case 2:
                return dupPremTeams3.Count;
            default:
                return 0;
        }
    }

    /// <summary>
    /// Titles for header.
    /// 每一节单独标题设置
    /// </summary>
    /// <returns>The for header.</returns>
    /// <param name="tableView">Table view.</param>
    /// <param name="section">Section.</param>
    public override string TitleForHeader(UITableView tableView, nint section)
    {
        return dupTitleTeams[int.Parse(section.ToString())];
    }

    public override nfloat GetHeightForHeader(UITableView tableView, nint section)
    {
        return 50;
    }
}
```

### 一次修改相同的视图
在一个应用程序中，使用了很多相同的视图。如果想要将这些视图的属性设置为相同值，我们可以采用一个简单的方。

使用Appearance属性，它是一个类型方法，语法形式如下：
`视图类.Appearance.视图的属性 = 属性设置;`

比如修改多个label标签的颜色和字体大小如下：
```cs
public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    UILabel label1 = new UILabel();
    label1.Frame = new CGRect(0, 90, View.Frame.Width, 50);
    label.Text = "Label1";
    View.AddSubview(label1);

    UILabel label2 = new UILabel();
    label1.Frame = new CGRect(0, 200, View.Frame.Width, 50);
    label.Text = "Label2";
    View.AddSubview(label2);

    UILabel label3 = new UILabel();
    label1.Frame = new CGRect(0, 300, View.Frame.Width, 50);
    label.Text = "Label3";
    View.AddSubview(label3);

    //统一设置颜色
    UILabel.Appearance.TextColor = UIColor.Red;
    //统一设置字体大小
    UILabel.Appearance.Font = UIFont.SystemFontOfSize(40);
}
```




