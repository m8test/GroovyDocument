功能:

+ 设置悬浮按钮内容颜色.

定义:

+ [FloatingActionButton](/API/UI/Compose/Widget/FloatingActionButton/README.md) contentColor(Closure
  closure)

参数:

+ Closure closure - 设置颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [FloatingActionButton](/API/UI/Compose/Widget/FloatingActionButton/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [FloatingActionButton.contentColor()](/API/UI/Compose/Widget/FloatingActionButton/README.md?id=contentColor)
  方法设置悬浮按钮内容颜色.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.FloatingActionButton() 用于创建 FloatingActionButton 可组合项
    FloatingActionButton {
        // delegate -> FloatingActionButton
        // FloatingActionButton.contentColor() 用于设置悬浮按钮内容颜色
        contentColor {
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }
        // FloatingActionButton.content() 用于设置悬浮按钮内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("+")
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