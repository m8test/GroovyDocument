功能:

+ 创建 [DisposableEffect](/API/UI/Compose/Effects/DisposableEffect/README.md)

定义:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) DisposableEffect(Closure closure)

参数:

+ Closure closure - 设置 [DisposableEffect](/API/UI/Compose/Effects/DisposableEffect/README.md) 的闭包
    + 参数 - 无
    + delegate - [DisposableEffect](/API/UI/Compose/Effects/DisposableEffect/README.md)

返回值:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Slot.DisposableEffect()](/API/UI/Compose/Slot/Slot/README.md?id=DisposableEffect)
  方法创建 [DisposableEffect](/API/UI/Compose/Effects/DisposableEffect/README.md)

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def state = mutableStateOf(false)
    // Slot.Column() 用于创建 Column 可组合项
    Column {
        // delegate -> Column
        // Column.content() 用于设置 Column 内容
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
                        // Text.withSingleStates() 用于设置可组合项使用到的所有 SingleState
                        withSingleStates(state)
                        if (state.value()) {
                            // Text.text() 用于设置文本可组合项内容
                            text("隐藏")
                        } else {
                            // Text.text() 用于设置文本可组合项内容
                            text("显示")
                        }
                    }
                }
                // TextButton.onClick() 用于处理点击事件
                onClick {
                    state.value(!state.value())
                }
            }
            // Slot.Row() 用于创建 Row 可组合项
            Row {
                // delegate -> Row
                // Row.withSingleStates() 用于设置可组合项使用到的所有 SingleState
                withSingleStates(state)
                // Row.show() 用于设置可组合项是否显示
                show(state.value())
                // Row.content() 用于设置 Row 内容
                content {
                    // delegate -> Slot
                    // Slot.DisposableEffect() 用于创建 DisposableEffect
                    DisposableEffect {
                        // delegate -> DisposableEffect
                        // DisposableEffect.effect() 用于设置效应
                        effect {
                            // delegate -> DisposableEffectScope
                            $console.log("进入")
                            // DisposableEffectScope.onDispose() 用于为 DisposableEffect 在它离开组合或其键更改时运行监听器
                            onDispose {
                                $console.log("退出")
                            }
                        }
                    }
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        // Text.text() 用于设置文本可组合项内容
                        text("Row")
                    }
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