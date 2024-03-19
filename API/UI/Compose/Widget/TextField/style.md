功能:

+ 设置输入框字体样式.

定义:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) style(Closure closure)

参数:

+ Closure closure - 设置字体样式的闭包
    + 参数 - 无
    + delegate - [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md)

返回值:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [TextField.style()](/API/UI/Compose/Widget/TextField/README.md?id=style) 方法设置输入框字体样式.

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
            // Slot.TextField() 用于创建 TextField 可组合项
            TextField {
                // delegate -> TextField
                // TextField.value() 用于设置输入框内容
                value("字体大小:20sp")
                // TextField.style() 用于设置输入框颜色.
                style {
                    // delegate -> TextStyle
                    // TextStyle.fontSize() 用于设置字体大小
                    fontSize(20, "sp")
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