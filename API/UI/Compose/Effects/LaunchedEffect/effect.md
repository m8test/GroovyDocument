功能:

+ 设置效应

定义:

+ [LaunchedEffect](/API/UI/Compose/Effects/LaunchedEffect/README.md) effect(Closure closure)

参数:

+ Closure closure - 设置效应的闭包
    + 参数 - 无
    + delegate - [CoroutineScope](/API/Coroutines/CoroutineScope/README.md)

返回值:

+ [LaunchedEffect](/API/UI/Compose/Effects/LaunchedEffect/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [LaunchedEffect.effect()](/API/UI/Compose/Effects/LaunchedEffect/README.md?id=effect)
  方法设置效应

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
            // Slot.LaunchedEffect() 用于创建 LaunchedEffect
            LaunchedEffect {
                // delegate -> LaunchedEffect
                // LaunchedEffect.effect() 用于设置效应
                effect {
                    // delegate -> CoroutineScope
                    // CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
                    launch({
                        // delegate -> CoroutineContext
                        dispatcher("IO")
                    }, "DEFAULT") {
                        // delegate -> CoroutineScope
                        $console.log("进入")
                    }
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