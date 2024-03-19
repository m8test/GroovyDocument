功能:

+ 配置蓝色通道.

定义:

+ [Color](/API/UI/Compose/Theme/Color/Color/README.md) blue(int value)

参数:

+ int value - 需要设置的值,范围[0-255]

返回值:

+ [Color](/API/UI/Compose/Theme/Color/Color/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Color.blue()](/API/UI/Compose/Theme/Color/Color/README.md?id=blue) 方法配置蓝色通道.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Button() 用于创建 Button 可组合项
    Button {
        // delegate -> Button
        // Button.colors() 用于设置按钮颜色
        colors {
            // delegate -> FilledButtonColors
            // FilledButtonColors.contentColor() 用于设置按钮的内容颜色
            contentColor {
                // delegate -> Color
                // Color.blue() 用于配置蓝色通道
                blue(255)
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