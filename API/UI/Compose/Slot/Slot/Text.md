功能:

+ 创建文本可组合项

定义:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) Text(Closure closure)

参数:

+ Closure closure - 设置 [Text](/API/UI/Compose/Widget/Text/README.md) 的闭包
    + 参数 - 无
    + delegate - [Text](/API/UI/Compose/Widget/Text/README.md)

返回值:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity显示 Text 可组合项, 并通过 [Slot.Text()](/API/UI/Compose/Slot/Slot/README.md?id=Text) 方法创建文本可组合项

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
                    // TextStyle.fontSize() 用于设置字体大小
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