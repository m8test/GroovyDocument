功能:

+ 设置文本是否应在软换行符处中断。

定义:

+ [Text](/API/UI/Compose/Widget/Text/README.md) softWrap(boolean softWrap)

参数:

+ boolean softWrap - 默认为true,如果为false,文本中的字形将被定位为有无限的水平空间。 overflow 和 TextAlign 可能会产生意外的效果。

返回值:

+ [Text](/API/UI/Compose/Widget/Text/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity显示 [Text](/API/UI/Compose/Widget/Text/README.md) 可组合项,
  并通过 [Text.softWrap()](/API/UI/Compose/Widget/Text/README.md?id=softWrap) 设置文本是否应在软换行符处中断。

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
                text("softWrap")
                // Text.softWrap() 用于设置文本是否应在软换行符处中断。
                softWrap(true)
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