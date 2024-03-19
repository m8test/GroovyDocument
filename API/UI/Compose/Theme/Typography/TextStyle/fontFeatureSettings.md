功能:

+ 设置字体提供的高级排版。格式与 CSS font-feature-settings
  属性相同： https://www.w3.org/TR/css-fonts-3/#font-feature-settings-prop

定义:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) fontFeatureSettings(String
  fontFeatureSettings)

参数:

+ String fontFeatureSettings - 参考 https://www.w3.org/TR/css-fonts-3/#font-feature-settings-prop

返回值:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [TextStyle.fontFeatureSettings()](/API/UI/Compose/Theme/Typography/TextStyle/README.md?id=fontFeatureSettings)
  方法设置字体提供的高级排版

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def state = mutableStateOf("normal")
    // Slot.Button() 用于创建 Button 可组合项
    Button {
        // delegate -> Button
        // Button.content() 用于设置按钮内容
        content {
            // delegate -> Slot
            // Button.onClick() 用于处理点击事件
            onClick {
                if (state.value() == "afrc")
                    state.value("normal")
                else
                    state.value("afrc")
            }
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.withSingleStates() 用于设置可组合项使用到的所有 SingleState
                withSingleStates(state)
                // Text.text() 用于设置文本可组合项内容
                text("Difficult waffles")
                // Text.style() 用于配置文本样式
                style {
                    // delegate -> TextStyle
                    // TextStyle.fontFeatureSettings() 用于设置字体提供的高级排版
                    fontFeatureSettings(state.value())
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