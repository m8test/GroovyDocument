功能:

+ 设置文字阴影

定义:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) shadow(Closure closure)

参数:

+ Closure closure - 设置阴影的闭包
    + 参数 - 无
    + delegate - [Shadow](/API/UI/Compose/Theme/Typography/Shadow/README.md)

返回值:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [TextStyle.shadow()](/API/UI/Compose/Theme/Typography/TextStyle/README.md?id=shadow)
  方法设置文字阴影

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
            // TextStyle.shadow() 用于设置文字阴影
            shadow {
                // delegate - Shadow
                // Shadow.color() 用于设置阴影颜色
                color {
                    // delegate -> Color
                    // Color.red() 用于配置红色通道
                    red(255)
                }
                // Shadow.offset() 用于设置阴影偏移量
                offset {
                    // delegate -> Offset
                    // Offset.x() 用于设置横坐标偏移量
                    x(10)
                    // Offset.y() 用于设置纵坐标偏移量
                    y(10)
                }
                // Shadow.blurRadius() 用于设置阴影模糊半径
                blurRadius(0.0f)
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