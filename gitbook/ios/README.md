理解iOS的无障碍特性
===============================

> 翻译：[umcsdon](https://github.com/zac1st1k)

从一开始，基于iOS的设备就包含了很多使得大家都能很容易地使用iOS设备的特性。其中包括可视化的语音留言信箱，邮件大字体，网页、照片、地图缩放。通过引入以下的无障碍特性，有视碍、听碍、肢体残障的人士甚至可以更加方便的使用他们的设备。

- 缩放。放大整个设备屏幕。
- 黑白转换。转换屏幕的颜色。
- 单声道化。把左右声道混合成一个信号，在左右耳播放。
- 自动文本播报。当用户打字时，自动播放文本纠错与候选建议。
- 语音控制。允许用户使用语音命令来打电话和控制iPod回放。

此外，视障用户靠VoiceOver的帮助来使用设备。

# 无障碍特性与VoiceOver

VoiceOver 是苹果公司创新的读屏技术，通过这个技术，用户无需看屏幕就可以控制设备。VoiceOver在用户界面与用户触控之间充当媒介，描述了应用程序中的元素与行为。当VoiceOver激活时，用户无需担心意外地删除了联系人或者拨打了电话，因为VoiceOver会提醒用户界面位置，他们可以操作什么，结果如何。

一个程序是不是无障碍的，取决于用户可以交互的所有界面元素是否是无障碍的。一个界面元素是否是无障碍的取决于它是否在恰当的时候告知用户它是一个无障碍的元素。

一个无障碍的界面元素必须准确提供关于它的信息才能被使用。这些信息包括它在屏幕的位置、名称、行为、值和类型。这正是VoiceOver播报给用户的信息。iOS SDK包含了编程接口和工具，来帮你确保程序中的用户界面元素是无障碍且好用的（更多信息，请查看“iOS无障碍API与工具”（第7页））。

# 为什么写没有障碍的应用

你应该让你你的iPhone应用能被VoiceOver的用户们无障碍的使用，因为：

- 这会增加你的用户基数。你已经努力的创造优秀的程序，不要错过让你的程序能被更多用户使用的机会。
- 无障碍应用可以使你的用户无需看屏幕。视障用户可以通过VoiceOver的帮助来使用的你的应用。
- 写无障碍程序使你理解无障碍准则。很多管理部门编写了无障碍准则，你为VoiceOver用户编写无障碍的iPhone应用能帮助你满足这些准则。
- 这是正确的决定。

支持无障碍特性不会影响你创造优异iPhone应用的能力，记得这点非常重要。为用户界面编程接口增加薄薄的一个功能层，不会改变应用的外观，也不会妨碍到应用的主要逻辑。

#iOS无障碍API与工具

iOS 3.0及之后的版本包含了用户界面无障碍编程接口，这个轻量级的API可以让应用提供全部所需信息，让VoiceOver来给用户描述界面，以帮助视障用户使用应用。
用户界面无障碍编程接口是UIKit的一部分，默认通过标准UIKit控件和视图来实现。也就是说，当你使用标准的控件和视图时，大部分使应用无障碍的工作都已经完成了。编无障碍程序可以简单到只是给用户接口元素提供准确易懂的描述，简单的程度取决于你程序自定义的程度。

iOS SDK也提供工具来帮你编写无障碍应用：
- 当你设计nib文件时，Interface Builder观察器面板提供了一个简单的方式来添加描述性的无障碍信息。想进一步了解如何添加这些信息，请看”在Interface Builder中添加自定义属性信息“（第19页）。
- Accessibility Inspector可以显示嵌入到应用用户界面中的无障碍信息，你可以在iOS模拟器中运行应用来验证这些信息。想进一步了解如何检查应用中的无障碍信息，请看“在iOS模拟器中使用Accessibility Inspector来除错”。

此外，你可以使用VoiceOver本身来测试应用的无障碍功能。想学习如何用VoiceOver来测试你的应用，请看“用VoiceOver在你的设备上测试无障碍信息”。

#UI无障碍编程接口

UI无障碍编程接口包含两个非正式协议，一个类，一个函数，还有一些常量。

- UIAccessibility非正式协议。实现UIAccessibility协议的对象可以报告无障碍状态（即他们是否是无障碍的）并且提供关于他们的描述性信息。UIAccessibility协议默认由标准UIKit控件和视图实现。
- UIAccessibilityContainer非正式协议。此协议通过子类UIView来使它所包含的部分或者全部对象是无障碍的分离元素，当非UIView子类的对象被UIView视图包含时，这些元素不会自动变成无障碍元素，此时UIAccessibilityContainer协议就非常有用。
- UIAccessibilityElement类。定义了一个对象是否能通过UIAccessibilityContainer协议返回。你可以创建UIAccessibilityElement实例来代表无法自动变为无障碍的元素，例如一个没有继承自UIView的对象，或者一个不存在的对象。
- UIAccessibilityConstants.h头文件。此头文件定义了用来描述某些特征的常量。这些常量即可展示的无障碍元素，还有可被应用发布的通知。

#无障碍属性

用来描述无障碍用户界面元素的无障碍属性构成了UI Accessibility API的核心。当用户访问或操作控件和视图时，VoiceOver会告知用户无障碍属性的相关信息。

因为无障碍属性封装了区分不同控件和视图的信息，所以无障碍属性也是你最有可能用到的编程接口的组件。就标准UIKit控件和视图来说，确保应用中默认的属性信息准确可能就够了。就自定义的控件和视图来说，或许要添加大部分的属性信息。

UI Accessibility 编程接口定义了如下属性。

- **标签**。一个简短的本地化词或短语，此短语简洁地描述控件或者视图，但是不能识别元素类型。例如“添加”、“播放”。
- **特征**。一个或多个独立特征的组合。每个特征描述一个元素状态、行为、使用中的某一方面。例如当元素的行为如同被选中键盘上的按键，这个元素就有了Keyboard Key和Selected的组合特征。
- **提示**。一个简短的本地化短语，描述发生在元素上动作的结果。例如“添加标题”或者“打开购物列表”。
- **框架**。元素在屏幕上坐标的框架。由CGRect结构体提供，详细说明了元素的屏幕位置和大小。
- **值**。不是由标签定义的元素时的当前值。例如，一个幻灯片的标签可以是”速度”，但是它当前的值是“50%”。

无论由你指定还是默认情况，无障碍元素需有无障碍属性值。无障碍元素都要有框架和标签属性。因为无障碍元素必须能够报告它在用户界面上的位置，所以框架属性是强制的。（注意一个由UIView继承的对象默认包含了框架属性值）。因为标签属性包含了VoiceOver播报的无障碍元素的名称和描述，所以它也是强制的。

当提示和特征属性不适用时，就无需这些属性。例如不能触发动作的元素不需提示属性。

仅当元素的内容是可改变并且永不被标签描述时，一个无障碍元素才需要提供给值属性提供内容。例如，一个文本域包含了一个可能有Email标签的Email地址，但是它的内容取决于用户的输入，通常格式为”username@address。“图1-1显示了VoiceOver可以提供了一些信息。

**图 1-1** VoiceOver可以读出由无障碍元素提供的信息。

![alt text](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/iPhoneAccessibility/Art/iphoneax_axinfo_2x.png)

VoiceOver用户靠听标签和提示来使用应用。因此，确保应用中的每一个无障碍元素提供准确全面的描述是极其重要的。标准UIKit控件和视图的默认值信息经常是准确的，但是你应该检查一下确保无误。对于自定义控件和视图，你可能不得不自己提供部分或者全部信息。关于如何去提供这些信息的指导，请看”打造好用的标签和提示“（第16页）。