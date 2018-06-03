<!-- TOC -->

- [Xamarin](#xamarin)
    - [Xamarin简介](#xamarin)
    - [Xamarin 的工作原理](#xamarin)
        - [Xamarin.iOS.dll 和 Mono.Android.dll](#xamariniosdll--monoandroiddll)
        - [应用程序输出](#)

<!-- /TOC -->

# Xamarin

## Xamarin简介
考虑如何生成 iOS 和 Android 应用程序时，许多用户都认为本机语言、Objective-C、Swift 和 Java 是唯一的选择。 但是，在过去几年中，一个全新的生成移动应用程序平台的生态系统已经出现了。

Xamarin 是唯一能通过提供跨 iOS、Android 和 Windows Phone（Windows Phone 的本机语言已经是 C#）这三种平台可正常工作的单一语言 - C#、类库和运行时，却仍能编译性能甚至足以满足高要求游戏的本机（非解释型）应用程序的平台。
其中的每个平台都有不同的功能组合，不同点在于编写本机应用程序的能力 - 即可编译为本机代码，并可与基础 Java 子系统进行流畅互操作的应用程序。 例如，某些平台只允许使用 HTML 和 JavaScript 生成应用，而某些平台级别非常低，且只允许使用 C/C++ 代码。 某些平台甚至不能使用本机控件工具包。

Xamarin 是唯一结合了本机平台的所有功能，并自身增加了大量的强大功能的平台，包括：
1. 基础 SDK 完全绑定 - Xamarin 包含 iOS 和 Android 中几乎整个基础平台 SDK 的绑定。 此外，这些绑定属于强类型，意味着可以轻松导航和使用，并提供可靠的编译时类型检查和开发过程。 这可使运行时错误更少，应用程序质量更好。
2. Objective-C、Java、C 和 C++ 互操作 - Xamarin 提供直接调用 Objective-C、Java、C 和 C++ 库的功能，使用户能够使用已创建的各种第三方代码。 这样可以充分利用使用 Objective-C、Java 或 C/C++ 编写的现有 iOS 和 Android 库。 另外，Xamarin 还提供绑定项目功能，使用户可使用声明性语法轻松绑定本机 Objective-C 和 Java 库。
3. 新式语言构造 - Xamarin 应用程序采用 C# 编写，C# 是一种新式语言，包含针对 Objective-C 和 Java 的重大改进，比如动态语言功能、功能性构造（比如 Lambdas）、LINQ、并行编程功能和复杂泛型等。
4. 出色的基类库 (BCL) - Xamarin 应用程序使用 .NET BCL，后者是类的大规模集合，具有全面而简化的功能，比如强大的 XML、数据库、序列化、IO、字符串和网络支持，这只是其中的几个例子。 此外，还以编译现有 C# 代码用于应用程序，这可提供对成千上万的库的访问权限，允许用户在其中执行 BCL 中尚无法执行的操作。
5. 新式集成开发环境 (IDE) - Xamarin 在 Mac OS X 上使用 Visual Studio for Mac，在 Windows 上使用 Visual Studio。 两者都属于新式 IDE，其中包括诸如代码自动完成、复杂项目和解决方案管理系统、综合项目模板库、集成源代码管理等功能。
6. 移动跨平台支持 - Xamarin 对 iOS、Android 和 Windows Phone 这三个主移动平台提供复杂的跨平台支持。 可编写应用程序共享其多达 90% 的代码，并且 Xamarin.Mobile 库提供了 Unified API 跨这三个平台来访问公共资源。 这可明显减少移动开发人员针对这三种最热门移动平台的开发成本和进行市场推广所需的时间。

## Xamarin 的工作原理
amarin 提供两种商业产品：Xamarin.iOS 和 Xamarin.Android。 两者都是在 Mono 基础上生成的，后者是基于已发布 .NET ECMA 标准的 .NET Framework 的开源版本。 Mono 推出时间几乎与 .NET Framework 本身一样长，并可在几乎每一个能想到的平台上运行，包括 Linux、Unix、FreeBSD 和 Mac OS X。

在 iOS 上，Xamarin 的预先 (AOT) 编译器将 Xamarin.iOS 应用程序直接编译到本机 ARM 程序集代码。 在 Android 上，Xamarin 编译器则将应用编译为中间语言 (IL)，随后启用应用程序时，再实时 (JIT) 编译为本机程序集。

两种情况中，Xamarin 应用程序均使用自动处理事务（比如内存分配、垃圾回收和基础平台互操作等）的运行时。

### Xamarin.iOS.dll 和 Mono.Android.dll
Xamarin 应用程序针对 .NET BCL（称为 Xamarin 移动配置文件）的子集生成。 此配置文件专门为移动应用程序创建，并打包在 MonoTouch.dll 和 Mono.Android.dll（分别针对 iOS 和 Android）中。 这与 Silverlight（和 Moonlight）应用程序针对 Silverlight/Moonlight .NET 配置文件生成的方式很类似。 事实上，Xamarin 移动配置文件相当于 Silverlight 4.0 配置文件以及加回其中的一系列 BCL 类。

有关可用程序集和类的完整列表，请参阅 Xamarin.iOS 程序集列表和 Xamarin.Android 程序集列表
除了 BCL，这些 .dll 还包括几乎整个 iOS SDK 和 Android SDK 的包装器，允许直接从 C# 调用基础 SDK API。

### 应用程序输出

编译 Xamarin 应用程序时，结果是应用程序包，要么是 iOS 中的 .app 文件，要么是 Android 中的 .apk 文件。 这些文件与使用平台的默认 IDE 生成的应用程序包不好区别，并且这些文件均可通过完全相同的方式部署。

