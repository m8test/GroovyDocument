功能:

+ 设置可组合项显示文本的最大行数.

定义:

+ [Text](/API/UI/Compose/Widget/Text/README.md) maxLines(int maxLines)

参数:

+ int maxLines - 可组合项显示文本的最大行数.

返回值:

+ [Text](/API/UI/Compose/Widget/Text/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity显示 [Text](/API/UI/Compose/Widget/Text/README.md) 可组合项,
  并通过 [Text.maxLines()](/API/UI/Compose/Widget/Text/README.md?id=maxLines) 方法设置可组合项显示文本的最大行数.

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
                text("1" * 100)
                // Text.maxLines() 用于设置文本显示最大行数
                maxLines(1)
            }
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("2" * 100)
                // Text.maxLines() 用于设置文本显示最大行数
                maxLines(2)
            }
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("3" * 100)
                // Text.maxLines() 用于设置文本显示最大行数
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