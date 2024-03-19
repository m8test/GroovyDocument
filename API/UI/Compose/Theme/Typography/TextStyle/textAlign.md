功能:

+ 设置文字对齐方式

定义:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) textAlign(String textAlign)

参数:

+ String textAlign - 对齐方式,可选值有
    + Center - 将文本对齐到容器的中心。
    + End - 对齐容器尾部的文本。对于从左到右的文本 (ResolvedTextDirection.Ltr)，这是右边缘。对于从右到左的文本 (
      ResolvedTextDirection.Rtl)，如阿拉伯语，这是左边缘。
    + Justify - 拉伸以软换行符结尾的文本行以填充容器的宽度。以硬换行符结尾的行与开始边缘对齐。
    + Left - 将文本对齐到容器的左边缘。
    + Right - 将文本对齐到容器的右边缘。
    + Start - 对齐容器前缘的文本。对于从左到右的文本 (ResolvedTextDirection.Ltr)，这是左边缘。对于从右到左的文本 (
      ResolvedTextDirection.Rtl)，如阿拉伯语，这是右边缘。

返回值:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [TextStyle.textAlign()](/API/UI/Compose/Theme/Typography/TextStyle/README.md?id=textAlign) 方法设置文字对齐方式

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Text() 用于创建文本可组合项
    Text {
        // delegate -> Text
        // Text.text() 用于设置文本可组合项内容
        text("Text")
        // Text.modifier() 用于修饰 Composable
        modifier {
            // delegate -> Modifier
            // Modifier.height() 用于设置高度
            height(250)
            // Modifier.width() 用于设置宽度
            width(250)
        }
        // Text.style() 用于配置文本样式
        style {
            // delegate -> TextStyle
            // TextStyle.textAlign() 用于设置文字对齐方式
            textAlign("Center")
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