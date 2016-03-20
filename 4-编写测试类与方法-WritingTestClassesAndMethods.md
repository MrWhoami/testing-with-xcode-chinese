# 编写测试类与方法
当你使用测试导航面板往项目中添加测试目标时，Xcode 会在测试导航面板里展示出测试类与方法。在测试中，目标是包含测试方法的测试类。本章节将解释如何创建测试类和编写测试方法。

## 测试目标，测试包，测试导航
在学习创建测试类前，有必要看看测试导航面板。它对创建和运行测试工作极为重要。

向一个项目添加测试类会创建一个测试包。测试导航面板罗列了所有测试包里的项目组件内容，并在一个层次列表里展示出测试类和测试方法。下面是一个项目的测试导航面板视图，其包含了两个测试目标，列出了测试包、测试类以及测试方法的嵌套层级。

![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-wtcm-1_2x.png)

测试包可包含多个测试类。你可以使用测试类把测试分到相关的组群中，无论是按照功能分或者按照组织目的分。比如，对于计算器示例项目，你可以创建 `BasicFunctionsTests`、 `AdvancedFunctionsTests` 以及 `DisplayTests` 三个类，但他们都属于 `Mac_Calc_Tests` 测试包。

![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-wtcm-2_2x.png)

一些测试可能会共享某些类型的开始[^1]和结束[^2]需求，把这些测试整合到类里面会更加合理，这样仅使用一组开始和结束方法可以最小化每个测试方法所需的代码。

## 创建测试类
> **注意：**本节着重于说明单元测试类和方法。创建用户交互界面测试目标、类和方法以及它和单元测试有何不同会在 *用户交互界面测试* 里讨论。

使用测试导航面板中的加号按钮（+）创建新测试类。 

![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-wtcm-3_2x.png)

你可以选择添加一个单元测试类或是一个用户交互界面测试类。在你选择其中之一后，Xcode 会显示一个文件类型选择器，其中文件模板已被选好，“New Unit Test Class”模板会在下面的视图中被高亮。点击 Next 以继续。

![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-wtcm-4_2x.png)

其中基于你在配置页面键入的测试类名，你添加的每个测试类都会使得一个名为 *TestClassName*.m 的文件被添加到项目中。

![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-wtcm-5_2x.png)

> **注意：**所有测试类都是 `XCTest` 框架中 `XCTestCase` 类的子类。

尽管 Xcode 会默认的把测试类的实现文件添加到为项目测试目标所创建的组中，你还是可以在项目中组织自己选择的文件。当你按下 Next 按钮，标准的 Xcode 添加文件页面会出现。

![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-wtcm-6_2x.png)

