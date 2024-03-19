功能:

+ 设置 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md) 内容颜色,
  可配合 [snackBarData()](/API/UI/Compose/Widget/SnackBar/README.md?id=snackBarData) 使用

定义:

+ [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md) contentColor(Closure closure)

参数:

+ Closure closure - 设置颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [SnackBar.contentColor()](/API/UI/Compose/Widget/SnackBar/README.md?id=contentColor)
  方法设置 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md) 内容颜色

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newSnackBarHostState() 用于创建 SnackBarHostState
    def snackBarHostState = newSnackBarHostState {
        // delegate -> SnackBarHostState
    }
    // Slot.TextButton() 用于设置文本按钮
    TextButton {
        // delegate -> TextButton
        // TextButton.content() 用于设置按钮内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("显示SnackBar")
            }
        }
        // TextButton.onClick() 用于处理点击事件
        onClick {
            // SnackBarHostState.showSnackBar() 用于显示 SnackBar
            snackBarHostState.showSnackBar("红色内容SnackBar", "取消", "Short")
        }
    }
    // delegate -> Slot
    // Slot.SnackBarHost() 用于创建 SnackBarHost 可组合项
    SnackBarHost {
        // delegate -> SnackBarHost
        // SnackBarHost.hostState() 用于设置 SnackBarHostState
        hostState(snackBarHostState)
        // SnackBarHost.snackBar() 用于设置 SnackBar 可组合项
        snackBar { data ->
            // delegate -> Slot
            // Slot.SnackBar() 用于创建 SnackBar 可组合项
            SnackBar {
                // delegate -> SnackBar
                // SnackBar.snackBarData() 用于设置 SnackBarData
                snackBarData(data)
                // SnackBar.contentColor() 用于设置 SnackBar 内容颜色
                contentColor {
                    // delegate -> Color
                    // Color.red() 用于配置红色通道
                    red(255)
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