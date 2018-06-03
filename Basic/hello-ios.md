<!-- TOC -->

- [Hello.Ios](#helloios)
    - [Phoneword](#phoneword)
        - [新建项目](#)
        - [控件初体验](#)
        - [调试](#)
    - [Phoneword实现](#phoneword)
        - [界面](#)

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






