功能:

+ 新建 [ScaffoldState](/API/UI/Compose/State/ScaffoldState/README.md)

定义:

+ [ScaffoldState](/API/UI/Compose/State/ScaffoldState/README.md) newScaffoldState(Closure closure)

参数:

+ Closure closure - 设置 [ScaffoldState](/API/UI/Compose/State/ScaffoldState/README.md) 的闭包
    + 参数 - 无
    + delegate - [ScaffoldState](/API/UI/Compose/State/ScaffoldState/README.md)

返回值:

+ [ScaffoldState](/API/UI/Compose/State/ScaffoldState/README.md) -
  新创建的 [ScaffoldState](/API/UI/Compose/State/ScaffoldState/README.md)

示例代码:

+ 启动一个Activity, 并通过 [Slot.newScaffoldState()](/API/UI/Compose/Slot/Slot/README.md?id=newScaffoldState)
  方法新建 [ScaffoldState](/API/UI/Compose/State/ScaffoldState/README.md)

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newScaffoldState() 用于新建 ScaffoldState
    def state = newScaffoldState {
        // delegate -> ScaffoldState
    }
    // Slot.Scaffold() 用于创建 Scaffold 可组合项
    Scaffold {
        // delegate -> Scaffold
        // Scaffold.drawerGesturesEnabled() 用于设置是否开启抽屉手势
        drawerGesturesEnabled(false)
        // Scaffold.scaffoldState() 用于设置 ScaffoldState
        scaffoldState(state)
        // Scaffold.drawerContent() 用于设置抽屉内容
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
                    // ScaffoldState.drawerState() 用于获取 DrawerState
                    def drawerState = state.drawerState()
                    // DrawerState.close() 用于关闭抽屉
                    drawerState.close()
                }
            }
        }
        // Scaffold.content() 用于设置 Scaffold 内容
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
                    // ScaffoldState.drawerState() 用于获取 DrawerState
                    def drawerState = state.drawerState()
                    // DrawerState.open() 用于打开抽屉
                    drawerState.open()
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