你可以使用添加文件页面就像在项目导航面板中向项目添加文件一样。具体的添加文件页面使用方法参见 [Adding an Existing File or Folder](https://developer.apple.com/library/ios/recipes/xcode_help-structure_navigator/articles/Adding_an_Existing_File_or_Folder.html#//apple_ref/doc/uid/TP40009934-CH17)。

> **注意：**当你创建项目时，一个测试目标和相关的测试包都会默认的被创建，名字根据项目名获得。比如创建名为 `MyApp` 的项目，则会自动生成名为 `MyAppTests` 的测试包，以及一个名为 `MyAppTests` 的测试类，关联在 `MyAppTests.m` 实现文件中。

## <a name="test-class-structure"></a>测试类的结构
测试类包含如下的基本结构：

```objective-c
#import <XCTest/XCTest.h>

@interface SampleCalcTests : XCTestCase
@end

@implementation SampleCalcTests

- (void)setUp {
    [super setUp];
   // Put setup code here. This method is called before the invocation of each test method in the class.
}

- (void)tearDown {
   // Put teardown code here. This method is called after the invocation of each test method in the class.
   [super tearDown];
}

- (void)testExample {
   // This is an example of a functional test case.
   // Use XCTAssert and related functions to verify your tests produce the correct results.
}

- (void)testPerformanceExample {
   // This is an example of a performance test case.
   [self measureBlock:^{
       // Put the code you want to measure the time of here.
   }];
}

@end
```

在本例中测试类是用 Objective-C 实现的，但是也可以用 Swift 实现。

> **注意：**为了连续性，在本文中所有的样例都是用 Objective-C 实现的。  
> Swift 与使用 XCTest 并实现你的测试方法完全兼容。所有的 Swift 和 Objective-C 跨语言实现特性也都可以使用。

注意到实现里包含了实例通过一个基本实现来开始和结束的方法；这些方法不是必须的。如果类中所有的测试方法都需要相同的代码，你可以定制 `setUp` 和 `tearDown` 来包含这些代码。你添加的代码在每个测试方法运行前和运行后执行。你也可以选择向类中添加定制的开始 (+ `(void)setUp`) 和结束 (+ `(void)tearDown`) 方法，他们在类里所有测试方法的运行和运行后执行。

## 测试执行的流程

在执行测试的默认过程中，XCTest 找到所有的测试类（所有测试类继承于 `XCTestCase`，并为每个类运行它的所有测试方法。

> **注意：**有选项可以指定 XCTests 执行的测试，你可以用测试导航或者编辑方案[^3]来禁用测试。你也可以只进行一项测试或一组测试的一个子集，通过测试导航或者源代码编辑器侧栏的运行按钮

对于每个类来说，测试开始于类的开始方法的运行。对于每个测试方法来说，一个新的类实例被创建，它的实例开始方法就会执行，在那之后会运行测试方法，再之后运行实例的结束方法，对类中所有测试方法都如此。在类最后的测试方法结束后，Xcode会执行类的结束方法，并开始下一个类的测试。这种序列一直重复直到跑完所有测试类的所有测试方法。

## 编写测试方法
你通过编写测试方法把测试写到测试类中，测试方法是以 *test* 开头的测试类的实例方法，没有参数，返回 `void`，比如 `(void)testColorIsRed()`。测试方法调用项目中的代码，如果代码没有产生预期的结果，那么会用一系列的断言 API 报错。比如，一个函数返回值可能与预期值相比不同，或者你的测试方法使用了某个类里不适当的方法都将会抛出异常。[XCTest 断言](#XCTest-assertions) 描述了这些情况。

为了使测试方法能够正常访问被测试代码，引入正确的头文件到测试类中很重要。

当 Xcode 运行测试时，它调用的每个测试方法都是独立的。因此每个方法需要准备和清理辅助变量、结构以及与目标 API 进行交互的对象等。如果类中所有测试方法的代码是相同的，你可以直接把它添加到必需的 `setUp` 和 `tearDown` 的实例方法中，详见 [测试类结构](#test-class-structure)。

下面是个单元测试方法的模型:

```objective-c
- (void)testColorIsRed {
   ...     // Set up, call test subject API. (Code could be shared in setUp method.)
   ...     // Test logic and values, assertions report pass/fail to testing framework.
   ...     // Tear down. (Code could be shared in tearDown method.
}
```

这里有一个简单的测试方法例子，检查是否成功地为 SampleCalc 创建了 `CalcView` 实例，应用详见 [快速开始](2-快速开始-QuickStart.md) 章节：


```objective-c
- (void) testCalcView {
   // setup
   app = [NSApplication sharedApplication];
   calcViewController = (CalcViewController*)[NSApplication sharedApplication] delegate];
   calcView             = calcViewController.view;
 
   XCTAssertNotNil(calcView, @"Cannot find CalcView instance");
   // no teardown needed
}    
```

//TODO

## <a name="XCTest-assertions"></a>XCTest断言
你的测试方法使用 XCTest 框架提供的断言来呈现 Xcode 显示的测试结果。所有断言都有一个相似的形式：项目比较或逻辑表达式，一个失败结果字符串格式，和插入到字符串格式中的参数。


>注意：所有断言的最后一个参数是`format...`，格式字符串和变量参数列表。XCTest 为所有断言提供了默认的失败结果字符串，可使用参数传递到断言里。`format`字符串提供了可选的额外的失败自定义描述，就可以进一步选择提供的描述。这个参数是可选的，也可以完全被忽略。
    
    
比如，[Quick Start](https://developer.apple.com/library/mac/documentation/DeveloperTools/Conceptual/testing_with_xcode/testing_1_quick_start/testing_1_quick_start.html#//apple_ref/doc/uid/TP40014132-CH2-SW1)里`testAddition`方法中的断言：

```objective-c
XCTAssertEqualObjects([calcViewController.displayField stringValue], @"10", @"Part 2 failed.");
```

阅读这段简单明了的语句，是说：“Indicate a failure when a string created from the value of the controller’s display field is not the same as the reference string ‘8’” 。如果断言失败，那么 Xcode 在测试导航面板发出失败信号，然后 Xcode 会在 issues 导航面板、源码编辑器以及其他地方展示失败的描述。下面是源代码编辑器中典型的断言结果：

![](https://developer.apple.com/library/mac/documentation/DeveloperTools/Conceptual/testing_with_xcode/art/twx-test_failure_assert_result_2x.png)

测试类可以包含多个断言，如果任何断言包含失败报告，那么 Xcode 都发出的测试失败信号。

断言分为五种类型：无条件失败、等价测试、nil测试、Boolean测试以及异常测试。

##用类别区分断言

下面的区域列出了 XCTest 断言。你可以在 Xcode 中使用 Quick Help 查看`XCTestAssertions.h`来引用来获得更多关于 XCTest 断言的信息。

###无条件失败
__XCTFail__。生成一个无条件失败

     XCTFail(format...)


###等价测试
__XCTAssertEqualObjects__。当_expression1_不等于_expression2_时报错（或者一个对象为空，另一个不为空）。

     XCTAssertEqualObjects(expression1, expression2, format...)

__XCTAssertNotEqualObjects__。当_expression1_等于_expression2_时报错

     XCTAssertNotEqualObjects(expression1, expression2, format...)


__XCTAssertEqual__。当_expression1_不等于_expression2_时报错，这个测试用于C语言的标量。

     XCTAssertEqual(expression1, expression2, format...)

__XCTAssertNotEqual__。当_expression1_等于_expression2_时报错，这个测试用于C语言的标量。

     XCTAssertNotEqual(expression1, expression2, format...)


__XCTAssertEqualWithAccuracy__。当_expression1_和_expression2_之间的差别高于 _accuracy_ 时报错。这种测试适用于 floats 和 doubles 这些标量，两者之间的细微差异导致它们不完全相等，但是对所有的标量都有效。

     XCTAssertEqualWithAccuracy(expression1, expression2, accuracy, format...)

__XCTAssertNotEqualWithAccuracy__。当_expression1_和_expression2_之间的差别低于 _accuracy_ 时报错。这种测试适用于 floats 和 doubles 这些标量，两者之间的细微差异导致它们不完全相等，但是对所有的标量都有效。 


     XCTAssertNotEqualWithAccuracy(expression1, expression2, accuracy, format...)


###Nil(空)测试

__XCTAssertNil__。当_expression_参数非nil时报错。

    XCTAssertNil(expression, format...)

__XCTAssertNotNil__。当_expression_参数为nil时报错。

    XCTAssertNotNil(expression, format...)
    
    
###布尔测试


__XCTAssertTrue__。当_expression_计算结果为_false_时报错。

    XCTAssertTrue(expression, format...)

__XCTAssert__。当_expression_计算结果为_false_时报错，与_XCTAssertTrue_同义。

     XCTAssert(expression, format...)
     

__XCTAssertFalse__。当_expression_计算结果为_true_时报错。

     XCTAssertFalse(expression, format...)


###异常测试

__XCTAssertThrows__。当_expression_不抛出异常时报错误。

     XCTAssertThrows(expression, format...)
     
__XCTAssertThrowsSpecific__。当_expression_针对指定类不抛出异常时报错。

     XCTAssertThrowsSpecific(expression, exception_class, format...)

__XCTAssertThrowsSpecificNamed__。当_expression_针对特定类和特定名字不抛出异常时报错。对于AppKit框架或Foundation框架非常有用，抛出带有特定名字的NSException(NSInvalidArgumentException等等)。

    XCTAssertThrowsSpecificNamed(expression, exception_class, exception_name, format...)


__XCTAssertNoThrow__。当_expression_抛出异常时报错。

     XCTAssertNoThrow(expression, format...)


__XCTAssertNoThrowSpecific__。当_expression_针对指定类抛出异常时报错。任意其他异常都可以；也就是说它不会报错。

    XCTAssertNoThrowSpecific(expression, exception_class, format...)


__XCTAssertNoThrowSpecificNamed__。当_expression_针对特定类和特定名字抛出异常时报错。对于 AppKit 框架或 Foundation 框架非常有用，抛出带有特定名字的NSException(NSInvalidArgumentException等等)。


     XCTAssertNoThrowSpecificNamed(expression, exception_class, exception_name, format...)

[^1]: 开始 Set up，Setup
[^2]: 结束 Tear down
[^3]: 方案 Scheme


