功能:

+ 设置是否跳过半展开状态.如果工作表足够高,是否应跳过半展开状态。如果为true,则在以编程方式或通过用户交互隐藏工作表时,工作表将始终展开到“展开”状态并移动到“隐藏”状态。如果
  [initialValue](/API/UI/Compose/State/MaterialState/README.md?id=initialValue) 为 HalfExpanded,
  则不能设置为true。如果为 [initialValue](/API/UI/Compose/State/MaterialState/README.md?id=initialValue) 提供了
  HalfExpended，则将引发 IllegalArgumentException。

定义:

+ [ModalBottomSheetState](/API/UI/Compose/State/ModalBottomSheetState/README.md) isSkipHalfExpanded(boolean
  value)

参数:

+ boolean value - true表示跳过半展开状态,false表示不跳过半展开状态

返回值:

+ [ModalBottomSheetState](/API/UI/Compose/State/ModalBottomSheetState/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [ModalBottomSheetState.isSkipHalfExpanded()](/API/UI/Compose/State/ModalBottomSheetState/README.md?id=isSkipHalfExpanded)
  方法设置是否跳过半展开状态

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
        // ModalBottomSheetState.isSkipHalfExpanded() 用于设置是否跳过半展开状态
        isSkipHalfExpanded(false)
    }
    // Slot.ModalBottomSheetLayout() 用于创建 ModalBottomSheetLayout 可组合项
    ModalBottomSheetLayout {
        // delegate -> ModalBottomSheetLayout
        // ModalBottomSheetLayout.sheetState() 用于设置 ModalBottomSheetState
        sheetState(state)
        // ModalBottomSheetLayout.sheetContent() 用于设置 ModalBottomSheetLayout 底页内容
        sheetContent {
            // delegate -> Slot
            // Slot.Column() 用于创建 Column 可组合项
            Column {
                // delegate -> Column
                // Column.modifier() 用于修饰 Composable
                modifier {
                    // delegate -> Modifier
                    // Modifier.height() 用于设置高度
                    height(550)
                }
                // Column.content() 用于设置 Column 可组合项中的内容
                content {
                    // delegate -> Slot
                    MyTextButton.delegate = delegate
                    MyTextButton("关闭") {
                        // ModalBottomSheetState.hide() 用于隐藏 ModalBottomSheetLayout 底页
                        state.hide()
                    }
                }
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