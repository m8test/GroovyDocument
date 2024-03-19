功能:

+ 创建一个用于立即将动画值切换为结束值的 [SnapSpec](/API/UI/Compose/Animation/SnapSpec/README.md)。

定义:

+ [SnapSpec](/API/UI/Compose/Animation/SnapSpec/README.md) snap(int delayMillis)

参数:

+ int delayMillis - 动画在开始前等待的时间（以毫秒为单位）

返回值:

+ [SnapSpec](/API/UI/Compose/Animation/SnapSpec/README.md) -
  新创建的 [SnapSpec](/API/UI/Compose/Animation/SnapSpec/README.md) 对象

示例代码:

+ 启动一个Activity, 并通过 [Animations.snap()](/API/UI/Compose/Animation/Animations/README.md?id=snap)
  方法创建一个用于立即将动画值切换为结束值的 [SnapSpec](/API/UI/Compose/Animation/SnapSpec/README.md)。

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
                    // Animations.snap() 用于创建一个用于立即将动画值切换为结束值的 AnimationSpec。
                    def animationSpec = $animations.snap(2000)
                    // BottomDrawerState.animateTo() 用于通过启动动画将状态设置为目标值。
                    state.animateTo("Closed", animationSpec)
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
                    // Animations.snap() 用于创建一个用于立即将动画值切换为结束值的 AnimationSpec。
                    def animationSpec = $animations.snap(2000)
                    // BottomDrawerState.animateTo() 用于通过启动动画将状态设置为目标值。
                    state.animateTo("Expanded", animationSpec)
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