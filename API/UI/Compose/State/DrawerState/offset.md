功能:

+ 获取抽屉偏移量

定义:

+ float offset()

参数:

+ 无

返回值:

+ float - 当前抽屉偏移量

示例代码:

+ 启动一个Activity, 并通过 [DrawerState.offset()](/API/UI/Compose/State/DrawerState/README.md?id=offset) 方法获取抽屉偏移量

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newDrawerState() 用于创建 DrawerState
    def state = newDrawerState {
        // delegate -> DrawerState
    }
    // Slot.ModalDrawer() 用于创建 ModalDrawer 可组合项
    ModalDrawer {
        // delegate -> ModalDrawer
        // ModalDrawer.drawerState() 用于设置 DrawerState
        drawerState(state)
        // ModalDrawer.gesturesEnabled() 用于设置是否开启手势功能
        gesturesEnabled(false)
        // ModalDrawer.withAggregatedStates() 用于设置可组合项重组需要的聚合状态
        withAggregatedStates((state): ["offset"])
        // ModalDrawer.scrimColor() 用于设置 ModalDrawer 抽屉打开时非抽屉部分的颜色
        scrimColor {
            // delegate -> Color
            // DrawerState.offset() 用于获取抽屉偏移量
            def offsetValue = state.offset()
            if (offsetValue >= -200) {
                // Color.parse() 用于从字符串或者整数中解析颜色
                parse("#ffff0000")
            } else {
                // Color.parse() 用于从字符串或者整数中解析颜色
                parse("#ff0000ff")
            }
        }
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