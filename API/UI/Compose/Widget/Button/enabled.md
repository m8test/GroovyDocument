功能:

+ 设置是否启用按钮.

定义:

+ [Button](/API/UI/Compose/Widget/Button/README.md) enabled(boolean value)

参数:

+ boolean value - true表示启用按钮,false表示不启用按钮

返回值:

+ [Button](/API/UI/Compose/Widget/Button/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Button.enabled()](/API/UI/Compose/Widget/Button/README.md?id=enabled) 方法设置是否启用按钮.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Button() 用于创建 Button 可组合项
    Button {
        // delegate -> Button
        // Button.enabled() 用于设置是否启用按钮
        enabled(false)
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