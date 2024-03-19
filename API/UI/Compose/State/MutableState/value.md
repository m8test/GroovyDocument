功能1:

+ 设置 [MutableState](/API/UI/Compose/State/MutableState/README.md) 对象的值.

定义1:

+ [MutableState](/API/UI/Compose/State/MutableState/README.md) value(Object value)

参数1:

+ Object value - 需要设置的值

返回值1:

+ [MutableState](/API/UI/Compose/State/MutableState/README.md) - 返回对象本身方便链式调用

功能2:

+ 获取 [MutableState](/API/UI/Compose/State/MutableState/README.md) 对象的值.

定义2:

+ Object value()

参数2:

+ 无

返回值2:

+ Object - [MutableState](/API/UI/Compose/State/MutableState/README.md) 对象保存的值

示例代码:

+ 启动一个Activity, 并通过 [MutableState.value()](/API/UI/Compose/State/MutableState/README.md?id=value)
  方法设置/获取 [MutableState](/API/UI/Compose/State/MutableState/README.md) 对象的值.

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
                // MutableState.value() 用于获取 MutableState 对象的值
                def currentValue = state.value()
                // TextField.value() 用于设置输入框内容
                value(currentValue)
                // TextField.onValueChange() 用于设置输入框内容变化事件
                onValueChange { value ->
                    // MutableState.value() 用于设置 MutableState 对象的值.
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