功能:

+ 设置 [Checkbox](/API/UI/Compose/Widget/Checkbox/README.md) 是否选中.

定义:

+ [Checkbox](/API/UI/Compose/Widget/Checkbox/README.md) checked(boolean value)

参数:

+ boolean value - true表示选中,false表示未选中

返回值:

+ [Checkbox](/API/UI/Compose/Widget/Checkbox/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Checkbox.checked()](/API/UI/Compose/Widget/Checkbox/README.md?id=checked)
  方法设置 [Checkbox](/API/UI/Compose/Widget/Checkbox/README.md) 是否选中.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def state = mutableStateOf(false)
    // Slot.Checkbox() 用于创建 Checkbox 可组合项
    Checkbox {
        // delegate -> Checkbox
        // Checkbox.withSingleStates() 用于设置可组合项使用到的所有 SingleState
        withSingleStates(state)
        // Checkbox.checked() 用于设置 Checkbox 是否选中
        checked(state.value())
        // Checkbox.onCheckedChange() 用于设置 Checkbox 选中/取消选中监听器
        onCheckedChange { isChecked ->
            // 更新状态
            state.value(isChecked)
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