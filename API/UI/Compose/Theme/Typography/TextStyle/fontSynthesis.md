功能:

+ 设置字体合成的可能选项。
    + FontSynthesis 用于指定当使用的 FontFamily 不包含粗体或倾斜字体时，系统是否应伪造粗体或倾斜字形。
    + 如果字体系列不包括请求的 FontWeight 或 FontStyle，则系统分别在 Weight 或 Style 或两者都设置时伪造粗体或倾斜字形。 如果不需要，请使用 None
      禁用字体合成。
    + 可以伪造 FontWeight 的增加而不是减少。 可以伪造倾斜的常规字体，但反之则不行。
    + FontSynthesis 的工作方式与 CSS font-synthesis 属性相同。

定义:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) fontSynthesis(String fontSynthesis)

参数:

+ String fontSynthesis - 合成选项,可选值有
    + None - 关闭字体合成。如果 FontFamily 中不存在，则不会合成粗体和斜面
    + All - 如果在 FontFamily 中不可用，系统会合成粗体和倾斜字体
    + Weight - 如果在 FontFamily 中不可用，则仅合成粗体字体。不会合成倾斜的字体。
    + Style - 如果在 FontFamily 中不可用，则仅合成倾斜字体。不会合成粗体。

返回值:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [TextStyle.fontSynthesis()](/API/UI/Compose/Theme/Typography/TextStyle/README.md?id=fontSynthesis)
  方法设置字体合成的可能选项。

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
                text("Difficult waffles")
                // Text.style() 用于配置文本样式
                style {
                    // delegate -> TextStyle
                    // TextStyle.fontStyle() 用于设置字体样式
                    fontStyle(state.value())
                    // TextStyle.fontSynthesis() 用于设置字体合成的可能选项
                    fontSynthesis("All")
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