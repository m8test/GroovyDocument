功能:

+ 设置键盘类型

定义:

+ [KeyboardOptions](/API/UI/Compose/Widget/TextField/KeyboardOptions/README.md) keyboardType(String action)

参数:

+ String action - 键盘类型,可选值如下
    + Text - 用于请求显示常规键盘的输入法的键盘类型。
    + Ascii - 用于请求能够输入ASCII字符的输入法的键盘类型
    + Number - 用于请求能够输入数字的输入法的键盘类型.但不保证IME可以提供数字以外的输入
    + Phone - 用于请求能够输入电话号码的输入法的键盘类型
    + Uri - 用于请求能够输入URI的IME的键盘类型。
    + Email - 用于请求能够输入电子邮件地址的输入法的键盘类型。
    + Password - 用于请求能够输入密码的输入法的键盘类型。
    + NumberPassword - 用于请求能够输入数字密码的输入法的键盘类型。
    + Decimal - 用于请求能够输入小数的输入法的键盘类型.IME应显式地提供十进制分隔符作为输入,这是Number无法保证的。

返回值:

+ [KeyboardOptions](/API/UI/Compose/Widget/TextField/KeyboardOptions/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [KeyboardOptions.keyboardType()](/API/UI/Compose/Widget/TextField/KeyboardOptions/README.md?id=keyboardType)
  方法设置键盘类型

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
            // Slot.mutableStateOf() 用于创建一个 MutableState 对象
            def state = mutableStateOf("")
            // Slot.TextField() 用于创建 TextField 可组合项
            TextField {
                // delegate -> TextField
                // TextField.value() 用于设置输入框内容
                value(state.value())
                // TextField.withSingleStates() 用于设置可组合项使用到的所有 SingleState
                withSingleStates(state)
                // TextField.onValueChange() 用于监听输入框中内容变化
                onValueChange { textFieldValue ->
                    // MutableState.value() 用于设置 MutableState 对象的值.
                    state.value(textFieldValue)
                }
                // TextField.keyboardOptions() 用于设置输入框键盘配置选项
                keyboardOptions {
                    // delegate -> KeyboardOptions
                    // KeyboardOptions.keyboardType() 用于设置键盘类型
                    keyboardType("Number")
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