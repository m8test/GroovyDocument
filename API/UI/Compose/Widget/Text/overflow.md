功能:

+ 设置文本超出可组合项范围的显示模式.

定义:

+ [Text](/API/UI/Compose/Widget/Text/README.md) overflow(String overflow)

参数:

+ String overflow - 需要设置的显示模式,可取值有三个,分别是 Clip, Visible 和 Ellipsis
    + Clip - 剪切溢出的文本以修复其容器。
    + Visible -
      显示所有文本，即使指定边界中没有足够的空间。Visible意味着文本可能在可组合项边界之外显示文本。这确保向用户显示所有文本，并且通常为大多数文本显示的正确选择。这确实意味着文本可能在视觉上占据大于其可组合边界的区域。这可能导致出现以下情况：
      1.显示在背景边界之外，并可在可与 2.固定高度和宽度。
    + Ellipsis - 使用省略号表示文本已溢出。

返回值:

+ [Text](/API/UI/Compose/Widget/Text/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity显示 [Text](/API/UI/Compose/Widget/Text/README.md) 可组合项,
  并通过 [Text.overflow()](/API/UI/Compose/Widget/Text/README.md?id=overflow) 方法设置文本超出可组合项范围时的显示模式.

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
                text("Clip" * 20)
                // Text.overflow() 用于设置文本超出范围时的显示模式
                overflow("Clip")
                // Text.maxLines() 用于设置文本显示最大行数
                maxLines(1)
            }
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Visible" * 20)
                // Text.overflow() 用于设置文本超出范围时的显示模式
                overflow("Visible")
                // Text.maxLines() 用于设置文本显示最大行数
                maxLines(1)
            }
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Ellipsis" * 20)
                // Text.overflow() 用于设置文本超出范围时的显示模式
                overflow("Ellipsis")
                // Text.maxLines() 用于设置文本显示最大行数
                maxLines(1)
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