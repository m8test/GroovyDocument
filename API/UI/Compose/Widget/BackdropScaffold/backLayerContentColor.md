功能:

+ 设置后层内容颜色.

定义:

+ [BackdropScaffold](/API/UI/Compose/Widget/BackdropScaffold/README.md) backLayerContentColor(Closure
  closure)

参数:

+ Closure closure - 设置后层内容颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [BackdropScaffold](/API/UI/Compose/Widget/BackdropScaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BackdropScaffold.backLayerContentColor()](/API/UI/Compose/Widget/BackdropScaffold/README.md?id=backLayerContentColor)
  方法设置后层内容颜色.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.BackdropScaffold() 用于创建 BackdropScaffold 可组合项
    BackdropScaffold {
        // delegate -> BackdropScaffold
        // BackdropScaffold.backLayerContentColor() 用于设置后层内容颜色
        backLayerContentColor {
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }
        // BackdropScaffold.backLayerContent() 用于设置后层内容
        backLayerContent {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("后层内容")
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