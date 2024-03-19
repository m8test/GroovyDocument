功能:

+ 设置文字装饰

定义:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) textDecoration(List<String>
  textDecorations)

参数:

+ List<String> textDecorations - 装饰方式,可选值有
    + LineThrough - 在文本上绘制一条水平线。
    + Underline - 在文本下方绘制一条水平线。
    + None - 无装饰

返回值:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [TextStyle.textDecoration()](/API/UI/Compose/Theme/Typography/TextStyle/README.md?id=textDecoration)
  方法设置文字装饰

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
            // TextStyle.textDecoration() 用于设置文字装饰
            textDecoration(["LineThrough", "Underline"])
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