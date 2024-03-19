功能:

+ 设置输入框内容.

定义:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) value(String value)

参数:

+ String value - 需要设置到输入框的内容

返回值:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [TextField.value()](/API/UI/Compose/Widget/TextField/README.md?id=value) 方法设置输入框内容.

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
                // TextField.withSingleStates() 用于设置可组合项使用到的所有 SingleState
                withSingleStates(state)
                // TextField.value() 用于设置输入框内容
                value(state.value())
                // TextField.onValueChange() 用于设置输入框内容变化事件
                onValueChange { value ->
                    // 更新状态值
                    state.value(value)
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