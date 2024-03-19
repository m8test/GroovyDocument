功能:

+ 获取滑动方向,如果您想要在每一侧执行不同的操作，请使用它来更改 [SwipeToDismiss](/API/UI/Compose/Widget/SwipeToDismiss/README.md) 的背景。

定义:

+ String dismissDirection()

参数:

+ 无

返回值:

+ String - 已关闭或正在关闭可组合项的方向(如果有)。如果可组合项设置为默认状态,则这将为 null。

示例代码:

+ 启动一个Activity,
  并通过 [DismissState.dismissDirection()](/API/UI/Compose/State/DismissState/README.md?id=dismissDirection)
  方法获取滑动方向

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
                // Box.withAggregatedStates() 用于设置可组合项重组需要的聚合状态
                withAggregatedStates((dismissState): ["dismissDirection"])
                // Box.modifier() 用于修饰 Composable
                modifier {
                    // delegate -> Modifier
                    // Modifier.fillMaxSize() 用于设置填充最大宽度
                    fillMaxSize(1.0f)
                    // Modifier.background() 用于设置背景颜色
                    background({
                        // delegate -> Color
                        // DismissState.dismissDirection() 用于获取滑动方向
                        def direction = dismissState.dismissDirection()
                        if (direction == "StartToEnd") {
                            // Color.parse() 用于从字符串或者整数中解析颜色
                            parse("#ffff0000")
                        } else if (direction == "EndToStart") {
                            // Color.parse() 用于从字符串或者整数中解析颜色
                            parse("#ff00ff00")
                        } else {
                            // Color.parse() 用于从字符串或者整数中解析颜色
                            parse("#ff0000ff")
                        }
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
    MySwipeToDismiss.delegate = delegate
    MySwipeToDismiss(dismissState)
}
// Activity.onDestroy() 方法用于监听Activity销毁
$composeActivity.onDestroy {
    // Script.stop() 方法用于停止脚本
    $script.stop()
}
// Activity.start() 用于启动Android系统的Activity
$composeActivity.start()
```