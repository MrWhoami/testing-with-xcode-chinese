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

## 编写异步操作测试
测试是同步执行的因为每个测试都是被依次独立调用的。但是越来越多的代码是异步执行的，为了处理这些异步方法和功能的组件,XCTest 在 Xcode 6 通过等待一个异步回调的完成或超时增加了连续异步执行测试方法的能力。

一份示例源代码：

```objective-c
// Test that the document is opened. Because opening is asynchronous,
// use XCTestCase's asynchronous APIs to wait until the document has
// finished opening.
- (void)testDocumentOpening
{
   // Create an expectation object.
   // This test only has one, but it's possible to wait on multiple expectations.
   XCTestExpectation *documentOpenExpectation = [self expectationWithDescription:@"document open"];

   NSURL *URL = [[NSBundle bundleForClass:[self class]]
                             URLForResource:@"TestDocument" withExtension:@"mydoc"];
   UIDocument *doc = [[UIDocument alloc] initWithFileURL:URL];
   [doc openWithCompletionHandler:^(BOOL success) {
       XCTAssert(success);
       // Possibly assert other things here about the document after it has opened...

       // Fulfill the expectation-this will cause -waitForExpectation
       // to invoke its completion handler and then return.
       [documentOpenExpectation fulfill];
   }];

   // The test will pause here, running the run loop, until the timeout is hit
   // or all expectations are fulfilled.
   [self waitForExpectationsWithTimeout:1 handler:^(NSError *error) {
       [doc closeWithCompletionHandler:nil];
   }];
}
```

更多编写异步操作测试方法的细节，参见 `XCTest.framework` 中的 `XCTestCase+AsynchronousTesting.h` 头文件。

## 编写性能测试
性能测试包括一块代码，这块代码将被评估并被运行十次，然后收集平均运行时间和标准差。这些测量平均出的结果将被用来和一个基准线进行比较从而评估成功或失败。

> **注意：**基准线是你指定的用来衡量测试是成功还是失败的变量，报告界面会提供一个机制来设置或修改基准线。

为了实现性能测试，你需要用 XCode 6 及之后版本提供的新 API  来编写方法。

```	objective-c
- (void)testPerformanceExample {
    // This is an example of a performance test case.
    [self measureBlock:^{
        // Put the code you want to measure the time of here.
    }];
}
```

下面的简单例子是一个测试计算器示例应用加法速度的性能测试。包括一个给定次数迭代的 `measureBlock:` 被添加到了 XCTest 中。

```objective-c
- (void) testAdditionPerformance {
    [self measureBlock:^{
        // set the initial state
        [calcViewController press:[calcView viewWithTag: 6]];  // 6
        // iterate for 100000 cycles of adding 2
        for (int i=0; i<100000; i++) {
           [calcViewController press:[calcView viewWithTag:13]];  // +
           [calcViewController press:[calcView viewWithTag: 2]];  // 2
           [calcViewController press:[calcView viewWithTag:12]];  // =
        }
    }];
}
```

性能测试运行之后的信息会显示在你浏览实现文件时的源代码编辑器的中，测试导航栏中以及报告导航栏中。点击信息回现实每次运行的值。结果显示包括将结果作为将来测试的基准的设置。基准线基于设备设置保存，因此你可以在几个不同的设备上进行相同的测试，每个测试有基于特定设置的处理器速度、内存等等的不同的基准线。

> **注意：**性能测试总是会在第一次运行的时候报告失败，直到一个基准线的值基于特定设备的配置文件被设置好。

性能测试方法编写的更多细节，参见 `XCTest.framework` 的 `XCTestCase.h` 头文件。

## 编写 UI 测试
通过 XCTest 创建 UI 测试是创建单元测试所使用的编程模型的一个扩展，总的来说二者有相似的操作和编程方法。工作流程和实现的区别集中在 UI 记录和 XCTest UI 测试 API 的使用，这些在 [用户交互界面测试](9-UserInterfaceTesting.md) 中有详细描述。

## 使用 Swift 编写测试
Swift 的访问控制模型阻止了测试访问应用或框架内部的声明。为了在 Xcode 6 中通过 Swift 访问内部的功能，你需要为测试把入口声明为公用的，从而削弱 Swift 的类型安全。

Xcode 7 为这一问题提供了一种两部分的解决方案：

1. 通过告知编译器相关信息使得在为测试进行编译时 Swift 内部被设置为可访问的。编译的的变化通过一个新的 `-enable-testing` 标记进行控制，在 Xcode 执行你测试的编译时被给出。`Enable Testability` 编译设置控制这一行为，新的项目默认被置为 `Yes`，这不需要你改变任何源代码。
2. 测试入口的可见性被限定在通过修改 `import` 表述来请求测试的客户端。通过 `import` 新的 `@testable` 属性实现这一修改，这个对你测试代码的修改是一次性的，不需要你修改应用的代码。

