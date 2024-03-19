功能:

+ 设置按钮边框.

定义:

+ [Button](/API/UI/Compose/Widget/Button/README.md) border(Closure closure)

参数:

+ Closure closure - 设置边框的闭包
    + 参数 - 无
    + delegate - [BorderStroke](/API/UI/Compose/Graphics/BorderStroke/README.md)

返回值:

+ [Button](/API/UI/Compose/Widget/Button/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Button.border()](/API/UI/Compose/Widget/Button/README.md?id=border) 方法设置按钮边框.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Button() 用于创建 Button 可组合项
    Button {
        // delegate -> Button
        // Button.border() 用于设置按钮边框
        border {
            // delegate -> BorderStroke
            // BorderStroke.width() 用于设置边框宽度
            width(5)
            // BorderStroke.color() 用于设置边框颜色
            color {
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