功能:

+ 创建 [DismissState](/API/UI/Compose/State/DismissState/README.md)

定义:

+ [DismissState](/API/UI/Compose/State/DismissState/README.md) newDismissState(Closure closure)

参数:

+ Closure closure - 设置 [DismissState](/API/UI/Compose/State/DismissState/README.md) 的闭包
    + 参数 - 无
    + delegate - [DismissState](/API/UI/Compose/State/DismissState/README.md)

返回值:

+ [DismissState](/API/UI/Compose/State/DismissState/README.md) -
  新创建的 [DismissState](/API/UI/Compose/State/DismissState/README.md)

示例代码:

+ 启动一个Activity, 并通过 [Slot.newDismissState()](/API/UI/Compose/Slot/Slot/README.md?id=newDismissState)
  方法创建 [DismissState](/API/UI/Compose/State/DismissState/README.md)

```groovy
def MySwipeToDismiss = { dismissState ->
    // delegate -> Slot
    // Slot.SwipeToDismiss() 用于创建 SwipeToDismiss 可组合项
    SwipeToDismiss {
        // delegate -> SwipeToDismiss
        // SwipeToDismiss.state() 用于设置 DismissState
        state(dismissState)
        // SwipeToDismiss.background() 用于设置 SwipeToDismiss 背景
        background {
            // delegate -> Slot
            // Slot.Box() 用于创建 Box 可组合项
            Box {
                // delegate -> Box
                // Box.modifier() 用于修饰 Composable
                modifier {
                    // delegate -> Modifier
                    // Modifier.fillMaxSize() 用于设置填充最大宽度
                    fillMaxSize(1.0f)
                    // Modifier.background() 用于设置背景颜色
                    background({
                        // delegate -> Color
                        // Color.red() 用于配置红色通道
                        red(255)
                    }) {
                        // delegate -> Shape
                        // 不配置Shape默认为矩形
                    }
                }
            }
        }
        // SwipeToDismiss.dismissContent() 用于设置 SwipeToDismiss 可取消内容
        dismissContent {
            // delegate -> Slot
            // Slot.Row() 用于创建 Row 可组合项
            Row {
                // delegate -> Row
                // Row.content() 用于设置行内容
                content {
                    // delegate -> Slot
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        // Text.text() 用于设置文本可组合项内容
                        text("SwipeToDismiss")
                    }
                }
                // Row.modifier() 用于修饰 Composable
                modifier {
                    // delegate -> Modifier
                    // Modifier.fillMaxWidth() 用于设置填充最大宽度
                    fillMaxWidth(1.0f)
                }
            }
        }
    }
}
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newDismissState() 用于创建 DismissState
    def dismissState = newDismissState {
        // delegate -> DismissState
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
                        text("Dismiss")
                    }
                }
                // TextButton.onClick() 用于处理点击事件
                onClick {
                    // DismissState.dismiss() 用于取消 SwipeToDismiss
                    dismissState.dismiss("StartToEnd")
                }
            }
            MySwipeToDismiss.delegate = delegate
            MySwipeToDismiss(dismissState)
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