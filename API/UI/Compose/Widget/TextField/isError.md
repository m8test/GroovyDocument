功能:

+ 设置输入框内容是否显示错误样式.

定义:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) isError(boolean isError)

参数:

+ boolean isError - true表示输入框内容显示错误样式,false表示输入框内容不显示错误样式

返回值:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [TextField.isError()](/API/UI/Compose/Widget/TextField/README.md?id=isError)
  方法设置输入框内容是否显示错误样式.

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
                value("错误样式")
                // TextField.isError() 用于设置输入框内容是否显示错误样式
                isError(true)
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