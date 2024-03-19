功能:

+ 设置文本的几何变换

定义:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) textGeometricTransform(float scaleX,
  float skewX)

参数:

+ float scaleX - 文本在水平方向上的比例。
+ float skewX - 文本在水平方向上的剪切。 (x, y) 处的像素，其中 y 是基线上方的距离，将被转换为 (x + y * skewX, y)。

返回值:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [TextStyle.textGeometricTransform()](/API/UI/Compose/Theme/Typography/TextStyle/README.md?id=textGeometricTransform)
  方法设置文本的几何变换

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
            // TextStyle.textGeometricTransform() 用于设置文本的几何变换
            textGeometricTransform(1.5f, 1.0f)
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