举个例子， 有一个 Swift 模块是应用中 `AppDelegate` 的实现，应用叫做 “MySwiftApp.”

```swift
import Cocoa
@NSApplicationMain
class AppDelegate: NSObject, NSApplicationDelegate {
    @IBOutlet weak var window: NSWindow!
   func foo() {
       println("Hello, World!")
   }
}
```

为了写一个可以访问 `AppDelegate` 类的测试类，你需要像下面这样修改你测试代码中的 `import` 表述，添加 `@testable` 属性。

```swift
// Importing XCTest because of XCTestCase
import XCTest

// Importing AppKit because of NSApplication
import AppKit

// Importing MySwiftApp because of AppDelegate
@testable import MySwiftApp

class MySwiftAppTests: XCTestCase {
   func testExample() {
       let appDelegate = NSApplication.sharedApplication().delegate as! AppDelegate
       appDelegate.foo()
   }
}
```

通过这一解决方案，你的 Swift 应用代码的内部功能在你的测试类和方法中都是可以访问的。通过 `@testable` 获取访问权确保了其他的非测试用户不会侵犯 Swift 访问控制规则，即便是在测试编译过程中。

> **注意：**`@testable` 提供的访问权限仅限于“内部”功能，“私有”声明在文件外是不可见的，即便使用了 `@testable`。

## <a name="XCTest-assertions"></a>XCTest 断言
你的测试方法使用 XCTest 框架提供的断言来呈现 Xcode 显示的测试结果。所有断言都有一个相似的形式：项目比较或逻辑表达式，一个失败结果的字符串格式，和插入到字符串格式中的参数。

> **注意：**所有断言的最后一个参数都是 `format...`，一个格式字符串和变量参数列表。XCTest 为所有断言提供了默认的失败结果字符串，可使用参数传递到断言里。`format` 字符串提供了额外的失败自定义描述，你可以使用它提供进一步的描述。这个参数是可选的，可以被忽略。
    
比如，[快速开始](2-快速开始-QuickStart.md)里 `testAddition` 方法中的断言：

```objective-c
XCTAssertEqualObjects([calcViewController.displayField stringValue], @"8", @"Part 1 failed.");
```

阅读这段简单明了的语句：*“当一个字符串被控制器的显示域创建并且与引用参照‘8’不同，则运行失败。”*如果断言失败，那么 Xcode 在测试导航面板发出失败信号，然后 Xcode 会在 事件导航面板、源码编辑器以及其他地方显示失败的描述。下面是源代码编辑器中典型的断言结果：

