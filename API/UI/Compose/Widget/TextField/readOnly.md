功能:

+ 设置输入框内容是否只读.

定义:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) readOnly(boolean readOnly)

参数:

+ boolean readOnly - true表示输入框内容只读,false表示输入框内容可读写

返回值:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [TextField.readOnly()](/API/UI/Compose/Widget/TextField/README.md?id=readOnly)
  方法设置输入框内容是否只读.

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
                value("只读内容")
                // TextField.readOnly() 用于设置输入框内容是否只读
                readOnly(true)
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