功能:

+ 创建 [BackdropScaffoldState](/API/UI/Compose/State/BackdropScaffoldState/README.md)

定义:

+ [BackdropScaffoldState](/API/UI/Compose/State/BackdropScaffoldState/README.md) newBackdropScaffoldState(
  Closure closure)

参数:

+ Closure closure - 设置 [BackdropScaffoldState](/API/UI/Compose/State/BackdropScaffoldState/README.md) 的闭包
    + 参数 - 无
    + delegate - [BackdropScaffoldState](/API/UI/Compose/State/BackdropScaffoldState/README.md)

返回值:

+ [BackdropScaffoldState](/API/UI/Compose/State/BackdropScaffoldState/README.md) -
  新创建的 [BackdropScaffoldState](/API/UI/Compose/State/BackdropScaffoldState/README.md)

示例代码:

+ 启动一个Activity,
  并通过 [Slot.newBackdropScaffoldState()](/API/UI/Compose/Slot/Slot/README.md?id=newBackdropScaffoldState)
  方法创建 [BackdropScaffoldState](/API/UI/Compose/State/BackdropScaffoldState/README.md)

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
            }
        }
        // TextButton.onClick() 用于处理点击事件
        onClick {
            // BackdropScaffoldState.isRevealed() 用于判断后层是否显示
            if (state.isRevealed()) {
                // BackdropScaffoldState.conceal() 用于隐藏后层
                state.conceal()
            } else {
                // BackdropScaffoldState.reveal() 用于显示后层
                state.reveal()
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