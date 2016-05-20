# 用户交互界面测试

UI 测试使你能够找到并与你应用的 UI 进行交互，以此验证 UI 元素的适当性和状态。

UI 测试包括 UI 记录和你实现 UI 测试可以添加的东西。UI 记录能够生成代码，用和你一样的方式检测你应用的 UI。这是一种快速开始编写 UI 测试的很好的方式。

测试报告能够提供 UI 测试的详细信息，包括测试失败时 UI 状态的快照。

UI 测试主要依靠两项核心技术：XCTest 框架和辅助功能。

* XCTest 提供了 UI 测试的框架，这被集成在 Xcode 中。创建并使用 UI 测试是使用 XCTest 创建单元测试的扩充。你创建一个 UI 测试目标的同时，你创建了 UI 测试类和 UI 测试方法作为你项目的一部分。你使用 XCTest 断言来验证预期输出的正确性。你也可以通过 Xcode Server 和 xcodebuild 得到连续集成。XCTest 同时完全兼容 Objective-C 和 Swift。
* 辅助功能是帮助残障人士拥有与其他用户同等丰富的 iOS 和 OS X 体验的核心技术。它提供了丰富的关于 UI 的语义数据使得用户能够通过它们使用你的应用。辅助功能在 UIKit 和 AppKit 中都有集成，提供 API 帮助你调整行为和额外的功能。UI 测试使用数据来实现它的功能。

在源代码中创建 UI 测试与创建单元测试类似。你为你的应用创建了一个 UI 测试目标，接下来 Xcode 会创建一个默认的 UI 测试组以及包含样例测试方法模版的实现文件。当你创建一个 UI 测试目标，你就指定了你测试针对的应用。

UI 测试会查询应用的 UI 对象，同步事件并向那些对象发送事件，以及提供丰富的 API 使你能够检查 UI 对象的内容和状态，并与预期状态相比较。

## 需求
UI 测试不仅依赖于开发工具的服务和 API，也依赖于操作系统平台的服务和 API。你需要 Xcode 7，OS X 10.11 El Captain，以及 iOS 9（或是后续版本）。UI 测试会保护隐私：

* iOS 设备需要启用开发设置并且连接到一个信任的主体。
* OS X 需要赋予一个特殊的 Xcode Helper 应用权限。你在初次使用 UI 测试时会自动得到提示。

## 概念和 API
UI 测试与单元测试有一些基础的不同。单元测试使你能够在应用的视野内工作并且允许你任意访问你应用的变量和状态来测试函数和方法。UI 测试用和用户一样的方法测试你应用的 UI，并不能够访问你应用内部的方法、函数和变量。这令你的测试能够以用户的视角观察你的应用，暴露出用户所遭遇的 UI 问题。

你的测试代码作为一个单独的进程运行，你的应用 UI 响应的事件会被同步。

### API
UI 测试基于下面三个新的类实现：

* XCUIApplication
* XCUIElement
* XCUIElementQuery

## 开始使用 UI 记录
开始使用 UI 记录。其会在一个测试实现文件中生成源代码，该源代码可以被编辑用以构建测试或是重现一个特定的使用场景。UI 记录对于探索新的 UI 或是学习如何编写 UI 测试序列同样有用。基本的操作序列如下：

1. 使用测试导航，创建一个 UI 测试目标。
2. 在刚被创建的模板文件中，将光标置于测试函数。
3. 开始 UI 记录。  
应用启动并运行。通过一系列 UI 动作测试应用。Xcode 会捕获动作并转化成函数体的代码。
4. 当你结束了你想要测试的动作，停止 UI 记录。
5. 向源代码添加 XCTest 断言。

## 编写 UI 测试
API 测试可能既有功能方面也有性能方面，UI 测试也是一样。UI 测试在应用的表层空间进行操作，趋向于集成很多低层次的功能来实现用户视角的显示与响应。

UI 测试基本上在事件与响应层面上进行操作。

* 询问用于寻找一个元素。
* 作为参考了解元素所期望的行为。
* 点击元素触发响应。
* 确定响应是否符合预期，生成通过/失败结果。

使用 XCTest 创建 UI 测试是创建单元测试的相同计算模型的一个扩展，总的来说使用了相似的操作和编程方法，基本的概念区分了 UI 测试的 API。具体的操作方式在 [用户交互界面测试](9-用户交互界面测试-UserInterfaceTesting.md) 中描述。

在测试类结构中，提供的 `setUp` 方法包含与单元测试类中的 `setUp` 方法的两处不同。

```objective-c
- (void)setUp {
    [super setUp];

    // Put setup code here. This method is called before the invocation of each test method in the class.

    self.continueAfterFailure = NO;
    [[[XCUIApplication alloc] init] launch];
}
```

`self.continueAfterFailure` 的值被默认设置为 [NO](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/ObjCRuntimeRef/index.html#//apple_ref/doc/c_ref/NO)。这通常是正确的配置，因为 UI 测试的每一步一般都依赖于上一步的成功执行。如果一步出错，接下来的所有测试都会失败。

其他对于 `setUp` 方法的添加包括创建一个 `XCUIApplication` 的实例并启动它。UI 测试必然会启动它要测试的应用，`setUp` 方法在每一个测试方法前执行，这保证了应用为了每一个测试方法启动。

在编写 UI 测试方法时，你需要使用 UI 记录特性来创建你的测试的一系列基本操作。接下来你可以为了你的目的编辑这个基本的序列，使用 XCTest 断言来提供通过或失败的结果就像单元测试一样。UI 测试既有功能方面也有性能方面，就像单元测试。

一个 UI 正确性测试的基本模式如下：

* 使用 XCUIElementQuery 用来查询一个 XCUIElement。
* 同步一个事件并发送到 XCUIElement。
* 使用断言来比较 XCUIElement 的状态和预期的参考状态。

构建一个 UI 性能测试，在 `measureBlock` 结构中封装一个重复的 UI 动作序列，具体见 [编写性能测试](4-编写测试类与方法-WritingTestClassesAndMethods.md)。
