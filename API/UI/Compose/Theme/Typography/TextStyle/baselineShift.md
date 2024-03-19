功能:

+ 设置文本从当前基线向上或向下移动的量。

定义:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) baselineShift(float multiplier)

参数:

+ float multiplier - 通过 multiplier *（基线 - 上升）移动基线

返回值:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [TextStyle.baselineShift()](/API/UI/Compose/Theme/Typography/TextStyle/README.md?id=baselineShift)
  方法设置文本从当前基线向上或向下移动的量。

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Text() 用于创建文本可组合项
    Text {
        // delegate -> Text
        // Text.text() 用于设置文本可组合项内容
        text("Text")
        // Text.style() 用于配置文本样式
        style {
            // delegate -> TextStyle
            // TextStyle.baselineShift() 用于设置文本从当前基线向上或向下移动的量。
            baselineShift(-0.5f)
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