功能:

+ 设置可组合项是否显示.

定义:

+ [Composable](/API/UI/Compose/Widget/Composable/README.md) show(boolean show)

参数:

+ boolean show - true表示显示,false表示不显示

返回值:

+ [Composable](/API/UI/Compose/Widget/Composable/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity显示 [Text](/API/UI/Compose/Widget/Text/README.md) 可组合项,
  并通过 [Composable.show()](/API/UI/Compose/Widget/Composable/README.md?id=show) 方法设置 [Text](/API/UI/Compose/Widget/Text/README.md)
  可组合项显示与否.

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
                text("show:false")
                // Composable.show() 用于设置可组合项是否显示, 因为 Text 可组合项继承自 Composable ,所以可以调用 show 方法
                show(false)
            }
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("show:true")
                // Composable.show() 用于设置可组合项是否显示 ,因为 Text 可组合项继承自 Composable ,所以可以调用 show 方法
                show(true)
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