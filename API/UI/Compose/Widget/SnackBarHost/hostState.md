功能:

+ 设置 [SnackBarHostState](/API/UI/Compose/State/SnackBarHostState/README.md)

定义:

+ [SnackBarHost](/API/UI/Compose/Widget/SnackBarHost/README.md)
  hostState([SnackBarHostState](/API/UI/Compose/State/SnackBarHostState/README.md) snackBarHostState)

参数:

+ [SnackBarHostState](/API/UI/Compose/State/SnackBarHostState/README.md) snackBarHostState -
  需要设置的 [SnackBarHostState](/API/UI/Compose/State/SnackBarHostState/README.md) 对象

返回值:

+ [SnackBarHost](/API/UI/Compose/Widget/SnackBarHost/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [SnackBarHost.hostState()](/API/UI/Compose/Widget/SnackBarHost/README.md?id=hostState)
  方法设置 [SnackBarHostState](/API/UI/Compose/State/SnackBarHostState/README.md)

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