功能:

+ 设置初始状态

定义:

+ [MaterialState](/API/UI/Compose/State/MaterialState/README.md) initialValue(String value)

参数:

+ String value - 初始状态,不同的状态对象具有不同的值,下面列举所有状态的所有可用值
    + [BackdropScaffoldState](/API/UI/Compose/State/BackdropScaffoldState/README.md) - Concealed , Revealed
    + [BottomDrawerState](/API/UI/Compose/State/BottomDrawerState/README.md) - Closed , Expanded , Open
    + [BottomSheetState](/API/UI/Compose/State/BottomSheetState/README.md) - Expanded , Collapsed
    + [DismissState](/API/UI/Compose/State/DismissState/README.md) - DismissedToStart , DismissedToEnd ,
      Default
    + [DrawerState](/API/UI/Compose/State/DrawerState/README.md) - Open , Closed
    + [ModalBottomSheetState](/API/UI/Compose/State/ModalBottomSheetState/README.md) - HalfExpanded ,
      Expanded , Hidden

返回值:

+ [MaterialState](/API/UI/Compose/State/MaterialState/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [MaterialState.initialValue()](/API/UI/Compose/State/MaterialState/README.md?id=initialValue) 方法设置初始状态

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newDrawerState() 用于创建 DrawerState
    def state = newDrawerState {
        // delegate -> DrawerState
        // DrawerState.initialValue() 用于设置初始状态
        initialValue("Open")
    }
    // Slot.ModalDrawer() 用于创建 ModalDrawer 可组合项
    ModalDrawer {
        // delegate -> ModalDrawer
        // ModalDrawer.drawerState() 用于设置 DrawerState
        drawerState(state)
        // ModalDrawer.gesturesEnabled() 用于设置是否开启手势功能
        gesturesEnabled(false)
        // ModalDrawer.drawerContent() 用于设置 ModalDrawer 抽屉内容
        drawerContent {
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
                        text("关闭抽屉")
                    }
                }
                // TextButton.onClick() 用于处理点击事件
                onClick {
                    // DrawerState.close() 用于关闭抽屉
                    state.close()
                }
            }
        }
        // ModalDrawer.content() 用于设置 ModalDrawer 内容
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
                        text("打开抽屉")
                    }
                }
                // TextButton.onClick() 用于处理点击事件
                onClick {
                    // DrawerState.open() 用于打开抽屉
                    state.open()
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