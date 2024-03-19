功能:

+ 创建 [OutlinedButton](/API/UI/Compose/Widget/OutlinedButton/README.md) 可组合项

定义:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) OutlinedButton(Closure closure)

参数:

+ Closure closure - 设置 [OutlinedButton](/API/UI/Compose/Widget/OutlinedButton/README.md) 的闭包
    + 参数 - 无
    + delegate - [OutlinedButton](/API/UI/Compose/Widget/OutlinedButton/README.md)

返回值:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Slot.OutlinedButton()](/API/UI/Compose/Slot/Slot/README.md?id=OutlinedButton) 方法创建
  [OutlinedButton](/API/UI/Compose/Widget/OutlinedButton/README.md) 可组合项

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.OutlinedButton() 用于创建 OutlinedButton 可组合项
    OutlinedButton {
        // delegate -> OutlinedButton
        // OutlinedButton.colors() 用于设置带轮廓按钮颜色
        colors {
            // delegate -> OutlinedButtonColors
            // OutlinedButtonColors.contentColor() 用于设置带轮廓按钮内容颜色
            contentColor {
                // delegate -> Color
                // Color.red() 用于配置红色通道
                red(255)
            }
        }
        // OutlinedButton.content() 用于设置带轮廓按钮内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("OutlinedButton")
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