功能:

+ 设置应用于除第一行以外的每一行的缩进量

定义:

+ [TextIndent](/API/UI/Compose/Theme/Typography/TextIndent/README.md) restLine(Number size, String unit)

参数:

+ Number size - 需要设置的尺寸大小
+ String unit - 尺寸单位,可选值有 sp 和 em

返回值:

+ [TextIndent](/API/UI/Compose/Theme/Typography/TextIndent/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [TextIndent.restLine()](/API/UI/Compose/Theme/Typography/TextIndent/README.md?id=restLine)
  方法设置应用于除第一行以外的每一行的缩进量

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
            // TextStyle.textIndent() 用于设置段落缩进
            textIndent {
                // delegate - TextIndent
                // TextIndent.firstLine() 用于设置应用于第一行的缩进量
                firstLine(20, "sp")
                // TextIndent.restLine() 用于设置应用于除第一行以外的每一行的缩进量
                restLine(5, "sp")
            }
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