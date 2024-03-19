功能:

+ 创建一个使用给定弹簧常数（即阻尼比和刚度）的 [SpringSpec](/API/UI/Compose/Animation/SpringSpec/README.md)。

定义:

+ [SpringSpec](/API/UI/Compose/Animation/SpringSpec/README.md) spring(float dampingRatio, float
  stiffness, Object visibilityThreshold)

参数:

+ float dampingRatio - 弹簧的阻尼比
+ float stiffness - 弹簧的刚度
+ Object visibilityThreshold - 可选地指定可见性阈值

返回值:

+ [SpringSpec](/API/UI/Compose/Animation/SpringSpec/README.md) -
  新创建的 [SpringSpec](/API/UI/Compose/Animation/SpringSpec/README.md) 对象

示例代码:

+ 启动一个Activity, 并通过 [Animations.spring()](/API/UI/Compose/Animation/Animations/README.md?id=spring)
  方法创建一个使用给定弹簧常数（即阻尼比和刚度）的 [SpringSpec](/API/UI/Compose/Animation/SpringSpec/README.md)。

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
                    // Animations.spring() 用于创建一个使用给定弹簧常数（即阻尼比和刚度）的 AnimationSpec。
                    def animationSpec = $animations.spring(1f, 1500f, null)
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
                    // Animations.spring() 用于创建一个使用给定弹簧常数（即阻尼比和刚度）的 AnimationSpec。
                    def animationSpec = $animations.spring(1f, 1500f, null)
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