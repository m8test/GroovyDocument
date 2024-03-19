功能:

+ 获取抽屉状态的目标值。如果正在进行滑动，则这是滑动完成时抽屉将设置动画的值。如果动画正在运行，则这是该动画的目标值。
  最后，如果没有滑动或动画正在进行，则这与 [[BottomDrawerState.currentValue()](/API/UI/Compose/State/BottomDrawerState/README.md?id=currentValue)]
  相同。

定义:

+ String targetValue()

参数:

+ 无

返回值:

+ String - 当前抽屉状态值,值可为 Closed 或者 Open 以及 Expanded

示例代码:

+ 启动一个Activity,
  并通过 [BottomDrawerState.targetValue()](/API/UI/Compose/State/BottomDrawerState/README.md?id=targetValue)
  方法获取抽屉状态的目标值

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
                        // Text.withAggregatedStates() 用于设置可组合项重组需要的聚合状态
                        withAggregatedStates((state): ["targetValue"])
                        // Text.style() 用于配置文本样式
                        style {
                            // delegate -> TextStyle
                            // BottomDrawerState.targetValue() 用于获取抽屉状态的目标值
                            if (state.targetValue() == "Closed") {
                                // TextStyle.fontSize() 用于设置字体大小
                                fontSize(20, "sp")
                            } else {
                                // TextStyle.fontSize() 用于设置字体大小
                                fontSize(15, "sp")
                            }
                        }
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