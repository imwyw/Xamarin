<!-- TOC -->

- [Hello.Ios](#helloios)
    - [Phoneword](#phoneword)
        - [新建项目](#)
        - [控件初体验](#)
        - [调试](#)
    - [Phoneword实现](#phoneword)
        - [界面](#)
        - [业务逻辑](#)

<!-- /TOC -->
# Hello.Ios
## Phoneword

本指南介绍如何创建一个应用程序，它将用户输入的字母数字电话号码转换为数字电话号码，然后呼叫该号码。 最终应用程序如下所示:

![](..\assets\helloios\helloios1.png)

### 新建项目
本演练介绍如何创建一个名为 Phoneword 的应用程序，它将字母数字电话号码转换为数字电话号码。

1.从 Applications 文件夹或 Spotlight 启动 Visual Studio for Mac 以显示启动屏幕:

![](..\assets\helloios\vs start.png)

2.在“启动屏幕”中，单击“新项目...”以创建新的 Xamarin.iOS 解决方案:

![](..\assets\helloios\vs_start_new.png)

3.从“新建解决方案”对话框中，选择“iOS”>“应用”>“单视图应用程序”模板，确保选择了 C#。 单击“下一步”:

![](..\assets\helloios\vs_start_singleview.png)

4.配置应用。 为其提供名称 Phoneword_iOS ，并使其他项保留为默认值。 单击“下一步”:

![](..\assets\helloios\Phoneword_name.png)

5.将项目和解决方案名称保留为原样。 在此处选择项目的位置，或将它保留为默认值:

![](..\assets\helloios\Phoneword_config.png)

6.通过在“解决方案板”中双击 Main.storyboard 文件来打开它。 这提供了一种直观创建 UI 的方法：

![](..\assets\helloios\Main.storyboard0.png)

加载UI界面时有可能会显示：无法打开文件，关掉标签重新打开即可，如下即可

![](..\assets\helloios\Main.storyboard.png)

### 控件初体验
在【工具箱】中，向搜索栏键入“标签”并将一个“标签”拖动到设计图面上（中央区域）：

![](..\assets\helloios\MainLabel_1.png)

备注：可以通过导航到“视图”>“面板”，随时打开“属性”窗口或“工具箱”。

抓取拖动控件的图柄（控件周围的圆圈）并使标签更宽，选中该控件并通过属性窗口修改文本内容和对齐方式等值：

![](..\assets\helloios\MainLabel_2.png)

### 调试
1.保存更改，然后通过选择“生成”>“全部生成”或按 ⌘ + B 来生成应用程序。如果应用程序进行了编译，则成功消息会出现在 IDE 顶部：

![](..\assets\helloios\Build_0.png)

如果发生错误，则完成前面的步骤并更正任何错误，直到应用程序成功生成。

2.最后，在 iOS 模拟器中测试应用程序。 在 IDE 左上角，从第一个下拉菜单中选择“调试”，并第二个下拉菜单中选择“iPhone 8 iOS x.x”，然后按“启动”（类似于“播放”按钮的三角形按钮）：

![](..\assets\helloios\Debug_1.png)

![](..\assets\helloios\Debug_2.png)

3.这会在 iOS 模拟器中启动应用程序：

![](..\assets\helloios\Simulator_1.png)

## Phoneword实现

### 界面
1.修改Label标签内容，在设计图面上选择了“标签”的情况下，使用“属性板”将“标签”的“文本”属性更改为“Enter a Phoneword:”

![](..\assets\helloios\MainLabel_new1.png)

2.在工具箱内搜索，将一个“Text Field”从“工具箱”拖动到设计图面上，并将它放置在“Label”下方。 

![](..\assets\helloios\Text_1.png)

3.在设计图面上选择了“Text Field”的情况下，在“Properties Pad”的“标识”部分中将“Text Field”的“名称”属性更改为 PhoneNumberText，并将“文本”属性更改为“1-855-XAMARIN”：

![](..\assets\helloios\Text_2.png)

4.将一个“Button”从“工具箱”拖动到设计图面上，并将它放置在“Text Field”下方。 调整宽度，以便“Button”与“Text Field”和“Label”一样宽：

![](..\assets\helloios\btn_1.png)

5.在设计图面上选择了“按钮”的情况下，在“属性板”的“标识”部分中将“名称”属性更改为 TranslateButton。 将“标题”属性更改为“Translate”：

![](..\assets\helloios\btn_1_1.png)

6.重复上面的两个步骤，将一个“Button”从“工具箱”拖动到设计图面上，并将它放置第一个“Button”下方。 调整宽度，以便该“Button”与第一个“Button”一样宽：

![](..\assets\helloios\btn_2.png)

7.在设计图面上选择了第二个“按钮”的情况下，在“属性板”的“标识”部分中将“名称”属性更改为 CallButton。 将“标题”属性更改为“Call”：

![](..\assets\helloios\btn_2_1.png)

通过导航到“文件”>“保存”或通过 快捷键（⌘ + s） 来保存更改。

### 业务逻辑
1.需要将一些逻辑添加到应用，以便将电话号码为字母数字转换为数字。 右键单击“Solution Pad”中的“Phoneword_iOS”，再依次选择“添加”>“新文件…”或按“⌘ + n”，向项目添加新文件：

![](..\assets\helloios\project_new_file.png)

2.在“新建文件”对话框中，选择“常规”>“空类”，将新文件命名为 PhoneTranslator：

![](..\assets\helloios\new_class_name.png)

3.这会为我们创建新的空 C# 类。 删除所有模板代码并替换为以下代码：

```cs
using System.Text;
using System;

namespace Phoneword_iOS
{
    public static class PhoneTranslator
    {
        public static string ToNumber(string raw)
        {
            if (string.IsNullOrWhiteSpace(raw))
            {
                return "";
            }
            else
            {
                raw = raw.ToUpperInvariant();
            }

            var newNumber = new StringBuilder();
            foreach (var c in raw)
            {
                if (" -0123456789".Contains(c))
                {
                    newNumber.Append(c);
                }
                else
                {
                    var result = TranslateToNumber(c);
                    if (result != null)
                    {
                        newNumber.Append(result);
                    }
                }
                // otherwise we've skipped a non-numeric char
            }
            return newNumber.ToString();
        }

        static bool Contains(this string keyString, char c)
        {
            return keyString.IndexOf(c) >= 0;
        }

        static int? TranslateToNumber(char c)
        {
            if ("ABC".Contains(c))
            {
                return 2;
            }
            else if ("DEF".Contains(c))
            {
                return 3;
            }
            else if ("GHI".Contains(c))
            {
                return 4;
            }
            else if ("JKL".Contains(c))
            {
                return 5;
            }
            else if ("MNO".Contains(c))
            {
                return 6;
            }
            else if ("PQRS".Contains(c))
            {
                return 7;
            }
            else if ("TUV".Contains(c))
            {
                return 8;
            }
            else if ("WXYZ".Contains(c))
            {
                return 9;
            }
            return null;
        }
    }
}
```

保存 PhoneTranslator.cs 文件并关闭它。

4.添加代码以关联用户界面。 若要执行此操作，请在“解决方案板”中双击 ViewController.cs以打开它：

![](..\assets\helloios\ViewCont_1.png)

5.首先关联 TranslateButton。 在 ViewController 类中，找到 ViewDidLoad 方法并在 base.ViewDidLoad() 调用下方添加以下代码：

```cs
public override void ViewDidLoad()
{
    base.ViewDidLoad();
    // Perform any additional setup after loading the view, typically from a nib.

    string translatedNumber = "";

    TranslateButton.TouchUpInside += (object sender, EventArgs e) => {
        // Convert the phone number with text to a number
        // using PhoneTranslator.cs
        translatedNumber = PhoneTranslator.ToNumber(
            PhoneNumberText.Text);

        // Dismiss the keyboard if text field was tapped
        PhoneNumberText.ResignFirstResponder();

        if (translatedNumber == "")
        {
            CallButton.SetTitle("Call ", UIControlState.Normal);
            CallButton.Enabled = false;
        }
        else
        {
            CallButton.SetTitle("Call " + translatedNumber,
                UIControlState.Normal);
            CallButton.Enabled = true;
        }
    };
}
```

6.添加代码以响应按第二个按钮的用户（名为 CallButton）。 将以下代码置于 TranslateButton 的代码下方，并将 using Foundation; 添加到文件顶部：

```cs
CallButton.TouchUpInside += (object sender, EventArgs e) => {
        // Use URL handler with tel: prefix to invoke Apple's Phone app...
        var url = new NSUrl ("tel:" + translatedNumber);

        // ...otherwise show an alert dialog
        if (!UIApplication.SharedApplication.OpenUrl (url)) {
            var alert = UIAlertController.Create ("Not supported", "Scheme 'tel:' is not supported on this device", UIAlertControllerStyle.Alert);
            alert.AddAction (UIAlertAction.Create ("Ok", UIAlertActionStyle.Default, null));
            PresentViewController (alert, true, null);
        }
    };
```

7.保存更改，然后通过选择“生成”>“全部生成”或按 ⌘ + B 来生成应用程序。如果应用程序进行了编译，则成功消息会出现在 IDE 顶部：

![](..\assets\helloios\Build_0.png)

8.最后在模拟器中测试该程序：

![](..\assets\helloios\Simulator_2.png)



