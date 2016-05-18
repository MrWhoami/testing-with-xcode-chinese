# 代码覆盖
代码覆盖是 Xcode 7 的一个新特性，它使你能可视化地测量你的代码被测试的程度。通过代码覆盖，你能够确定你的测试是否正在做你希望它做的工作。

## 启用代码覆盖
代码覆盖在 Xcode 中是一个 LLVM 支持的测试选项。当你启用了代码覆盖，LLVM 会检测你的代码收集基于方法和功能被调用频率的覆盖数据。代码覆盖选项可以收集正确性和性能测试数据用于报告，无论是单元测试或是 UI 测试。

你可以通过编辑方案的测试行为来启用代码覆盖。

1. 通过方案编辑菜单选择编辑方案。  
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-codecov-1_2x.png)
2. 选择 Test 行为。
3. 通过 Code Coverage 复选框启用代码覆盖以收集覆盖数据。  
![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-codecov-3_2x.png)
4. 点击 Close。

> **注意：**代码覆盖数据收集会导致一定的性能损失。无论损失是否显著，代码执行时的影响应该是线性的，所以性能结果在启用了该功能后依旧是可以彼此比较的。然而，当你在严谨地通过测试评估性能表现时，你仍应该考虑是否开启代码覆盖。

## 代码覆盖如何融入测试
代码覆盖是一个用来评价你的测试的价值的工具。它回答了以下问题：

* 当你运行你的测试时，实际上有哪些代码在执行？
* 需要进行多少测试才够？  
换句话说，你是否设计了足够多的测试确保你所有的代码都进行了正确性和性能测试？
* 你代码的那些部分没有被测试？

在一个测试完成后，Xcode 得到 LLVM 的覆盖数据并用这些数据在报告导航栏创建了一个覆盖报告，可以在 Coverage 面板看到。这个报告展示了测试运行的概要信息，一个源代码文件的列表和文件中的函数，以及每一个的覆盖比例。

![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-codedov-4_2x.png)

源代码编辑器显示文件中每一行代码的计数，没有执行的代码会被高亮。它会高亮需要覆盖的代码而不是已经覆盖的代码。

举个例子，将光标悬浮在覆盖报告的 `-[Calculator input:]` 方法之上，会出现一个按钮，这个按钮会把你带到标注的源代码处。

![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-codedov-5_2x.png)

覆盖标注在编辑器的右侧，显示各部分代码在运行中被调用多少次，如下：

![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-codedov-6_2x.png)

从上面的计数可以看出，`input:` 方法在测试中被频繁调用，然而，方法有一些部分没有被调用，这在源代码编辑器中被明显地标记了出来，如下：

![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-codedov-7_2x.png)

这个报告的数据和标注提供了编写一个包含不应出现或非法字符的测试的机会，以此来确定错误处理是否如预想一般地工作。
