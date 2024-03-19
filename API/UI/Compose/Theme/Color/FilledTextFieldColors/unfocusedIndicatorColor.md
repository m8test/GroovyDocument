功能:

+ 设置输入框失去焦点时指示器颜色.

定义:

+ [FilledTextFieldColors](/API/UI/Compose/Theme/Color/FilledTextFieldColors/README.md)
  unfocusedIndicatorColor(Closure closure)

参数:

+ Closure closure - 设置颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [FilledTextFieldColors](/API/UI/Compose/Theme/Color/FilledTextFieldColors/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [FilledTextFieldColors.unfocusedIndicatorColor()](/API/UI/Compose/Theme/Color/FilledTextFieldColors/README.md?id=unfocusedIndicatorColor)
  方法设置输入框失去焦点时指示器颜色.

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
                value("TextField")
                // TextField.colors() 用于设置输入框颜色.
                colors {
                    // delegate -> FilledTextFieldColors
                    // FilledTextFieldColors.unfocusedIndicatorColor() 用于设置输入框失去焦点时指示器颜色
                    unfocusedIndicatorColor {
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