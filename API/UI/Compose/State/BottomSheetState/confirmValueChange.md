功能:

+ 设置状态改变监听器,只有通过手势操作导致状态改变时才会触发.

定义:

+ [BottomSheetState](/API/UI/Compose/State/BottomSheetState/README.md) confirmValueChange(Closure
  closure)

参数:

+ Closure closure - 设置状态改变监听器的闭包
    + 参数
        + String value - 状态值
    + delegate - 无
    + 返回值 - boolean

返回值:

+ [BottomSheetState](/API/UI/Compose/State/BottomSheetState/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BottomSheetState.confirmValueChange()](/API/UI/Compose/State/BottomSheetState/README.md?id=confirmValueChange)
  方法设置状态改变监听器

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
        // BottomSheetState.confirmValueChange() 用于设置状态改变监听器
        confirmValueChange { value ->
            $console.log("当前状态:$value")
            true
        }
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