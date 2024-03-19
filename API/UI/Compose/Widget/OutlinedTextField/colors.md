功能:

+ 设置输入框颜色.

定义:

+ [OutlinedTextField](/API/UI/Compose/Widget/OutlinedTextField/README.md) colors(Closure closure)

参数:

+ Closure closure - 设置颜色的闭包
    + 参数 - 无
    + delegate - [OutlinedTextFieldColors](/API/UI/Compose/Theme/Color/OutlinedTextFieldColors/README.md)

返回值:

+ [OutlinedTextField](/API/UI/Compose/Widget/OutlinedTextField/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [OutlinedTextField.colors()](/API/UI/Compose/Widget/OutlinedTextField/README.md?id=colors) 方法设置输入框颜色.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Column() 用于创建纵向布局
    Column {
        // delegate -> Column
        // Column.content() 用于设置布局内容
        content {
            // delegate -> Slot
            // Slot.OutlinedTextField() 用于创建 OutlinedTextField 可组合项
            OutlinedTextField {
                // delegate -> OutlinedTextField
                // OutlinedTextField.value() 用于设置输入框内容
                value("red color")
                // OutlinedTextField.colors() 用于设置输入框颜色.
                colors {
                    // delegate -> OutlinedTextFieldColors
                    // OutlinedTextFieldColors.textColor() 用于设置文本颜色
                    textColor {
                        // delegate -> Color
                        // Color.red() 用于配置红色通道
                        red(255)
                    }
                }
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