功能:

+ 设置 [Chip](/API/UI/Compose/Widget/Chip/README.md) 点击事件.

定义:

+ [Chip](/API/UI/Compose/Widget/Chip/README.md) onClick(Closure closure)

参数:

+ Closure closure - 设置点击事件的闭包
    + 参数 - 无
    + delegate - 无

返回值:

+ [Chip](/API/UI/Compose/Widget/Chip/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Chip.onClick()](/API/UI/Compose/Widget/Chip/README.md?id=onClick)
  方法设置 [Chip](/API/UI/Compose/Widget/Chip/README.md) 点击事件.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Chip() 用于创建 Chip 可组合项
    Chip {
        // delegate -> Chip
        // Chip.onClick() 用于设置 Chip 点击事件
        onClick {
            $console.log(" Chip 被点击了")
        }
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