![](https://developer.apple.com/library/ios/documentation/DeveloperTools/Conceptual/testing_with_xcode/Art/twx-test_failure_assert_result_2x.png)

一个测试方法可以包含多个断言，如果它包含的任何断言报告了失败，Xcode 都会发出的测试方法失败信号。

断言分为五种类型：无条件失败、等价测试、nil 测试、布尔值测试以及异常测试。例如：

### 无条件失败
**XCTFail**。生成一个无条件失败

     XCTFail(format...)

### 等价测试
**XCTAssertEqualObjects**。当 `expression1` 不等于 `expression2` 时报错。这个测试是针对标量的。

     XCTAssertEqual(expression1, expression2, format...)

XCTest 断言的所有类别参见 [分类断言列表](#assertions-listed-by-category)。

## 通过 Objective-C 和 Swift 使用断言
当使用 XCTest 断言时，你应该知道编写 Objective-C （以及其它 C 语言衍生的语言）代码和 Swift 代码时断言兼容性和行为的基本区别。理解这些区别有助于简化测试的书写和调试。

进行等价测试的 XCTest 断言被分为两类：比较对象的和比较非对象。举个例子，`XCTAssertEqualObjects` 测试两个解决对象类型的表达式的等价性，`XCTAssertEqual` 测试两个解决标量[^4]类型的表达式的等价性。这一差异在 XCTest 断言中会被标记出来，通过描述中的“这是标量测试”来标明。通过“标量”来标记断言从而提示你这一基本区别，但是对于那些相互兼容的表达式类型这并不是一个确切的描述。

* 对于 Objective-C，标记为标量类型的断言可以和那些能被比较操作符（==, !=, <=, <, >=, >）使用的类型一起使用。如果表达式要解决 C 类型、结构或者数组使用上述操作符的比较，被视为一个标量。
* 对于 Swift，标记为标量类型的断言可以被用来比较任意满足 `Equatable` 协议（用于所有的“相等”和“不等”断言）和 `Comparable` 协议（用于“大于”和“小于”断言）。此外标记为标量类型的断言可以覆盖 `[T]` 和 `[K:V]`，这里 `T`、`K`、`V` 表示 `Equatable` 和 `Comparable` 协议。例如，等式类型的数组与 `XCAssertEqual` 相匹配，而键值和值均为比较类型的字典与 `XCAssertLessThan` 相匹配。

**注意：**Swift 语言中，`NSObject` 可以用于等式类型，所以不必要使用 `XCTAssertEqualObjects`。

在你的测试中使用 XCTest 断言根据语言不同也会有区别，因为不同语言对待数据类型和隐式转换的方式不同。

* 对于 Objective-C，在 XCTest 实现中使用隐式类型转换允许独立与表达式数据类型的操作数比较，并且没有输入类型检查。
* 对于 Swift，隐式转换是不被允许的因为 Swift 对于类型安全要求更严格。比较的两个参数必须是相通的类型。类型不匹配会在编译的时候在源代码编辑器中被标记出来。

## <a name="assertions-listed-by-category"></a>用类别区分断言
XCTestAssertions 被分为了五个类别，无条件失败、等价测试、空测试、布尔测试、异常测试。

下面列出了 XCTest 断言。你可以在 Xcode 中使用 Quick Help 查看 `XCTestAssertions.h` 来获得更多关于 XCTest 断言的信息。

### 无条件失败
`XCTFail`。生成一个无条件失败

     XCTFail(format...)


### 等价测试
**XCTAssertEqualObjects**。当 `expression1` 不等于 `expression2` 时报错（或者一个对象为空，另一个不为空）。

     XCTAssertEqualObjects(expression1, expression2, format...)

**XCTAssertNotEqualObjects**。当 `expression1` 等于 `expression2` 时报错。

     XCTAssertNotEqualObjects(expression1, expression2, format...)

**XCTAssertEqual**。当 `expression1` 不等于 `expression2` 时报错，这个测试用于标量。

     XCTAssertEqual(expression1, expression2, format...)

**XCTAssertNotEqual**。当 `expression1` 等于 `expression2` 时报错，这个测试用于标量。

     XCTAssertNotEqual(expression1, expression2, format...)

**XCTAssertEqualWithAccuracy**。当 `expression1` 和 `expression2` 之间的差别高于 `accuracy` 时报错。这种测试适用于 floats 和 doubles 这些标量，这些标量两者之间的细微差异导致它们不完全相等，但是对所有的标量都有效。

     XCTAssertEqualWithAccuracy(expression1, expression2, accuracy, format...)

**XCTAssertNotEqualWithAccuracy**。当 `expression1` 和 `expression2` 之间的差别低于 `accuracy` 时报错。这种测试适用于 floats 和 doubles 这些标量，这些标量两者之间的细微差异导致它们不完全相等，但是对所有的标量都有效。 

     XCTAssertNotEqualWithAccuracy(expression1, expression2, accuracy, format...)

### Nil(空)测试
**XCTAssertNil**。当 `expression` 参数非 `nil` 时报错。

    XCTAssertNil(expression, format...)

**XCTAssertNotNil**。当 `expression` 参数为 `nil` 时报错。

    XCTAssertNotNil(expression, format...)
    
### 布尔测试
**XCTAssertTrue**。当 `expression` 计算结果为 `false` 时报错。

    XCTAssertTrue(expression, format...)

**XCTAssert**。当 `expression` 计算结果为 `false` 时报错，与 `XCTAssertTrue` 同义。

     XCTAssert(expression, format...)
     

**XCTAssertFalse**。当 `expression` 计算结果为 `true` 时报错。

     XCTAssertFalse(expression, format...)

###异常测试
**XCTAssertThrows**。当 `expression` 不抛出异常时报错误。

     XCTAssertThrows(expression, format...)
     
**XCTAssertThrowsSpecific**。当 `expression` 针对指定类不抛出异常时报错。

     XCTAssertThrowsSpecific(expression, exception_class, format...)

**XCTAssertThrowsSpecificNamed**。当 `expression` 针对特定类和特定名字不抛出异常时报错。对于 AppKit 或 Foundation 一类的框架非常有用，这一类框架抛出带有特定名字的 `NSException` (`NSInvalidArgumentException` 等等)。

    XCTAssertThrowsSpecificNamed(expression, exception_class, exception_name, format...)

**XCTAssertNoThrow**。当 `expression` 抛出异常时报错。

     XCTAssertNoThrow(expression, format...)

**XCTAssertNoThrowSpecific**。当 `expression` 针对指定类抛出异常时报错。任意其他异常都可以；也就是说它不会报错。

    XCTAssertNoThrowSpecific(expression, exception_class, format...)

**XCTAssertNoThrowSpecificNamed**。当 `expression` 针对特定类和特定名字抛出异常时报错。对于 AppKit 或 Foundation 一类的框架非常有用，这一类框架抛出带有特定名字的 `NSException` (`NSInvalidArgumentException` 等等)。

     XCTAssertNoThrowSpecificNamed(expression, exception_class, exception_name, format...)



[^1]: 开始 Set up，Setup
[^2]: 结束 Tear down
[^3]: 方案 Scheme
[^4]: 标量 Scalar



