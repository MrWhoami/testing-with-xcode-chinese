# 自动化测试过程

在开发过程中除了以交互方式运行测试外，还可以充分利用服务器进行自动化测试。

## 基于服务器的持续集成测试

Xcode 测试具有交互性，它能确保您的代码在其指定的需求下不偏离正确的轨道，并且可以很简单地找到并修复 bug 。一系列快速运行的功能测试不仅可以校正你的开发，还可以让你高效率自信地构建一款健壮的应用程序。
 
这就是说，成功的开发项目往往超出单个开发人员实现和维护的能力范围。像源码管理，服务器上的自动化测试可让你顺利高效地根据团队的需要进行开发工作。

下面是使用基于服务器测试的一些优点：

* 使用服务器可以进行脱机构建和测试，以缓解开发系统做实施和调试的压力，特别是在全方位测试时可能需要很长时间来执行的情况下。
* 开发团队的所有成员使用相同的方案可在服务器上运行相同的测试，从而提高测试的一致性，整个团队也可以访问构建的产品，就像构建和测试报告。
* 你可以灵活调整调度项目需求和团队的需求。比如，当团队中任意一个成员向源码管理系统提交新工作或者在设定的时间定期开始运行测试。测试运行也可以按照需要手动启动。
* 服务器以同样的方式反复运行测试。服务器的报告可以让你和你的团队对构建过程中的问题、警告以及测试解决方案有个随着时间推移的整体轮廓。
* 你的项目可以有更多的目的地进行测试，更具自动性，而且比手动运行测试系统更加经济。例如,您可以有任意数量的 iOS 设备连接到服务器，使用单一的配置，该系统可以构建和测试库、应用程序、在所有设备上测试以及在多个版本的模拟器上进行测试。

## 命令行测试

使用 Xcode 的命令行工具，可以编写自动化脚本来构建和测试您的项目。通过使用此功能，你可以充分利用现有构建自动化系统的优势。

### 使用 xcodebuild 运行测试

`xcodebuild` 命令行工具像 Xcode IDE 一样驱动测试。用 `test` 行为运行 `xcodebuil` 测试，并用 `-destination` 参数指定不同的测试目的。例如，要在本地 OS X "My Mac 64 Bit" 测试 MyApp，使用如下命令来指定目标和架构：

```
> xcodebuild test -project MyAppProject.xcodeproj -scheme MyApp -destination 'platform=OS X,arch=x86_64'
``` 

如果你有 development-enabled 设备插入，你可以通过名称或 id 调用他们。例如，如果你有一个名为 "Development iPod touch" 的 iPod 设备连接了电脑并且你想在这个设备上测试代码，可以使用下面的命令：
	
```
> xcodebuild test -project MyAppProject.xcodeproj -scheme MyApp -destination 'platform=iOS,name=Development iPod touch'
```	

测试也可以在模拟器上运行。使用模拟器可以轻松应对不同的外形因素、操作系统和操作系统版本。模拟器目标可以通过名称或 id 指定，例如：
	
```	
> xcodebuild test -project MyAppProject.xcodeproj -scheme MyApp -destination 'platform=Simulator,name=iPhone,OS=8.1'
```	

`-destination` 参数可以被连接在一起，这样你只需使用一个命令，就可以跨目标进行指定集成共享方案。例如，下面的命令把之前的三个例子合并到一个命令中:

```
> xcodebuild test -project MyAppProject.xcodeproj -scheme MyApp
-destination 'platform=OS X,arch=x86_64'
-destination 'platform=iOS,name=Development iPod touch'
-destination 'platform=Simulator,name=iPhone,OS=9.0'
```	

如果测试失败，`xcodebuild` 将返回一个非零的值。

这些都是你所需要了解的命令行运行测试的概要。有关 `xcodebuild` 更详细的信息，请在终端的应用程序窗口中使用 `man` 命令进行查找。

```
> man xcodebuild 
```

### 通过 ssh 使用 xcodebuild

通过 `ssh` （或者是启动服务）远程登录后运行 `xcodebuild` 将会失败，除非正确的会话环境变量在服务器端被创建。

"Aqua session" 环境变量当你交互性地作为一个用户登录 OS X 系统时被创建。Aqua 会话会初始化 OS X 交互环境的底层部分，运行 OS X 应用需要需要这些会话。更确切地说，使用 UI 框架（AppKit 或 UIKit）的代码需要在 Aqua 会话中运行。因此，在 OS X 上进行测试（以及在模拟器里测试，模拟器也是一个 OS X 应用）需要 Aqua 会话。

默认情况下，使用 `ssh` 登录没有活跃的用户会话的 OS X 系统，会创建一个命令行会话。为了确保 `ssh` 登录创建 Aqua 会话，你必须有一个用户在远程 OS X 服务器系统中处于登录状态。远程系统中用户的存在强制 `ssh` 登录拥有 Aqua 会话。

当服务器端系统有用户在运行时，可以通过 `ssh` 登录运行 `xcodebuild` 执行各种测试。例如，下面的终端应用命令通过 `ssh` 在开发系统服务器上运行了为 “MyApp” 定义的测试：

```
> ssh localhost
> cd ~/Development/MyAppProject_Folder
> xcodebuild test -project MyApp.xcodeproj -scheme MyApp -destination 'platform=Simulator,name=iPhone 6'
```

如果想要深入理解 `ssh`、启动服务和启动代理，以及他们是如何与系统交互的，参见技术注释 *Daemons and Agents and Daemons and Services Programming Guide*。

## 使用 Xcode Server 和持续集成

Xcode 通过 Xcode Server 支持全集成的，基于服务器持续集成的工作流。Xcode Server，可以在 OS X Server 上安装，自动化了构建、分析、测试以及压制应用的集成工序。使用 Xcode Server 和持续集成工作流对于你的交互开发工作来说是无缝的、透明的。

了解所有关于配置并使用 Xcode Server 的内容，参见 [Xcode Server and Continuous Integration Guide](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/xcode_guide-continuous_integration/index.html#//apple_ref/doc/uid/TP40013292)。
