# 关于用 Xcode 测试
Xcode 向您提供了广泛的软件测试途径。对项目进行测试可以增强项目的健壮性、减少 bug 并通过使您的产品更易接受来促进销售。经过良好测试的应用能按照期望运行从而增加用户满意度。测试也能帮助您更高效、更快速、更深入地开发应用，并且能维持多人合作开发的协调性。

![Introduction-1](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-intro-1_2x.png)

## 概览
在这篇文档中，您将会学到如何使用 Xcode 中的测试功能，在所有新的目标中 XCTest 框架将会被自动链接。

* **快速开始**： 从 Xcode 5 开始并简介 XCTest 框架，测试导航栏将测试项目的设置过程串流并自动化以方便测试和运行。
* **性能度量**： Xcode 6 和之后的版本创建的测试可以使您通过一个基准线来衡量并跟踪性能变化。
* **UI 测试**： Xcode 7 增加了为应用 UI 编写测试的功能，包括通过源代码来记录 UI 的交互过程用以测试。
* **持续集成与 Xcode Server**： Xcode 测试可以通过命令行脚本来执行或通过在运行有 Xcode Server 的 Mac 上设置机器人来自动执行。
* **现代化**： Xcode 包含一个迁移向导用以将项目从 OCUnit 测试转换为 XCTest 测试。

## 能力要求
您需要熟悉应用设计与编程相关概念。

## 参考
观看以下 WWDC 视频片段来更好地了解 Xcode 的测试功能。

* WWDC 2013: [Testing in Xcode 5 (409)](https://developer.apple.com/videos/wwdc/2013/?id=409)
* WWDC 2014: [Testing in Xcode 6 (414)](https://developer.apple.com/videos/wwdc/2014/?id=414)
* WWDC 2015: [UI Testing in Xcode 7 (406)](https://developer.apple.com/videos/wwdc/2015/?id=406)
* WWDC 2015: [Continuous Integration and Code Coverage in Xcode 7 (410)](https://developer.apple.com/videos/wwdc/2015/?id=410)