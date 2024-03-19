功能:

+ 设置按钮获取焦点时的海拔.

定义:

+ [ButtonElevation](/API/UI/Compose/Widget/Button/ButtonElevation/README.md) focusedElevation(Number value)

参数:

+ Number value - 需要设置的海拔

返回值:

+ [ButtonElevation](/API/UI/Compose/Widget/Button/ButtonElevation/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [ButtonElevation.focusedElevation()](/API/UI/Compose/Widget/Button/ButtonElevation/README.md?id=focusedElevation)
  方法设置按钮获取焦点时的海拔.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Button() 用于创建 Button 可组合项
    Button {
        // delegate -> Button
        // Button.elevation() 用于设置按钮海拔
        elevation {
            // delegate -> ButtonElevation
            // ButtonElevation.focusedElevation() 用于设置按钮获取焦点时的海拔
            focusedElevation(20)
        }
        // Button.content() 用于设置按钮内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Button")
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