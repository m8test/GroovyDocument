功能:

+ 设置是否开启手势功能

定义:

+ [ModalDrawer](/API/UI/Compose/Widget/ModalDrawer/README.md) gesturesEnabled(boolean enabled)

参数:

+ boolean enabled - true表示开启手势,false表示关闭手势

返回值:

+ [ModalDrawer](/API/UI/Compose/Widget/ModalDrawer/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [ModalDrawer.gesturesEnabled()](/API/UI/Compose/Widget/ModalDrawer/README.md?id=gesturesEnabled)
  方法设置是否开启手势功能

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