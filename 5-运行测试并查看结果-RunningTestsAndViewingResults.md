# 运行测试并查看结果

正如在[“快速开始”](2-快速开始-QuickStart.md)看到的那样，使用 Xcode 测试导航面板，可以很容易的运行测试并查看其结果。有另外几种运行测试的交互方法。Xcode 运行测试取决于一个方案中包括并开启了哪些测试目标。测试导航面板让你无需使用方案编辑器就能直接控制那些被包含、被开启或被关闭的测试目标、类以及方法。

## 运行测试命令
为了将运行测试作为编码流程的一部分，测试导航面板为提供了便捷的方法。测试可以直接在源代码编辑器里运行，或使用 Product 菜单运行。 

### 使用测试导航面板
在测试导航面板中，将鼠标悬停在测试包、类或方法名上时，会出现一个 “Run” 按钮。你可以运行某个特定测试，也可以运行一个类中的测试或运行一个测试包中的所有测试，这取决于鼠标停留在列表中的位置。

* 将鼠标悬停在测试包名上，并点击右边出现的运行按钮来测试一个包中的所有测试。
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-1_2x.png)
* 将鼠标悬停在类名上，并点击右边出现的运行按钮来测试一个类中的所有测试。
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-2_2x.png)
* 将鼠标悬停在测试名称上，并点击右边出现的运行按钮来测试一个单独的测试。
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-3_2x.png)

### 使用源代码编辑器
当在源代码编辑器中打开一个测试类，每个测试方法名字旁的边栏会有很明显的指示器。在指示器上悬停鼠标，出现一个运行按钮。点击按钮运行该测试方法，指示器随后显示该测试成功或失败的状态。再次将鼠标悬停到指示器上可以再次显示运行按钮来重复测试。这种机制一次只运行一个测试。

![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-4_2x.png)
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-5_2x.png)

>**注意：**出现在 `@implementation` 旁边的指示器同样也适用于类，允许你运行类中所有的测试。

### 使用 Product 菜单

Product 菜单包括了从键盘直接运行测试的快捷命令。

**Product > Test**。运行当前激活的方案（scheme）。键盘快捷键是 Command-U。

**Product > Build for > Testing** 和 **Product > Perform Action > Test without Building**。这两个命令可以用来构建测试包并运行独立于其它的测试。这是简化构建和测试进程的快捷命令。对于修改了代码并在构建过程中检查警告或错误时，这是特别有用的，或者如果你知道当前的构建是最新的，它也可以加速测试过程。键盘快捷方式分别是 
Shift-Command-U 和 Control-Command-U。

**Product > Perform Action > Test**。当你编辑一个测试方法时，这个动态菜单选项展示当前光标所处的测试方法，并允许你使用键盘快捷方式来运行测试。命令的名称取决于将要运行的测试，比如，Product > Perform Action > Test testAddition。快捷键是 Control-Option-Command-U。

>**注意：**除了源代码编辑器，该命令还基于工程导航面板和测试导航面板中的选择情况运行。当任何一个导航面板处于激活状态，源代码编辑器就失去了焦点，并且该命令将使用任何一个导航面板中的当前选择作为输入。  
>在测试导航面板中，可以选择测试包，类或方法。在工程导航面板中，可以选择测试类实现文件，例如 `CalcTests.m`。

**Product > Perform Action > Test Again <testName>**。当测试方法在调试/编辑代码中暴露出问题时，返回最后一个被执行的测试方法非常有用。像 Product > Perform 
Action > Test 命令，运行的测试名称在命令中出现，例如，Product > Perform Action > Test Again testAddition。键盘快捷方式是 Control-Option-Command-G。

## 测试结果的显示
XCTest 框架有几种不同的方式在 Xcode 中展示测试结果。下面的屏幕截图展示了从哪里查看这些结果。 

* 在一个或一组测试运行后，你可以在测试导航面板中浏览 测试通过/失败指示。
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-6_2x.png)  
如果测试方法被折叠到各自的类中，或测试类被折叠到测试包中，该标识则反映了封闭测试的集合状态。在本例中，`BasicFunctionsTests` 类中至少有一个方法被标记为失败。
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-7_2x.png)

* 在源代码编辑器中，你可以浏览测试通过/失败标识和调试信息。
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-results-srceditor_2x.png)

* 在报告导航面板中，你可以浏览相关的错误描述和其他一些输出摘要。在测试面板被激活时，你可以在左侧的导航面板中选择你想要检查的测试。  
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-8_2x.png)  
对于性能测试，点击时间轴上的值可以获取性能结果的详细报告。你既可以查看总计的测试性能，也可以通过点击各个测试按钮看到十次运行中每次的值。你可以使用 Edit 按钮设置运来区分通过或失败的测试基准线和最大标准误差。  
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-10_2x.png)  
使用日志面板时，你可以浏览相关的失败描述和其他输出概要。点击左边的三角符号，你可以展开测试运行的细节。  
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-9_2x.png)

