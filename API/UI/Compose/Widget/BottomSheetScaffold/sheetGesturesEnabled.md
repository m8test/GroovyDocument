功能:

+ 设置是否开启底页手势

定义:

+ [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) sheetGesturesEnabled(boolean
  value)

参数:

+ boolean value - true表示开启底页手势,false表示关闭底页手势

返回值:

+ [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BottomSheetScaffold.sheetGesturesEnabled()](/API/UI/Compose/Widget/BottomSheetScaffold/README.md?id=sheetGesturesEnabled)
  方法设置是否开启底页手势

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newBottomSheetScaffoldState() 用于新建 BottomSheetScaffoldState
    def state = newBottomSheetScaffoldState {
        // delegate -> BottomSheetScaffoldState
    }
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