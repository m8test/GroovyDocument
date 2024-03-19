功能:

+ 设置前层内容.

定义:

+ [BackdropScaffold](/API/UI/Compose/Widget/BackdropScaffold/README.md) frontLayerContent(Closure closure)

参数:

+ Closure closure - 设置前层内容的闭包
    + 参数 - 无
    + delegate -
      [Slot](/API/UI/Compose/Slot/Slot/README.md)([Modifier](/API/UI/Compose/Modifier/Modifier/README.md))

返回值:

+ [BackdropScaffold](/API/UI/Compose/Widget/BackdropScaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BackdropScaffold.frontLayerContent()](/API/UI/Compose/Widget/BackdropScaffold/README.md?id=frontLayerContent)
  方法设置前层内容.

```groovy

// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.BackdropScaffold() 用于创建 BackdropScaffold 可组合项
    BackdropScaffold {
        // delegate -> BackdropScaffold
        // BackdropScaffold.frontLayerContent() 用于设置前层内容
        frontLayerContent {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("前层内容")
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