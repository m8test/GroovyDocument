功能:

+ 设置图标切换按钮选择改变事件

定义:

+ [IconToggleButton](/API/UI/Compose/Widget/IconToggleButton/README.md) onCheckedChange(Closure closure)

参数:

+ Closure closure - 设置监听事件的闭包
    + 参数
        + boolean checked - 当前图标切换按钮是否选中
    + delegate - 无

返回值:

+ [IconToggleButton](/API/UI/Compose/Widget/IconToggleButton/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [IconToggleButton.onCheckedChange()](/API/UI/Compose/Widget/IconToggleButton/README.md?id=onCheckedChange)
  方法设置图标切换按钮选择改变事件

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def state = mutableStateOf(false)
    // Slot.IconToggleButton() 用于创建 IconToggleButton 可组合项
    IconToggleButton {
        // delegate -> IconToggleButton
        // IconToggleButton.withSingleStates() 用于设置可组合项使用到的所有 SingleState
        withSingleStates(state)
        // IconToggleButton.checked() 用于设置图标切换按钮是否选中
        checked(state.value())
        // IconToggleButton.onCheckedChange() 用于设置图标切换按钮选择改变事件
        onCheckedChange {
            // 改变状态
            state.value(it)
        }
        // IconToggleButton.content() 用于设置图标切换按钮内容
        content {
            // delegate -> Slot
            // Slot.Icon() 用于创建 Icon 可组合项
            Icon {
                // delegate -> Icon
                // Icon.withSingleStates() 用于设置可组合项使用到的所有 SingleState
                withSingleStates(state)
                // Icon.contentDescription() 用于设置图标内容描述
                contentDescription("喜欢")
                // Icon.tint() 用于设置图标颜色
                tint {
                    // delegate -> Color
                    if (state.value()) {
                        // Color.red() 用于配置红色通道
                        red(255)
                        // Color.blue() 用于配置蓝色通道
                        blue(0)
                        // Color.green() 用于配置绿色通道
                        green(0)
                    } else {
                        // Color.red() 用于配置红色通道
                        red(0)
                        // Color.blue() 用于配置蓝色通道
                        blue(255)
                        // Color.green() 用于配置绿色通道
                        green(0)
                    }
                }
                vector("Filled", "Favorite")
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