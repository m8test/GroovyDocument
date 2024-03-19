功能:

+ 设置输入框错误时边框颜色.

定义:

+ [OutlinedTextFieldColors](/API/UI/Compose/Theme/Color/OutlinedTextFieldColors/README.md) errorBorderColor(
  Closure closure)

参数:

+ Closure closure - 设置颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [OutlinedTextFieldColors](/API/UI/Compose/Theme/Color/OutlinedTextFieldColors/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [OutlinedTextFieldColors.errorBorderColor()](/API/UI/Compose/Theme/Color/OutlinedTextFieldColors/README.md?id=errorBorderColor)
  方法设置输入框错误时边框颜色.

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
                value("OutlinedTextFiled")
                // OutlinedTextField.isError() 用于设置输入框内容是否显示错误样式
                isError(true)
                // OutlinedTextField.colors() 用于设置输入框颜色.
                colors {
                    // delegate -> OutlinedTextFieldColors
                    // OutlinedTextFieldColors.errorBorderColor() 用于设置输入框错误时边框颜色
                    errorBorderColor {
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