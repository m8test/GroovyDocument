功能:

+ 设置文本字体

定义:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) fontFamily(String fontFamily)

参数:

+ String fontFamily - 文本字体,可选值有
    + Default - 平台默认字体。
    + Cursive - 草书，手写字体家族。如果设备不支持此字体系列，系统将回退到默认字体。
    + Monospace - 字形具有相同固定宽度的字体系列。
    + Serif - 脚本的正式文本样式。
    + SansSerif - 具有低对比度和简单笔画结尾的字体系列。

返回值:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [TextStyle.fontFamily()](/API/UI/Compose/Theme/Typography/TextStyle/README.md?id=fontFamily) 方法设置文本字体

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
            // TextStyle.fontFamily() 用于设置文本字体
            fontFamily("Cursive")
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