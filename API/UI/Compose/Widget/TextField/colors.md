功能:

+ 设置输入框颜色.

定义:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) colors(Closure closure)

参数:

+ Closure closure - 设置颜色的闭包
    + 参数 - 无
    + delegate - [FilledTextFieldColors](/API/UI/Compose/Theme/Color/FilledTextFieldColors/README.md)

返回值:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [TextField.colors()](/API/UI/Compose/Widget/TextField/README.md?id=colors) 方法设置输入框颜色.

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
            // Slot.TextField() 用于创建 TextField 可组合项
            TextField {
                // delegate -> TextField
                // TextField.value() 用于设置输入框内容
                value("red color")
                // TextField.colors() 用于设置输入框颜色.
                colors {
                    // delegate -> FilledTextFieldColors
                    // FilledTextFieldColors.textColor() 用于设置文本颜色
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