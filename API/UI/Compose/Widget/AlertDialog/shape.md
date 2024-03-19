功能:

+ 设置警告对话框形状.

定义:

+ [AlertDialog](/API/UI/Compose/Widget/AlertDialog/README.md) shape(Closure closure)

参数:

+ Closure closure - 设置形状的闭包
    + 参数 - 无
    + delegate - [Shape](/API/UI/Compose/Theme/Shape/Shape/README.md)

返回值:

+ [AlertDialog](/API/UI/Compose/Widget/AlertDialog/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity显示警告对话框, 并通过 [AlertDialog.shape()](/API/UI/Compose/Widget/AlertDialog/README.md?id=shape)
  方法设置警告对话框形状.

```groovy
def MyAlertDialog = { state ->
    // delegate -> Slot
    // Slot.AlertDialog() 用于设置警告对话框
    AlertDialog {
        // delegate -> AlertDialog
        // AlertDialog.withSingleStates() 用于设置可组合项使用到的所有 SingleState
        withSingleStates(state)
        // AlertDialog.show() 用于显示警告对话框
        show(state.value())
        // AlertDialog.shape() 用于设置警告对话框形状
        shape {
            // delegate -> Shape
            // Shape.all() 用于设置四个角尺寸
            all(20, "dp")
            // Shape.roundedCorner() 用于设置角的类型为圆角
            roundedCorner()
        }
        // AlertDialog.title() 用于设置警告对话框标题
        title {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("这是警告对话框标题")
            }
        }
        // AlertDialog.text() 用于设置警告对话框内容
        text {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("这是警告对话框内容")
            }
        }
        // AlertDialog.confirmButton() 用于设置警告对话框确定按钮
        confirmButton {
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
                        text("确定")
                    }
                }
                // TextButton.onClick() 用于处理点击事件
                onClick {
                    // 设置状态
                    state.value(false)
                }
            }
        }
    }
}
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def state = mutableStateOf(false)
    MyAlertDialog.delegate = delegate
    MyAlertDialog(state)
    // Slot.Button() 用于创建 Button 可组合项
    Button {
        // delegate -> Button
        // Button.content() 用于设置按钮内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("显示警告对话框")
            }
        }
        // Button.onClick() 用于处理点击事件
        onClick {
            state.value(true)
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