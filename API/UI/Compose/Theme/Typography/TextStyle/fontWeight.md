功能:

+ 设置字体粗细,范围为1-1000。

定义:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) fontWeight(String|int fontWeight)

参数:

+ String|int fontWeight - 字体粗细,如果是int类型,范围1-1000,如果是String类型,可选值有
    + Bold - 比正常重的常用字体粗细,int值为700
    + Normal - 默认字体粗细,int值为400
    + Black - int值为900
    + Thin - int值为100
    + Light - int值为300
    + ExtraLight - int值为200
    + ExtraBold - int值为800
    + Medium - int值为500
    + SemiBold - int值为600

返回值:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [TextStyle.fontWeight()](/API/UI/Compose/Theme/Typography/TextStyle/README.md?id=fontWeight) 方法设置字体粗细

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def state = mutableStateOf("Bold")
    // Slot.Button() 用于创建 Button 可组合项
    Button {
        // delegate -> Button
        // Button.content() 用于设置按钮内容
        content {
            // delegate -> Slot
            // Button.onClick() 用于处理点击事件
            onClick {
                if (state.value() == "Normal")
                    state.value("Bold")
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
                    // TextStyle.fontWeight() 用于设置字体粗细
                    fontWeight(state.value())
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