>**注意：**除了左边展开的三角图标，测试失败项右边的小图标可以展开以显示更多信息，正如上图显示的 `testMultiplication` 失败。

* 调试控制台以文本形式展示了测试运行的综合信息。这些信息和日志导航面板中显示的信息一样，但如果你已经处于调试状态，那么调试的输出也会出现在这里。
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-11_2x.png)

## 使用方案和测试目标

Xcode 方案控制着构建、运行、测试和调试这些菜单命令的行为。当创建测试目标并使用测试导航面板执行其他测试系统操作时，Xcode 为我们管理方案配置--例如，当你开启或关闭一个测试方法、测试类或测试包时。使用 Xcode Server 和持续集成需要通过设置方案管理页面中的复选框来将一个方案设置成共享，并将其连同你的工程和源代码导出到一个源文件仓库。

方案配置方法如下:

1. 选择 Scheme menu > Manage Schemes，弹出方案管理页。  
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-12_2x.png)  
这个工程中有两个方案，一个用来构建应用，一个用来构建框架/库。右侧的 Shared 复选框用来将方案配置为共享，并允许 Xcode Server 机器人使用。 
2. 在管理页中，双击一个方案，显示方案编辑器。一个方案的测试行为标识了你执行测试命令时 Xcode 执行的测试。
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-13_2x.png)

>**注意：**测试目标、测试类和测试方法所关联的测试导航面板和配置/设置助手通常维护所有关于测试操作的方案设置。 

关于使用、配置和编辑方案的更多信息可以查看 [Scheme Configuration Help](https://developer.apple.com/library/ios/recipes/xcode_help-scheme_editor/_index.html#//apple_ref/doc/uid/TP40010402)，或者视频 [WWDC 2012: Working with Schemes and Projects in Xcode](https://developer.apple.com/videos/wwdc/2012/?id=408)。

## 构建设置--测试应用，测试库

应用测试在你应用的上下文中运行，允许你创建测试，这些测试结合了来自不同类、库/框架和应用功能角度的行为。库测试独立于你的应用，在一个库或框架中采用实验类和方法，来验证他们的行为符合库的明确要求。

两种类型的测试包需要不同的构建设置。在新 target 助手中通过选测目标参数来创建测试目标时，会执行构建设置配置。目标助手随着目标下拉菜单显示。名为 `SampleCalc` 的应用和名为 `CalcLibrary` 的库可供选择。

![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-14_2x.png)

选择 `SampleCalc` 作为改测试目标所关联的构建产品会使构建设置用来测试一个应用。测试的执行基于应用进程；测试在得到 `applicationDidFinishLaunching` 通知后执行。默认的产品名称 "SampleCalc Tests" 来自于目标名 `SampleCalc`，你可以根据自己的偏好改变它。

如果你选择 `CalcLibrary` 作为关联的构建产品，目标助手将会配置构建设置来测试库。Xcode 引导测试运行时的上下文和框架/库，以及你的测试代码--基于一个 Xcode 管理的进程。这种情况下默认的产品名字来自于库目标 (“CalcLibrary Tests”)。同样，你可以基于自己的喜好修改。

### 默认构建设置

大多数情况下，配置构建设置来测试应用或库所要做的唯一一件事就是选择正确的测试目标。Xcode 则自动关注构建设置管理。因为你可能有一个需要复杂构建设置的工程，所以了解 Xcode 为应用测试和库测试所建立的标准构建设置是非常有用的。

我们使用 `SampleCalc` 工程作为例子来演示正确的默认设置。

1. 在工程导航面板中单击 `SampleCalc` 进入工程编辑器，然后选择 `SampleCalcTests` 应用测试目标。在编辑器的通用面板中，有一个目标快捷菜单。该下拉菜单应当展示以 `SampleCalc` 为目标。  
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-15_2x.png)  
你可以检查该构建设置是否正确。

2. 点击构建设置，在搜索框中输入 `Bundle Loader`。针对 `SampleCalc` 的应用测试被 `SampleCalc` 应用加载。你可以看到针对 Debug 和 Release 的作为自定义参数的可执行文件路径。  
搜索 `Test Host` 也可以看到相同的路径。
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-runtst-16_2x.png)

该工程的库目标名为 `CalcLibrary`，并且已经与名为 `CalcLibraryTests` 的测试目标关联。 

3. 选择 `CalcLibraryTests` 目标并查看通用面板。  
目标应被设置为 `None`。与之类似，你可以使用构建设置面板查看 `Bundle Loader` 和 `Test Host` 构建设置，下图显示 Bundle Loader 搜索设置。这表明 Xcode 已经默认正确地配置了它们。
