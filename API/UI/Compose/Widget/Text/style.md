功能:

+ 设置可组合项文本样式,例如字体大小,颜色,粗斜体等.

定义:

+ [Text](/API/UI/Compose/Widget/Text/README.md) style(Closure style)

参数:

+ Closure style - 用于配置样式的闭包
    + 参数 - 无
    + delegate - [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md)

返回值:

+ [Text](/API/UI/Compose/Widget/Text/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity显示 [Text](/API/UI/Compose/Widget/Text/README.md) 可组合项,
  并通过 [Text.style()](/API/UI/Compose/Widget/Text/README.md?id=style) 方法设置文本样式.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Column() 用于创建纵向布局
    Column {
        // delegate -> Column
        // Column.content() 用于设置布局内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("字体大小:20sp")
                // Text.style() 用于配置文本样式
                style {
                    // delegate -> TextStyle 
                    fontSize(20, "sp")
                }
            }
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("字体大小:40sp")
                // Text.style() 用于配置文本样式
                style {
                    // delegate -> TextStyle 
                  // TextStyle.fontSize() 用于设置字体大小
                  fontSize(40, "sp")
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