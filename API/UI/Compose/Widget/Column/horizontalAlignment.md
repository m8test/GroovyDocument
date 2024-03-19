功能:

+ 设置水平方向对齐方式.

定义:

+ [Column](/API/UI/Compose/Widget/Column/README.md) horizontalAlignment(String alignment)

参数:

+ String alignment - 水平对齐方式,可选值有
    + Start - 左对齐
    + End - 右对齐
    + CenterHorizontally - 水平居中对齐

返回值:

+ [Column](/API/UI/Compose/Widget/Column/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [Column.horizontalAlignment()](/API/UI/Compose/Widget/Column/README.md?id=horizontalAlignment)
  方法设置水平方向对齐方式.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Column() 用于创建 Column 可组合项
    Column {
        // delegate -> Column
        // Column.modifier() 用于修饰 Composable
        modifier {
            // delegate -> Modifier
            // Modifier.fillMaxSize() 用于设置填充父可组合项宽度和高度, 参数为填充父可组合项的比例, 取值区间为 0.0f-1.0f
            fillMaxSize(1.0f)
        }
        // Column.horizontalAlignment() 用于设置水平方向对齐方式
        horizontalAlignment("CenterHorizontally")
        // Column.content() 用于设置 Column 内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Column")
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