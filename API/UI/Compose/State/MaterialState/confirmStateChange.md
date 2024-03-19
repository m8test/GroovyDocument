功能:

+ 设置状态改变监听器,只有通过手势操作导致状态改变时才会触发.

定义:

+ [MaterialState](/API/UI/Compose/State/MaterialState/README.md) confirmStateChange(Closure closure)

参数:

+ Closure closure - 设置状态改变监听器的闭包
    + 参数
        + String value - 状态值
    + delegate - 无
    + 返回值 - boolean

返回值:

+ [MaterialState](/API/UI/Compose/State/MaterialState/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [MaterialState.confirmStateChange()](/API/UI/Compose/State/MaterialState/README.md?id=confirmStateChange)
  方法设置状态改变监听器

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newDrawerState() 用于创建 DrawerState
    def state = newDrawerState {
        // delegate -> DrawerState
        // DrawerState.confirmStateChange() 用于设置状态改变监听器
        confirmStateChange { value ->
            $console.log("当前状态:$value")
            true
        }
    }
    // Slot.ModalDrawer() 用于创建 ModalDrawer 可组合项
    ModalDrawer {
        // delegate -> ModalDrawer
        // ModalDrawer.drawerState() 用于设置 DrawerState
        drawerState(state)
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