功能:

+ 设置字体样式。

定义:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) fontStyle(String fontStyle)

参数:

+ String fontStyle - 字体样式,可选值有
    + Italic - 使用专为倾斜设计的字形
    + Normal - 使用直立字形

返回值:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [TextStyle.fontStyle()](/API/UI/Compose/Theme/Typography/TextStyle/README.md?id=fontStyle) 方法设置字体样式

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def state = mutableStateOf("Italic")
    // Slot.Button() 用于创建 Button 可组合项
    Button {
        // delegate -> Button
        // Button.content() 用于设置按钮内容
        content {
            // delegate -> Slot
            // Button.onClick() 用于处理点击事件
            onClick {
                if (state.value() == "Normal")
                    state.value("Italic")
                else
                    state.value("Normal")
            }
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.withSingleStates() 用于设置可组合项使用到的所有 SingleState
                withSingleStates(state)
                // Text.text() 用于设置文本可组合项内容
                text("Text")
                // Text.style() 用于配置文本样式
                style {
                    // delegate -> TextStyle
                    // TextStyle.fontStyle() 用于设置字体样式
                    fontStyle(state.value())
                    // TextStyle.fontFamily() 用于设置文本字体
                    fontFamily("Cursive")
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