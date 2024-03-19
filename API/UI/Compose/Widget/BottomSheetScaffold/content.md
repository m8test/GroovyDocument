功能:

+ 设置 [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) 内容

定义:

+ [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) content(Closure closure)

参数:

+ Closure closure - 设置 [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) 内容的闭包
    + 参数 - [PaddingValues](/API/UI/Compose/Graphics/PaddingValues/README.md)
    + delegate -
      [Slot](/API/UI/Compose/Slot/Slot/README.md)([Modifier](/API/UI/Compose/Modifier/Modifier/README.md))

返回值:

+ [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BottomSheetScaffold.content()](/API/UI/Compose/Widget/BottomSheetScaffold/README.md?id=content)
  方法设置 [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) 内容

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.BottomSheetScaffold() 用于创建 BottomSheetScaffold 可组合项
    BottomSheetScaffold {
        // delegate -> BottomSheetScaffold
        // BottomSheetScaffold.content() 用于设置 BottomSheetScaffold 内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("BottomSheetScaffold内容")
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