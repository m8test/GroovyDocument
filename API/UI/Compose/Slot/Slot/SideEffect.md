功能:

+ 创建 [SideEffect](/API/UI/Compose/Effects/SideEffect/README.md)

定义:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) SideEffect(Closure closure)

参数:

+ Closure closure - 设置 [SideEffect](/API/UI/Compose/Effects/SideEffect/README.md) 的闭包
    + 参数 - 无
    + delegate - [SideEffect](/API/UI/Compose/Effects/SideEffect/README.md)

返回值:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Slot.SideEffect()](/API/UI/Compose/Slot/Slot/README.md?id=SideEffect)
  方法创建 [SideEffect](/API/UI/Compose/Effects/SideEffect/README.md)

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newBottomDrawerState() 用于创建 BottomDrawerState
    def state = newBottomDrawerState {
        // delegate -> BottomDrawerState
    }
    // Slot.BottomDrawer() 用于创建 BottomDrawer 可组合项
    BottomDrawer {
        // delegate -> BottomDrawer
        // BottomDrawer.drawerState() 用于设置 BottomDrawerState
        drawerState(state)
        // BottomDrawer.gesturesEnabled() 用于设置是否开启手势功能
        gesturesEnabled(false)
        // BottomDrawer.drawerContent() 用于设置 BottomDrawer 抽屉内容
        drawerContent {
            // delegate -> Slot
            // Slot.SideEffect() 用于创建 SideEffect
            SideEffect {
                // delegate -> SideEffect
                // SideEffect.effect() 用于设置效应
                effect {
                    $console.log("重组")
                }
            }
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
                    // BottomDrawerState.close() 用于关闭抽屉
                    state.close()
                }
            }
        }
        // BottomDrawer.content() 用于设置 BottomDrawer 内容
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
                    // BottomDrawerState.open() 用于打开抽屉
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