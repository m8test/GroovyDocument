功能:

+ 设置新状态动画的默认动画。

定义:

+ [ModalBottomSheetState](/API/UI/Compose/State/ModalBottomSheetState/README.md)
  animationSpec([AnimationSpec](/API/UI/Compose/Animation/AnimationSpec/README.md) animationSpec)

参数:

+ [AnimationSpec](/API/UI/Compose/Animation/AnimationSpec/README.md) animationSpec - 动画效果

返回值:

+ [ModalBottomSheetState](/API/UI/Compose/State/ModalBottomSheetState/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [ModalBottomSheetState.animationSpec()](/API/UI/Compose/State/ModalBottomSheetState/README.md?id=animationSpec)
  方法设置新状态动画的默认动画。

```groovy
def MyTextButton = { btnText, onBtnClick ->
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
                text(btnText)
            }
        }
        // TextButton.onClick() 用于处理点击事件
        onClick {
            onBtnClick()
        }
    }
}

// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newModalBottomSheetState() 用于创建 ModalBottomSheetState
    def state = newModalBottomSheetState {
        // delegate -> ModalBottomSheetState
        // Animations.tween() 用于创建一个配置有给定持续时间、延迟和缓动曲线的 AnimationSpec。
        def animation = $animations.tween(2000, 1000) { it }
        // ModalBottomSheetState.animationSpec() 用于设置新状态动画的默认动画
        animationSpec(animation)
    }
    // Slot.ModalBottomSheetLayout() 用于创建 ModalBottomSheetLayout 可组合项
    ModalBottomSheetLayout {
        // delegate -> ModalBottomSheetLayout
        // ModalBottomSheetLayout.sheetState() 用于设置 ModalBottomSheetState
        sheetState(state)
        // ModalBottomSheetLayout.sheetContent() 用于设置 ModalBottomSheetLayout 底页内容
        sheetContent {
            // delegate -> Slot
            MyTextButton.delegate = delegate
            MyTextButton("关闭") {
                // ModalBottomSheetState.hide() 用于隐藏 ModalBottomSheetLayout 底页
                state.hide()
            }
        }
        // ModalBottomSheetLayout.content() 用于设置 ModalBottomSheetLayout 内容
        content {
            // delegate -> Slot
            // Slot.Column() 用于创建 Column 可组合项
            Column {
                // delegate -> Column
                // Column.content() 用于设置 Column 可组合项中的内容
                content {
                    // delegate -> Slot
                    MyTextButton.delegate = delegate
                    MyTextButton("显示") {
                        // ModalBottomSheetState.show() 用于显示 ModalBottomSheetLayout 底页
                        state.show()
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