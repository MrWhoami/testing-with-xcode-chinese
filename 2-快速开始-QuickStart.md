# 快速开始
本文的目的在于让测试成为你软件开发的重要组成部分，并使测试更方便并易于使用。

## 测试导航栏简介
测试时我们会频繁使用 Xcode 的测试导航栏[^1]。

测试导航是Xcode工作区的一部分，其设计宗旨是方便你创建、管理、运行和审核测试功能。你可以通过点击导航选择栏上在事件导航[^2]和调试导航[^3]的中间那个图标来访问测试导航。当你的项目定义了一组测试，你会在导航栏看到如下图所示：

![1-1](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-qs-1_2x.png)

上面的测试导航展示了一个样板项目中的测试包、类和方法的分级表。这个项目是一个示例计算器应用。计算器引擎作为一个框架实现。你可以在分级表的顶部看到用于测试应用代码 `SampleCalcTests` 测试包。

> **注意**: Xcode的测试目标会生成测试包并显示在测试导航栏中。

> 如果你的测试使用存储数据文件、图片，和其他类似的类型，则可以把它们添加到测试包中，并使用 `NSBundle` 的API在运行时访问。和测试类一同使用 `+[NSBundle bundleForClass:]` 保证测试类从正确的包中取得数据。更多的信息可见 [NSBundle Class Reference](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSBundle_Class/index.html#//apple_ref/doc/uid/TP40003624).

> Xcode 方案[^4]控制编译的内容。方案也可以控制可用的测试方法来执行测试操作。你可以在测试导航面板列表中通过 Control+单击 项目来启用或禁用测试包、类和方法，或者从快捷菜单中启用或者关闭测试，此外还可以在方案中启用或者关闭测试。

此视图中的激活的测试包是 `SampleCalcTests`。`SampleCalcTests` 包括了一个测试类，该类中共有9个测试方法。当你按住表中任何一个项目的箭头，运行按钮![2-2](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-test_navigator_run_button_2x.png)
就会出现在项目名的右边。这是运行包或类里所有的测试以及任何独立的测试的比较快捷的方式。测试将返回通过或失败结果给 Xcode。当测试被执行，旁边的标识会更新从而向你显示结果，绿色的对勾标记是通过，红色的 X 为失败。在下面的测试导航面板中，两个测试被判定为失败。

![2-3](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-qs-2_2x.png)  


点击列表中的任意测试类或测试方法都会在源码编辑器中打开测试类。测试类和方法和标记一起放在源码编辑器的侧栏中，和在测试导航面板中的工作方式相同。测试失败将在源码编辑器中相关的断言处展示结果字符串。

测试导航面板底部是添加按钮 (+) ，还有一个过滤控制器。你可以缩小视图到只进行活跃的方案中的测试或者只测试曾失败的测试，也可以通过名称筛选测试。

更多测试导航详细信息可见[Test Navigator Help](https://developer.apple.com/library/ios/recipes/xcode_help-test_navigator/_index.html#//apple_ref/doc/uid/TP40013329)。


## 给你的应用添加测试
在 Xcode5 以及之后版本中创建新的应用、框架和库项目会预配置一个测试目标。当你打开新项目，在测试导航面板上可以看到一个测试包、一个测试类和一个测试方法的模板。但是如果打开一个比较老版本的 Xcode 的项目就不会有测试目标了。下面的工作流程展示了一个假定没有集成测试目标的老项目。

### 创建测试目标
打开测试导航栏，点击左下角的（+）按钮，从菜单中选择 New Unit Test Target。
![2-4](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-qs-3_2x.png)

在接下来的对话框中选择 OS X or iOS Unit Testing Bundle 并点击 Next。根据你的设置偏好和需求，在新目标设置助手中编辑 Product Name 和其他参数。

![2-5](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-qs-4_2x.png)

点击 Finish 按钮来添加目标，测试导航面板中的新目标包含了一个模板测试类和两个测试方法模板。
![2-6](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-qs-5_2x.png )

### 运行测试并查看结果
现在你已经把测试加到了项目中，你会想要运行这些测试来做一些有用的事。但首先要在测试导航面板中把鼠标悬停在 `SampleCalcTests` 测试类上并点击运行按钮来运行类中所有的测试方法。绿色的对号作为测试结果的标记显示在了源代码编辑器侧栏靠近函数名称的位置。

![2-7](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-qs-6_2x.png)

模板单元和性能测试皆为空白，这就是测试显示通过标记的原因－没有失败被断言。注意在 34 行 `measureBlock:` 方法旁的灰色钻石形标记，单击该钻石标记会显示性能结果面板。

![2-8](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-qs-7_2x.png)

该面板使你能够设置一条性能基准线、编辑基准线和编辑 Max STDDEV 参数，该特征将在后面的章节讨论。

### 编辑测试代码并再次运行

因为这个样板项目是一个计算器应用，你可能要检查它是否能正确执行加法、减法、乘法和除法操作，并测试其他计算器功能。因为测试被编译到了应用项目里面，不管你的需求多复杂，你都可以按照你的需求添加所有的上下文和其他所需信息来执行测试。举个例子，我们将 `#import` 和实例变量声明插入到了 `SampleCalcTests.m` 文件中。

```objective-c
#import <XCTest/XCTest.h>

//

// Import the application specific header files

#import "CalcViewController.h"

#import "CalcAppDelegate.h"

 

@interface CalcTests : XCTestCase {

// add instance variables to the CalcTests class

@private

    NSApplication       *app;

    CalcAppDelegate     *appDelegate;

    CalcViewController  *calcViewController;

    NSView              *calcView;

}

@end
```

接下来给测试方法一个描述性的名称，比如 `testAddition`，然后添加到方法的实现[^5]源代码中。

```objective-c
- (void) testAddition

{

   // obtain the app variables for test access

   app                  = [NSApplication sharedApplication];

   calcViewController   = (CalcViewController*)[[NSApplication sharedApplication] delegate];

   calcView             = calcViewController.view;

 

   // perform two addition tests

   [calcViewController press:[calcView viewWithTag: 6]];  // 6

   [calcViewController press:[calcView viewWithTag:13]];  // +

   [calcViewController press:[calcView viewWithTag: 2]];  // 2

   [calcViewController press:[calcView viewWithTag:12]];  // =

    XCTAssertEqualObjects([calcViewController.displayField stringValue], @"8", @"Part 1 failed.");

 

   [calcViewController press:[calcView viewWithTag:13]];  // +

   [calcViewController press:[calcView viewWithTag: 2]];  // 2

   [calcViewController press:[calcView viewWithTag:12]];  // =

    XCTAssertEqualObjects([calcViewController.displayField stringValue], @"10", @"Part 2 failed.");

}
```

注意测试导航的列表的改变反应了模板测试方法 `testExample` 已经被替换为`testAddition`。

![2-9](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-qs-8_2x.png)

现在，点击测试导航的运行按钮（或源代码编辑器中的指示标记）来运行 `testAddition` 方法。

![2-10](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-qs-9_2x.png)

如你所见，一个断言失败了并被测试导航和源代码编辑器高亮标记了出来。看下代码，第一部分成功了，第二部分有问题。进一步观察，错误很明显：字符引用 `"11"` 多算了1，改为`“10”` 就能修复问题并测试成功了。

![2-11](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-qs-8a_2x.png)

### 在通用代码中使用 setUp() 和 tearDown() 方法

Xcode 在活跃的测试包的所有测试类中一次运行一个测试方法。在这个小例子里只有一个测试方法被实现了，这里需要访问三个计算器应用对象变量的功能。如果在同一个类中写了4个或5个测试方法，你会发现你在每一次测试方法获得应用的对象状态中，重复了相同的代码。XCTest 框架为测试类提供了实例方法 `setUp` 和 `tearDown`，你可以用它在每个测试方法运行之前或者之后执行通用代码的调用。

`setUp` 和 `tearDown` 很简单。在 `Mac_Calc_Tests.m` 中的 `testAddition` 源代码里 ，将四行以 `// obtain the app variable for test access` 开头的代码剪切下来，并将它们粘贴到模板提供的默认的 `setUp` 实例方法中。

```objective-c
- (void)setUp

{

    [super setUp];

    // Put setup code here. This method is called before the invocation of each test method in the class.

 

   // obtain the app variables for test access

   app                  = [NSApplication sharedApplication];

   calcViewController   = (CalcViewController*)[[NSApplication sharedApplication] delegate];

   calcView             = calcViewController.view;

}
```

现在就可以使用最少的重复代码添加更多的测试方法：`testSubtraction` 以及其他。

![2-12](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-qs-10_2x.png)

##总结
当你看完这篇简短的快速开始，会发现向项目添加测试很简单。这里有几个要注意的地方:

1.Xcode配置好了大部分基本的测试设置。当你添加一个新的测试目标，Xcode 会自动将它添加到相关的产品目标的方案中。在测试导航中你会找到目标中包含一个初始化的有一个测试方法的测试类。

2.测试导航面板可以很方便的定位和编辑测试方法。你可以使用导航面板里的指示按钮快速运行测试，或在测试类实现打开时直接在资源编辑器中运行。当测试失败，测试导航面板中的标识跟源码编辑器中错误的地方会相互对应。

3.单个测试方法可以包括多个断言，导致单个通过或失败结果。这个途径可让你根据项目需要创建简单或者非常复杂的测试。

4.`setUp` 和 `tearDown` 实例方法为你提供了一种途径来把相同的代码用在很多个测试方法中，从而获得更高的一致性，并简化调试。


[^1]: 测试导航：Test navigator
[^2]: 事件导航：Issue navigator
[^3]: 调试导航：Debug navigator
[^4]: 方案 Scheme
[^5]: 实现 Implementation