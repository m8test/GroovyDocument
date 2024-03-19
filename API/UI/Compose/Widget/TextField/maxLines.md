功能:

+ 设置输入框显示最大行数.

定义:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) maxLines(int maxLines)

参数:

+ int maxLines - 输入框显示最大行数.

返回值:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [TextField.maxLines()](/API/UI/Compose/Widget/TextField/README.md?id=maxLines)
  方法设置输入框显示最大行数.

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
                // TextField.maxLines() 用于设置输入框显示最大行数
                maxLines(1)
            }
            // Slot.TextField() 用于创建 TextField 可组合项
            TextField {
                // delegate -> TextField
                // TextField.value() 用于设置输入框内容
                value("2" * 100)
                // TextField.maxLines() 用于设置输入框显示最大行数
                maxLines(2)
            }
            // Slot.TextField() 用于创建 TextField 可组合项
            TextField {
                // delegate -> TextField
                // TextField.value() 用于设置输入框内容
                value("3" * 100)
                // TextField.maxLines() 用于设置输入框显示最大行数
                maxLines(3)
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