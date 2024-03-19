功能:

+ 设置文字颜色

定义:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) color(Closure closure)

参数:

+ Closure closure - 设置颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [TextStyle.color()](/API/UI/Compose/Theme/Typography/TextStyle/README.md?id=color)
  方法设置文字颜色

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Text() 用于创建文本可组合项
    Text {
        // delegate -> Text
        // Text.text() 用于设置文本可组合项内容
        text("Text")
        // Text.style() 用于配置文本样式
        style {
            // delegate -> TextStyle
            // TextStyle.color() 用于设置文字颜色
            color {
                // delegate - Color
                // Color.red() 用于配置红色通道
                red(255)
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