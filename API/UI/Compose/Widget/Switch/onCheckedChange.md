功能:

+ 设置 [Switch](/API/UI/Compose/Widget/Switch/README.md) 选中/取消选中监听器.

定义:

+ [Switch](/API/UI/Compose/Widget/Switch/README.md) onCheckedChange(Closure closure)

参数:

+ Closure closure - 设置监听器的闭包
    + 参数
        + boolean checked - true表示选中,false表示未选中
    + delegate - 无

返回值:

+ [Switch](/API/UI/Compose/Widget/Switch/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Switch.onCheckedChange()](/API/UI/Compose/Widget/Switch/README.md?id=onCheckedChange)
  方法设置 [Switch](/API/UI/Compose/Widget/Switch/README.md) 选中/取消选中监听器.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def state = mutableStateOf(false)
    // Slot.Switch() 用于创建 Switch 可组合项
    Switch {
        // delegate -> Switch
        // Switch.withSingleStates() 用于设置可组合项使用到的所有 SingleState
        withSingleStates(state)
        // Switch.checked() 用于设置 Switch 是否选中
        checked(state.value())
        // Switch.onCheckedChange() 用于设置 Switch 选中/取消选中监听器
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