功能:

+ 获取当前位置在 [SwipeProgress.from()](/API/UI/Compose/State/SwipeState/SwipeProgress/README.md?id=from)
  到 [SwipeProgress.to()](/API/UI/Compose/State/SwipeState/SwipeProgress/README.md?id=to) 之间的分数,
  介于 0 和 1 之间。

定义:

+ float fraction()

参数:

+ 无

返回值:

+ float - 当前位置在 [SwipeProgress.from()](/API/UI/Compose/State/SwipeState/SwipeProgress/README.md?id=from)
  到 [SwipeProgress.to()](/API/UI/Compose/State/SwipeState/SwipeProgress/README.md?id=to)
  之间的分数

示例代码:

+ 启动一个Activity,
  并通过 [SwipeProgress.fraction()](/API/UI/Compose/State/SwipeState/SwipeProgress/README.md?id=fraction)
  方法获取当前位置在 [SwipeProgress.from()](/API/UI/Compose/State/SwipeState/SwipeProgress/README.md?id=from)
  到 [SwipeProgress.to()](/API/UI/Compose/State/SwipeState/SwipeProgress/README.md?id=to)
  之间的分数

```groovy
def MyTextButton = { state ->
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
                text("点我")
                // Text.withAggregatedStates() 用于设置可组合项重组需要的聚合状态
                withAggregatedStates((state): ["progress"])
                // Text.style() 用于配置文本样式
                style {
                    // delegate -> TextStyle
                    // BackdropScaffoldState.progress() 用于获取有关正在进行的滑动或动画的信息(如果有)
                    def currentDrawerValue = state.progress()
                    // SwipeProgress.fraction() 用于获取当前位置在 from 到 to 之间的分数
                    if (currentDrawerValue.fraction() >= 0.5f) {
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
            // BackdropScaffoldState.isConcealed() 用于判断后层是否隐藏
            if (state.isConcealed()) {
                // BackdropScaffoldState.reveal() 用于显示后层
                state.reveal()
            } else {
                // BackdropScaffoldState.conceal() 用于隐藏后层
                state.conceal()
            }
        }
    }
}

// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newBackdropScaffoldState() 用于创建 BackdropScaffoldState
    def backdropScaffoldState = newBackdropScaffoldState {
        // delegate -> BackdropScaffoldState
    }
    // Slot.BackdropScaffold() 用于创建 BackdropScaffold 可组合项
    BackdropScaffold {
        // delegate -> BackdropScaffold
        // BackdropScaffold.scaffoldState() 用于设置 BackdropScaffoldState
        scaffoldState(backdropScaffoldState)
        // BackdropScaffold.gesturesEnabled() 用于设置是否开启手势
        gesturesEnabled(false)
        // BackdropScaffold.backLayerBackgroundColor() 用于设置后层背景颜色
        backLayerBackgroundColor {
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }
        // BackdropScaffold.backLayerContent() 用于设置后层内容
        backLayerContent {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("后层内容")
            }
        }
        // BackdropScaffold.frontLayerContent() 用于设置前层内容
        frontLayerContent {
            // delegate -> Slot
            MyTextButton.delegate = delegate
            MyTextButton(backdropScaffoldState)
        }
        // BackdropScaffold.appBar() 用于设置背景顶部应用程序栏
        appBar {
            // delegate -> Slot
            MyTextButton.delegate = delegate
            MyTextButton(backdropScaffoldState)
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