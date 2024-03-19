功能:

+ 创建 [SnackBarHostState](/API/UI/Compose/State/SnackBarHostState/README.md)

定义:

+ [SnackBarHostState](/API/UI/Compose/State/SnackBarHostState/README.md) newSnackBarHostState(Closure
  closure)

参数:

+ Closure closure - 设置 [SnackBarHostState](/API/UI/Compose/State/SnackBarHostState/README.md) 的闭包
    + 参数 - 无
    + delegate - [SnackBarHostState](/API/UI/Compose/State/SnackBarHostState/README.md)

返回值:

+ [SnackBarHostState](/API/UI/Compose/State/SnackBarHostState/README.md) -
  新创建的 [SnackBarHostState](/API/UI/Compose/State/SnackBarHostState/README.md)

示例代码:

+ 启动一个Activity, 并通过 [Slot.newSnackBarHostState()](/API/UI/Compose/Slot/Slot/README.md?id=newSnackBarHostState)
  方法创建 [SnackBarHostState](/API/UI/Compose/State/SnackBarHostState/README.md)

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
            snackBarHostState.showSnackBar("测试SnackBar", null, "Short")
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