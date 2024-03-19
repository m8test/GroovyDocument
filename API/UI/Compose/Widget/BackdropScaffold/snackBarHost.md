功能:

+ 设置 [SnackBarHost](/API/UI/Compose/Widget/SnackBarHost/README.md) 可组合项

定义:

+ [BackdropScaffold](/API/UI/Compose/Widget/BackdropScaffold/README.md) snackBarHost(Closure closure)

参数:

+ Closure closure - 设置 [SnackBarHost](/API/UI/Compose/Widget/SnackBarHost/README.md) 的闭包
    + 参数 - [SnackBarHostState](/API/UI/Compose/State/SnackBarHostState/README.md)
    + delegate -
      [Slot](/API/UI/Compose/Slot/Slot/README.md)([Modifier](/API/UI/Compose/Modifier/Modifier/README.md))

返回值:

+ [BackdropScaffold](/API/UI/Compose/Widget/BackdropScaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BackdropScaffold.snackBarHost()](/API/UI/Compose/Widget/BackdropScaffold/README.md?id=snackBarHost)
  方法设置 [SnackBarHost](/API/UI/Compose/Widget/SnackBarHost/README.md) 可组合项

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newBackdropScaffoldState() 用于创建 BackdropScaffoldState
    def backdropScaffoldState = newBackdropScaffoldState {
        // delegate -> BackdropScaffoldState
    }
    // Slot.BackdropScaffold() 用于创建 BackdropScaffold 可组合项
    BackdropScaffold {
        // delegate -> BackdropScaffold
        // BackdropScaffold.scaffoldState() 用于设置 BackdropScaffoldState
        scaffoldState(backdropScaffoldState)
        frontLayerContent {
            // delegate -> Slot
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
                    // 设置状态
                    // BackdropScaffoldState.snackBarHostState() 用于获取 SnackBarHostState
                    def snackBarHostState = backdropScaffoldState.snackBarHostState()
                    // SnackBarHostState.showSnackBar() 用于显示 SnackBar
                    snackBarHostState.showSnackBar("测试SnackBar", null, "Short")
                }
            }
        }
        // BackdropScaffoldState.snackBarHost() 用于设置 SnackBarHost 可组合项
        snackBarHost { snackBarHostState ->
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