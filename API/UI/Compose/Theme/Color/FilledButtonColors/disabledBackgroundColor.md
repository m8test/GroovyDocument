功能:

+ 设置按钮未启用时的背景颜色.

定义:

+ [FilledButtonColors](/API/UI/Compose/Theme/Color/FilledButtonColors/README.md) disabledBackgroundColor(
  Closure closure)

参数:

+ Closure closure - 设置颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [FilledButtonColors](/API/UI/Compose/Theme/Color/FilledButtonColors/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [FilledButtonColors.disabledBackgroundColor()](/API/UI/Compose/Theme/Color/FilledButtonColors/README.md?id=disabledBackgroundColor)
  方法设置按钮未启用时的背景颜色.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Button() 用于创建 Button 可组合项
    Button {
        // delegate -> Button
        // Button.enabled() 用于设置是否启用按钮
        enabled(false)
        // Button.colors() 用于设置按钮颜色
        colors {
            // delegate -> FilledButtonColors
            // FilledButtonColors.disabledBackgroundColor() 用于设置按钮未启用时的背景颜色
            disabledBackgroundColor {
                // delegate -> Color
                // Color.red() 用于配置红色通道
                red(255)
            }
        }
        // Button.content() 用于设置按钮内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Button")
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