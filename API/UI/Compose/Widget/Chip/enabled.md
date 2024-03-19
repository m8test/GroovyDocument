功能:

+ 设置是否启用 [Chip](/API/UI/Compose/Widget/Chip/README.md) .

定义:

+ [Chip](/API/UI/Compose/Widget/Chip/README.md) enabled(boolean value)

参数:

+ boolean value - true表示启用 [Chip](/API/UI/Compose/Widget/Chip/README.md)
  ,false表示不启用 [Chip](/API/UI/Compose/Widget/Chip/README.md)

返回值:

+ [Chip](/API/UI/Compose/Widget/Chip/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Chip.enabled()](/API/UI/Compose/Widget/Chip/README.md?id=enabled)
  方法设置是否启用 [Chip](/API/UI/Compose/Widget/Chip/README.md) .

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Chip() 用于创建 Chip 可组合项
    Chip {
        // delegate -> Chip
        // Chip.enabled() 用于设置是否启用 Chip
        enabled(false)
        // Chip.content() 用于设置 Chip 内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Chip")
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