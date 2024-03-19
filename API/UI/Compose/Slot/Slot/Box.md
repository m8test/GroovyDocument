功能:

+ 创建 [Box](/API/UI/Compose/Widget/Box/README.md) 可组合项

定义:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) Box(Closure closure)

参数:

+ Closure closure - 设置 [Box](/API/UI/Compose/Widget/Box/README.md) 的闭包
    + 参数 - 无
    + delegate - [Box](/API/UI/Compose/Widget/Box/README.md)

返回值:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Slot.Box()](/API/UI/Compose/Slot/Slot/README.md?id=Box)
  方法创建 [Box](/API/UI/Compose/Widget/Box/README.md) 可组合项.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Box() 用于创建 Box 可组合项
    Box {
        // delegate -> Box
        // Box.content() 用于设置 Box 内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Box内容")
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