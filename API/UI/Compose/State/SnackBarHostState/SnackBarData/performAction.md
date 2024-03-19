功能:

+ 隐藏 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md)

定义:

+ [SnackBarData](/API/UI/Compose/State/SnackBarHostState/SnackBarData/README.md) performAction()

参数:

+ 无

返回值:

+ [SnackBarData](/API/UI/Compose/State/SnackBarHostState/SnackBarData/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [SnackBarData.performAction()](/API/UI/Compose/State/SnackBarHostState/SnackBarData/README.md?id=performAction)
  方法隐藏 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md)

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newSnackBarHostState() 用于创建 SnackBarHostState
    def snackBarHostState = newSnackBarHostState {
        // delegate -> SnackBarHostState
    }
    // Slot.Column() 用于创建 Column 可组合项
    Column {
        // delegate -> Column
        // Column.content() 用于设置 Column 可组合项中的内容
        content {
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
                    // SnackBarHostState.showSnackBar() 用于显示 SnackBar
                    snackBarHostState.showSnackBar("测试SnackBar", null, "Indefinite")
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
                        // SnackBar.action() 用于设置 SnackBar 动作按钮
                        action {
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
                                        text("取消")
                                    }
                                }
                                // TextButton.onClick() 用于处理点击事件
                                onClick {
                                    // SnackBarHostState.currentSnackBarData() 用于获取当前 SnackBarData
                                    def snackBarData = snackBarHostState.currentSnackBarData()
                                    // SnackBarData.performAction() 用于隐藏 SnackBar
                                    snackBarData.performAction()
                                }
                            }
                        }
                        // SnackBar.content() 用于设置 SnackBar 内容
                        content {
                            // delegate -> Slot
                            // Slot.Text() 用于创建文本可组合项
                            Text {
                                // delegate -> Text
                                // SnackBarData.message() 用于获取 SnackBar 消息
                                def message = data.message()
                                // Text.text() 用于设置文本可组合项内容
                                text(message)
                            }
                        }
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