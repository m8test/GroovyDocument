功能:

+ 设置 [BottomDrawer](/API/UI/Compose/Widget/BottomDrawer/README.md) 抽屉内容

定义:

+ [BottomDrawer](/API/UI/Compose/Widget/BottomDrawer/README.md) drawerContent(Closure closure)

参数:

+ Closure closure - 设置 [BottomDrawer](/API/UI/Compose/Widget/BottomDrawer/README.md) 抽屉内容的闭包
    + 参数 - 无
    + delegate -
      [Slot](/API/UI/Compose/Slot/Slot/README.md)([ColumnScopeModifier](/API/UI/Compose/Modifier/ColumnScopeModifier/README.md))

返回值:

+ [BottomDrawer](/API/UI/Compose/Widget/BottomDrawer/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BottomDrawer.drawerContent()](/API/UI/Compose/Widget/BottomDrawer/README.md?id=drawerContent)
  方法设置 [BottomDrawer](/API/UI/Compose/Widget/BottomDrawer/README.md) 抽屉内容

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.BottomDrawer() 用于创建 BottomDrawer 可组合项
    BottomDrawer {
        // delegate -> BottomDrawer
        // BottomDrawer.drawerContent() 用于设置 BottomDrawer 抽屉内容
        drawerContent {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("BottomDrawer抽屉内容")
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