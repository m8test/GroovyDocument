功能:

+ 设置 [TriStateCheckbox](/API/UI/Compose/Widget/TriStateCheckbox/README.md) 未启用并且不确定时颜色.

定义:

+ [CheckboxColors](/API/UI/Compose/Theme/Color/CheckboxColors/README.md) disabledIndeterminateColor(Closure
  closure)

参数:

+ Closure closure - 设置颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [CheckboxColors](/API/UI/Compose/Theme/Color/CheckboxColors/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [CheckboxColors.disabledIndeterminateColor()](/API/UI/Compose/Theme/Color/CheckboxColors/README.md?id=disabledIndeterminateColor)
  方法设置 [TriStateCheckbox](/API/UI/Compose/Widget/TriStateCheckbox/README.md)
  未启用并且不确定时颜色.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def checkBoxState = mutableStateOf("Indeterminate")
    // Slot.TriStateCheckbox() 用于创建 TriStateCheckbox 可组合项
    TriStateCheckbox {
        // delegate -> TriStateCheckbox
        // TriStateCheckbox.withSingleStates() 用于设置可组合项使用到的所有 SingleState
        withSingleStates(checkBoxState)
        // TriStateCheckbox.enabled() 用于设置 TriStateCheckbox 是否启用
        enabled(false)
        // TriStateCheckbox.colors() 用于设置 TriStateCheckbox 颜色
        colors {
            // delegate -> CheckboxColors
            // CheckboxColors.disabledIndeterminateColor() 用于设置 TriStateCheckbox 未启用并且不确定时颜色
            disabledIndeterminateColor {
                // delegate -> Color
                // Color.red() 用于配置红色通道
                red(255)
            }
        }
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