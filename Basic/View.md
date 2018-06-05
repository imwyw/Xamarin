<!-- TOC -->

- [用户界面](#)
    - [视图](#)
        - [常用视图](#)
        - [UIView](#uiview)
            - [工具拖拽](#)
            - [代码进行添加设置](#)
        - [UIButton](#uibutton)
            - [工具箱拖拽](#)
            - [通过代码进行维护](#)
            - [按钮的响应](#)
        - [UIImageView](#uiimageview)
            - [基本](#)
            - [ContentMode显示模式](#contentmode)
        - [UILabel](#uilabel)
        - [结合UITextField实现登陆框](#uitextfield)
        - [键盘UIKeyboardType](#uikeyboardtype)

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

1.UIKeyboardTypeDefault

![](..\assets\ui\UIKeyboardTypeDefault.png)

2.UIKeyboardTypeASCIICapable

![](..\assets\ui\UIKeyboardTypeASCIICapable.png)

3.UIKeyboardTypeNumbersAndPunctuation

![](..\assets\ui\UIKeyboardTypeNumbersAndPunctuation.png)

4.UIKeyboardTypeURL

![](..\assets\ui\UIKeyboardTypeURL.png)

5.UIKeyboardTypeNumberPad

![](..\assets\ui\UIKeyboardTypeNumberPad.png)

6.UIKeyboardTypePhonePad

![](..\assets\ui\UIKeyboardTypePhonePad.png)

7.UIKeyboardTypeNamePhonePad

![](..\assets\ui\UIKeyboardTypeNamePhonePad.png)

8.UIKeyboardTypeEmailAddress

![](..\assets\ui\UIKeyboardTypeEmailAddress.png)

9.UIKeyboardTypeDecimalPad

![](..\assets\ui\UIKeyboardTypeDecimalPad.png)

10.UIKeyboardTypeTwitter

![](..\assets\ui\UIKeyboardTypeTwitter.png)

11.UIKeyboardTypeWebSearch

![](..\assets\ui\UIKeyboardTypeWebSearch.png)

12.UIKeyboardTypeAlphabet == UIKeyboardTypeASCIICapable

![](..\assets\ui\UIKeyboardTypeAlphabet.png)












