功能1:

+ 设置 [BottomSheetState](/API/UI/Compose/State/BottomSheetState/README.md)

定义1:

+ [BottomSheetScaffoldState](/API/UI/Compose/State/BottomSheetScaffoldState/README.md)
  bottomSheetState([BottomSheetState](/API/UI/Compose/State/BottomSheetState/README.md) bottomSheetState)

参数1:

+ [BottomSheetState](/API/UI/Compose/State/BottomSheetState/README.md) bottomSheetState -
  需要设置的 [BottomSheetState](/API/UI/Compose/State/BottomSheetState/README.md)

返回值1:

+ [BottomSheetScaffoldState](/API/UI/Compose/State/BottomSheetScaffoldState/README.md) - 返回对象本身方便链式调用

功能2:

+ 获取 [BottomSheetState](/API/UI/Compose/State/BottomSheetState/README.md)

定义2:

+ [BottomSheetState](/API/UI/Compose/State/BottomSheetState/README.md) bottomSheetState()

参数2:

+ 无

返回值2:

+ [BottomSheetState](/API/UI/Compose/State/BottomSheetState/README.md) -
  [BottomSheetState](/API/UI/Compose/State/BottomSheetState/README.md) 对象

示例代码:

+ 启动一个Activity,
  并通过 [BottomSheetScaffoldState.bottomSheetState()](/API/UI/Compose/State/BottomSheetScaffoldState/README.md?id=bottomSheetState)
  方法设置/获取 [BottomSheetState](/API/UI/Compose/State/BottomSheetState/README.md)

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newBottomSheetScaffoldState() 用于新建 BottomSheetScaffoldState
    def state = newBottomSheetScaffoldState {
        // delegate -> BottomSheetScaffoldState
    }
    // Slot.newBottomSheetState() 用于创建 BottomSheetState
    def bState = newBottomSheetState {
        // delegate -> BottomSheetState
    }
    // BottomSheetScaffoldState.bottomSheetState() 用于设置 BottomSheetState
    state.bottomSheetState(bState)
    // Slot.BottomSheetScaffold() 用于创建 BottomSheetScaffold 可组合项
    BottomSheetScaffold {
        // delegate -> BottomSheetScaffold
        // BottomSheetScaffold.sheetGesturesEnabled() 用于设置是否开启底页手势
        sheetGesturesEnabled(false)
        // BottomSheetScaffold.scaffoldState() 用于设置 BottomSheetScaffoldState
        scaffoldState(state)
        // BottomSheetScaffold.sheetPeekHeight() 用于设置底页高度
        sheetPeekHeight(20)
        // BottomSheetScaffold.sheetContent() 用于设置 BottomSheetScaffold 底页内容
        sheetContent {
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
                        text("关闭底页")
                    }
                }
                // TextButton.onClick() 用于处理点击事件
                onClick {
                    // BottomSheetScaffoldState.bottomSheetState() 用于获取 BottomSheetState
                    def bottomSheetState = state.bottomSheetState()
                    // BottomSheetState.collapse() 用于关闭底页
                    bottomSheetState.collapse()
                }
            }
        }
        // BottomSheetScaffold.content() 用于设置 BottomSheetScaffold 内容
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
                        text("打开底页")
                    }
                }
                // TextButton.onClick() 用于处理点击事件
                onClick {
                    // BottomSheetScaffoldState.bottomSheetState() 用于获取 BottomSheetState
                    def bottomSheetState = state.bottomSheetState()
                    // BottomSheetState.expand() 用于打开底页
                    bottomSheetState.expand()
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