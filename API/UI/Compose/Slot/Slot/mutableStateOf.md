功能:

+ 创建一个 [MutableState](/API/UI/Compose/State/MutableState/README.md) 对象

定义:

+ [MutableState](/API/UI/Compose/State/MutableState/README.md) mutableStateOf(Object initialValue)

参数:

+ Object initialValue - 初始值

返回值:

+ [MutableState](/API/UI/Compose/State/MutableState/README.md) -
  新创建的 [MutableState](/API/UI/Compose/State/MutableState/README.md)

示例代码:

+ 启动一个Activity, 并通过 [Slot.mutableStateOf()](/API/UI/Compose/Slot/Slot/README.md?id=mutableStateOf)
  方法创建一个 [MutableState](/API/UI/Compose/State/MutableState/README.md) 对象

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