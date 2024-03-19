功能:

+ 设置输入框内容是否仅显示为单行.

定义:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) singleLine(boolean singleLine)

参数:

+ boolean singleLine - true表示输入框内容仅显示为单行,false表示输入框内容不仅显示为单行

返回值:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [TextField.singleLine()](/API/UI/Compose/Widget/TextField/README.md?id=singleLine)
  方法设置输入框内容是否仅显示为单行.

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
                value("1" * 100)
                // TextField.singleLine() 用于设置输入框内容是否仅显示为单行
                singleLine(true)
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