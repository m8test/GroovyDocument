功能:

+ 设置行高。

定义:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) lineHeight(Number size, String unit)

参数:

+ Number size - 需要设置的尺寸大小
+ String unit - 尺寸单位,可选值有 sp 和 em

返回值:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [TextStyle.lineHeight()](/API/UI/Compose/Theme/Typography/TextStyle/README.md?id=lineHeight) 方法设置行高。

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Text() 用于创建文本可组合项
    Text {
        // delegate -> Text
        // Text.text() 用于设置文本可组合项内容
        text("M8Test是一款免ROOT且功能强大的自动化测试软件,支持无障碍,ADB自动化,集成OpenCV支持图色查找,支持多种语言编写脚本,具有非常详细的文档,每个api都有例子,采用声明式UI,直接通过代码编写UI,无需xml")
        // Text.style() 用于配置文本样式
        style {
            // delegate -> TextStyle
            // TextStyle.lineHeight() 用于设置行高。
            lineHeight(10, "sp")
            // TextStyle.fontSize() 用于设置字体大小
            fontSize(20, "sp")
        }
    }
}
// Activity.onDestroy() 方法用于监听Activity销毁
$composeActivity.onDestroy {
    // Script.stop() 方法用于停止脚本
    $script.stop()
}
// Activity.start() 用于启动Android系统的Activity
$composeActivity.start()
```