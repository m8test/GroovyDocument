功能:

+ 设置输入框是否可用.

定义:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) enabled(boolean enabled)

参数:

+ boolean enabled - true表示输入框可用,false表示输入框不可用

返回值:

+ [TextField](/API/UI/Compose/Widget/TextField/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [TextField.enabled()](/API/UI/Compose/Widget/TextField/README.md?id=enabled)
  方法设置输入框是否可用.

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
                value("不可输入内容")
                // TextField.enabled() 用于设置输入框是否可用
                enabled(false)
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