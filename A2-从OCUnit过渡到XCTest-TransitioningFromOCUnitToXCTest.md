# 附录 B：从 OCUnit 过渡到 XCTest

XCTest 是 Xcode 5 中引入的一个测试框架。一些老的项目仍然在使用上一代的测试框架 OCUnit。将你的项目升级到使用 XCTest 使你能够充分利用 XCTest 提供的所有的新特性与能力。

## 从 OCUnit 转换至 XCTest

从 OCUnit 到 XCTest 的转换是一个复杂的操作，包括更新包含测试类和修改的项目配置等源文件。Xcode 中有一个迁移助手可帮你实现这些转换，选择 Edit > Convert > To XCTest。推荐使用迁移助手来地将项目升级至使用 XCTest。
 
OCUnit 到 XCTest 迁移工具在当前的方案下对目标进行转化。迁移工具会检查你选择的目标，并且为了自动转换会进行一系列的源代码更改。
 
> **注意：**建议您在进行 OCUnit 到 XCTest 的迁移时，将一个项目中的所有测试目标都进行转化。

更新项目从 OCUnit 到 XCTest ：

1. 通过方案菜单选择一个构建测试目标的方案。  
举个例子，在老一些的工作空间中有 OS X 和 iOS 的计算机项目，测试是基于 OCUnit 的。使用工具栏的方案编辑器菜单：  
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-OC2XC-1_2x.png)  
在出现的菜单中，选择构建 `Mac_Calc_ApplicationTests` 目标的方案从而使其变成活跃的方案。  
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-OC2XC-2_2x.png)
2. 选择 Edit > Convert > To XCTest。  
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-OC2XC-3_2x.png)
3. 点击 Next，进入到下一个工作表。
4. 在出现的表单中，选择要转换的测试目标。  
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-OC2XC-4_2x.png)  
点击特定目标的名字可以看到在转换后其是否会通过 XCTest 构建。
5. 单击 Next 按钮。  
助手弹出了一个 FileMerge 界面，您可以挨个文件地评估源代码的变化。  
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-OC2XC-5_2x.png)  
左边是更新后的源文件，右边是原始文件。你可以浏览所有可能的变化，并丢弃那些你觉得有问题的变化。
6. 如果你对所有的更改都满意，就可以单击 Save 按钮。  
Xcode 会把更改写入文件。

当转换完成，运行测试目标，并检查其输出，以确保测试按预期运行。如果出现任何问题，请参阅 [调试测试](6-调试测试-DebuggingTests.md) 一章解决。

## 人工从 OCUnit 转换至 XCTest
从 OCUnit 到 XCTest 迁移助手可能不能成功的转化一些项目。在其转换失败的情况下（或是你希望人工将你的测试转换至 XCTest），进行如下操作：

1. 在项目中添加一个新的 XCTest 测试目标。
2. 在新的测试目标中为测试类和方法添加实现文件。
3. 在你的新测试类中编辑 `#import XCTest/XCTest.h` 并在测试方法中使用 XCTest 断言。

使用以上方法确保 XCTest 测试目标对应的项目配置正确。当使用迁移助手时，完成转化后要运行测试目标并检查输出，确保测试如预期般执行。如果出现了任何问题，请参阅 [调试测试](6-调试测试-DebuggingTests.md) 一章解决。
	

