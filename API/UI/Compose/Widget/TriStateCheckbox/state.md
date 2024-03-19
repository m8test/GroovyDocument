功能:

+ 设置 [TriStateCheckbox](/API/UI/Compose/Widget/TriStateCheckbox/README.md) 状态.

定义:

+ [TriStateCheckbox](/API/UI/Compose/Widget/TriStateCheckbox/README.md) state(String state)

参数:

+ String state - 需要设置的状态,可选值有
    + Indeterminate - 表示无法确定组件的开/关值的状态
    + Off - 表示组件关闭的状态
    + On - 表示组件开启的状态

返回值:

+ [TriStateCheckbox](/API/UI/Compose/Widget/TriStateCheckbox/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [TriStateCheckbox.state()](/API/UI/Compose/Widget/TriStateCheckbox/README.md?id=state)
  方法设置 [TriStateCheckbox](/API/UI/Compose/Widget/TriStateCheckbox/README.md) 状态.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def checkBoxState = mutableStateOf("Off")
    // Slot.TriStateCheckbox() 用于创建 TriStateCheckbox 可组合项
    TriStateCheckbox {
        // delegate -> TriStateCheckbox
        // TriStateCheckbox.withSingleStates() 用于设置可组合项使用到的所有 SingleState
        withSingleStates(checkBoxState)
        // TriStateCheckbox.state() 用于设置 TriStateCheckbox 状态
        state(checkBoxState.value())
        // TriStateCheckbox.onClick() 用于设置 TriStateCheckbox 点击事件
        onClick {
            def currentValue = checkBoxState.value()
            if (currentValue == "Off") {
                checkBoxState.value("Indeterminate")
            } else if (currentValue == "Indeterminate") {
                checkBoxState.value("On")
            } else {
                checkBoxState.value("Off")
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