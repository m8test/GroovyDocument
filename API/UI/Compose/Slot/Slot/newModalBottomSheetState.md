功能:

+ 创建 [ModalBottomSheetState](/API/UI/Compose/State/ModalBottomSheetState/README.md)

定义:

+ [ModalBottomSheetState](/API/UI/Compose/State/ModalBottomSheetState/README.md) newModalBottomSheetState(
  Closure closure)

参数:

+ Closure closure - 设置 [ModalBottomSheetState](/API/UI/Compose/State/ModalBottomSheetState/README.md) 的闭包
    + 参数 - 无
    + delegate - [ModalBottomSheetState](/API/UI/Compose/State/ModalBottomSheetState/README.md)

返回值:

+ [ModalBottomSheetState](/API/UI/Compose/State/ModalBottomSheetState/README.md) -
  新创建的 [ModalBottomSheetState](/API/UI/Compose/State/ModalBottomSheetState/README.md)

示例代码:

+ 启动一个Activity,
  并通过 [Slot.newModalBottomSheetState()](/API/UI/Compose/Slot/Slot/README.md?id=newModalBottomSheetState)
  方法创建 [ModalBottomSheetState](/API/UI/Compose/State/ModalBottomSheetState/README.md)

```groovy
def MyTextButton = { btnText, onBtnClick ->
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
                text(btnText)
            }
        }
        // TextButton.onClick() 用于处理点击事件
        onClick {
            onBtnClick()
        }
    }
}

// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newModalBottomSheetState() 用于创建 ModalBottomSheetState
    def state = newModalBottomSheetState {
        // delegate -> ModalBottomSheetState
    }
    // Slot.ModalBottomSheetLayout() 用于创建 ModalBottomSheetLayout 可组合项
    ModalBottomSheetLayout {
        // delegate -> ModalBottomSheetLayout
        // ModalBottomSheetLayout.sheetState() 用于设置 ModalBottomSheetState
        sheetState(state)
        // ModalBottomSheetLayout.sheetContent() 用于设置 ModalBottomSheetLayout 底页内容
        sheetContent {
            // delegate -> Slot
            MyTextButton.delegate = delegate
            MyTextButton("关闭") {
                // ModalBottomSheetState.hide() 用于隐藏 ModalBottomSheetLayout 底页
                state.hide()
            }
        }
        // ModalBottomSheetLayout.content() 用于设置 ModalBottomSheetLayout 内容
        content {
            // delegate -> Slot
            MyTextButton.delegate = delegate
            MyTextButton("显示") {
                // ModalBottomSheetState.show() 用于显示 ModalBottomSheetLayout 底页
                state.show()
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