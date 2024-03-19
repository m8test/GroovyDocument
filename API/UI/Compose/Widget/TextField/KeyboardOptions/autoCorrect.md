功能:

+ 设置键盘是否启用自动校正

定义:

+ [KeyboardOptions](/API/UI/Compose/Widget/TextField/KeyboardOptions/README.md) autoCorrect(boolean value)

参数:

+ boolean value - true表示启用自动校正,false表示不启用自动校正

返回值:

+ [KeyboardOptions](/API/UI/Compose/Widget/TextField/KeyboardOptions/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [KeyboardOptions.autoCorrect()](/API/UI/Compose/Widget/TextField/KeyboardOptions/README.md?id=autoCorrect)
  方法设置键盘是否启用自动校正

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
                    // KeyboardOptions.autoCorrect() 用于设置键盘是否启用自动校正
                    autoCorrect(true)
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