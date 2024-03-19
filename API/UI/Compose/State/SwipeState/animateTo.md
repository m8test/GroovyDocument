功能:

+ 通过启动动画将状态设置为目标值。

定义:

+ [Job](/API/Coroutines/Job/README.md) animateTo(String
  targetValue, [AnimationSpec](/API/UI/Compose/Animation/AnimationSpec/README.md)
  animationSpec)

参数:

+ String targetValue - 目标值,
  参考 [MaterialState.initialValue()](/API/UI/Compose/State/MaterialState/README.md?id=initialValue)
+ [AnimationSpec](/API/UI/Compose/Animation/AnimationSpec/README.md)
  animationSpec - 动画效果

返回值:

+ [Job](/API/Coroutines/Job/README.md) - 协程对象

示例代码:

+ 启动一个Activity, 并通过 [SwipeState.animateTo()](/API/UI/Compose/State/SwipeState/README.md?id=animateTo)
  方法通过启动动画将状态设置为目标值。

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
            // Animations.spring() 用于创建一个使用给定弹簧常数（即阻尼比和刚度）的 AnimationSpec。
            def animationSpec = $animations.spring(1f, 1500f, null)
            // BackdropScaffoldState.isRevealed() 用于判断后层是否显示
            if (state.isRevealed()) {
                // BottomDrawerState.animateTo() 用于通过启动动画将状态设置为目标值。
                state.animateTo("Concealed", animationSpec)
            } else {
                // BottomDrawerState.animateTo() 用于通过启动动画将状态设置为目标值。
                state.animateTo("Revealed", animationSpec)
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
        // Animations.tween() 用于创建一个配置有给定持续时间、延迟和缓动曲线的 AnimationSpec。
        def animation = $animations.tween(2000, 1000) { it }
        // BackdropScaffoldState.animationSpec() 用于设置新状态动画的默认动画
        animationSpec(animation)
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