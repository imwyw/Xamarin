<!-- TOC -->

- [准备AppleID](#appleid)
    - [注册](#)
    - [账号登陆](#)
- [入门-基于mac os](#mac-os)
    - [必需组件](#)
    - [mac安装指南](#mac)
        - [安装](#)
        - [在 Mac 上安装和配置 Xamarin.iOS](#mac--xamarinios)
    - [设置设备进行开发](#)
    - [设置和安装 Visual Studio for Mac](#visual-studio-for-mac)

<!-- /TOC -->

# 准备AppleID
## 注册
通过苹果官方进行注册appleid，mac系统的使用和应用的更新离不开appleid

> https://appleid.apple.com/account#!&page=create

## 账号登陆
从Launchpad中打开AppStore，点击账户进行登陆

![](..\assets\mac-xcode\appstore_id.png)

# 入门-基于mac os
除了可随时获得一种新式语言 (C#) 的灵活性和优雅性、.NET 基类库 (BCL) 的强大功能，以及两个一流 IDE(Visual Studio for Mac 和 Visual Studio)，Xamarin.iOS 还可使开发者使用 Objective-C 和 Xcode 中提供的相同 UI 控件来 创建本机 iOS 应用程序。 本系列介绍如何设置和安装 Xamarin.iOS 并解决 Xamarin.iOS 开发的基础问题。

## 必需组件
若要针对 Xamarin.iOS 构建，需具备以下条件：
* iOS SDK 最新版。
* Xcode 最新版。
* Mac OS X Sierra(10.12) 及更高版本。

## mac安装指南
Xcode 的最新版可通过 iOS 开发人员中心（需要登录）或 Mac App Store 进行下载：

![](..\assets\mac-xcode\app_xcode9.4.png)

下载 Visual Studio for Mac 后，要开始开发本机跨平台应用，还需先安装并设置一些其他内容。

visual studio for Mac 下载地址：
> https://www.visualstudio.com/zh-hans/

要结合使用 iOS 和 Visual Studio，需要以下各项：
* 运行 macOS Sierra 10.12 或更高版本的 Mac
* Xcode 8.3 或更高版本。 通常建议使用稳定的最新版本。
* 一个 Apple ID。 如果没有 Apple ID，请在 https://appleid.apple.com 新建一个。需要 Apple ID 才可安装和登录 Xcode。

### 安装
1.从 https://www.visualstudio.com/ 下载 Visual Studio for Mac

2.下载安装包后，单击“VisualStudioInstaller.dmg”文件装载安装程序，然后通过双击徽标运行它，如下图所示：

![](..\assets\mac-xcode\installer-image1.png)

3.系统可能会通过警报对话框发出提示，如下图所示。 在此情况下，请单击“打开”：

![](..\assets\mac-xcode\installer-image2.png)

4.安装程序会检查系统，确定需要安装或更新的组件：

![](..\assets\mac-xcode\installer-image3.png)

5.之后，会出现一个警报对话框，要求确认隐私和许可条款。 按“继续”按钮接受条款：

![](..\assets\mac-xcode\installer-image4.png)

6.安装程序会列出缺少和需要下载并安装的所需组件。 在此处选择要下载的产品：

![](..\assets\mac-xcode\installer-image5.png)

如果不希望安装所有平台，请参阅以下指南，它们有助于确定要安装的平台：

**使用 Xamarin 的应用：**
Xamarin.Forms - 选择“Android”和“iOS”平台。
* 仅限 iOS - 选择“iOS”平台（请注意，需要安装 Xcode）。
* 仅限 Android - 选择“Android”平台（请注意，还应选择相关依赖项）。
* 仅限 Mac - 选择“macOS”平台（请注意，需要安装 Xcode）。
* 完全跨平台的 Xamarin 应用 - 选择“Android”、“iOS”和“macOS”平台。
**.NET Core 应用程序** - 选择“.NET Core”平台。
**ASP.NET Core Web 应用程序** - 选择“.NET Core”平台。
**跨平台 Unity 游戏开发** - 除 Visual Studio for Mac 之外，无需安装其他任何平台。 若要详细了解如何安装 Unity 扩展，请参阅 Unity 安装指南。

7.确认选择后，选择“安装和更新”按钮开始安装过程。

8.安装程序会启动所选项的下载和安装过程：

![](..\assets\mac-xcode\installer-image7.png)

![](..\assets\mac-xcode\installer-image8.png)

9.系统可能会提示为完成安装所需的各个组件提升必要的权限。 在此处输入管理员凭据以继续安装过程：

![](..\assets\mac-xcode\installer-image10.png)

10.安装成功后，可通过按“开始”，开始在 Visual Studio 中开发应用：

![](..\assets\mac-xcode\installer-image11.png)


