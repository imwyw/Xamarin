<!-- TOC -->

- [UIGraphics](#uigraphics)
    - [简单应用](#简单应用)
        - [项目结构](#项目结构)
        - [CanvasView](#canvasview)
        - [实例化canvasview](#实例化canvasview)
        - [album权限](#album权限)
        - [画板及保存](#画板及保存)

<!-- /TOC -->

# UIGraphics
## 简单应用
### 项目结构
新增C#类，命名为【CanvasView.cs】,项目结构如下：

![](..\assets\intermedia\CanvasPro_1.png)

### CanvasView
内容如下：
```cs
public partial class CanvasView : UIView
{
    CGPoint touchLocation;
    CGPoint previousTouchLocation;
    CGPath drawPath;
    bool fingerDraw;

    public CanvasView()
    {
        this.drawPath = new CGPath();
    }

    public CanvasView(IntPtr handle) : base(handle)
    {
        this.drawPath = new CGPath();
    }

    public override void TouchesBegan(NSSet touches, UIEvent evt)
    {
        base.TouchesBegan(touches, evt);
        UITouch touch = touches.AnyObject as UITouch;
        this.fingerDraw = true;

        //绘制触摸位置
        this.touchLocation = touch.LocationInView(this);
        this.previousTouchLocation = touch.PreviousLocationInView(this);
        this.SetNeedsDisplay();//更新图层内容
    }

    public override void TouchesMoved(NSSet touches, UIEvent evt)
    {
        base.TouchesMoved(touches, evt);
        UITouch touch = touches.AnyObject as UITouch;

        //获取触摸位置
        this.touchLocation = touch.LocationInView(this);
        this.previousTouchLocation = touch.PreviousLocationInView(this);
        this.SetNeedsDisplay();
    }

    public override void Draw(CGRect rect)
    {
        base.Draw(rect);
        if (this.fingerDraw)
        {
            using (CGContext context = UIGraphics.GetCurrentContext())
            {
                context.SetStrokeColor(UIColor.Blue.CGColor);
                context.SetLineWidth(5f);//线宽
                context.SetLineJoin(CGLineJoin.Round);//线的位置
                context.SetLineCap(CGLineCap.Round);
                this.drawPath.MoveToPoint(this.previousTouchLocation);//开始位置
                this.drawPath.AddLineToPoint(this.touchLocation);//结束位置

                context.AddPath(this.drawPath);//添加路径
                context.DrawPath(CGPathDrawingMode.Stroke);//开始绘制
            }
        }
    }

    public UIImage GetDrawingImage()
    {
        UIImage toReturn = null;
        UIGraphics.BeginImageContext(this.Bounds.Size);
        using (CGContext context = UIGraphics.GetCurrentContext())
        {
            context.SetStrokeColor(UIColor.Red.CGColor);
            context.SetLineWidth(10f);
            context.SetLineJoin(CGLineJoin.Round);
            context.SetLineCap(CGLineCap.Round);
            context.AddPath(this.drawPath);
            context.DrawPath(CGPathDrawingMode.Stroke);
            toReturn = UIGraphics.GetImageFromCurrentImageContext();
        }
        UIGraphics.EndImageContext();
        return toReturn;
    }

    public void ClearDrawing()
    {
        this.fingerDraw = false;
        this.drawPath.Dispose();
        this.drawPath = new CGPath();
        this.SetNeedsDisplay();
    }
}
```

### 实例化canvasview
修改【ViewController.cs】，修改方法【ViewDidLoad】，实例化View并添加：
```cs
public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    //实例化画板并添加
    CanvasView canvasView = new CanvasView();
    //canvasView.Frame = UIScreen.MainScreen.Bounds;
    canvasView.Frame = new CGRect(0, 0, UIScreen.MainScreen.Bounds.Width, UIScreen.MainScreen.Bounds.Height - 50);
    canvasView.BackgroundColor = UIColor.White;
    this.View.AddSubview(canvasView);

    //保存到相册按钮
    UIButton btnSave = new UIButton(UIButtonType.RoundedRect);
    btnSave.Frame = new CoreGraphics.CGRect(50, UIScreen.MainScreen.Bounds.Height - 50, 100, 50);
    btnSave.SetTitle("保存到相册", UIControlState.Normal);
    this.View.AddSubview(btnSave);

    //清空画板按钮
    UIButton btnClean = new UIButton(UIButtonType.RoundedRect);
    btnClean.Frame = new CoreGraphics.CGRect(250, UIScreen.MainScreen.Bounds.Height - 50, 100, 50);
    btnClean.SetTitle("清空画板", UIControlState.Normal);
    this.View.AddSubview(btnClean);

    btnSave.TouchUpInside += (sender, e) =>
    {
        UIImage drawingImage = canvasView.GetDrawingImage();
        drawingImage.SaveToPhotosAlbum((UIImage image, Foundation.NSError error) =>
        {
            UIAlertView altView = new UIAlertView();
            altView.Title = "消息";
            altView.AddButton("OK");
            if (null != error)
            {
                altView.Message = "发生错误：" + error.LocalizedDescription;
            }
            else
            {
                altView.Message = "保存成功";
            }
            altView.Show();
        });
    };

    btnClean.TouchUpInside += (sender, e) =>
    {
        canvasView.ClearDrawing();
    };
}
```

### album权限
保存图片到相册需要增加应用访问相册的权限，这里以IOS11+ 为例

修改【Info.plist】文件，增加key值【Privacy - Photo Library Additions Usage Description】

![](..\assets\intermedia\Canvas_plist_add.png)

### 画板及保存
![](..\assets\intermedia\Canvas_res_1.png)

![](..\assets\intermedia\Canvas_res_2.png)

