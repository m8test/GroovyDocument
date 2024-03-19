功能:

+ 设置 [BottomDrawer](/API/UI/Compose/Widget/BottomDrawer/README.md) 抽屉内容颜色

定义:

+ [BottomDrawer](/API/UI/Compose/Widget/BottomDrawer/README.md) drawerContentColor(Closure closure)

参数:

+ Closure closure - 设置 [BottomDrawer](/API/UI/Compose/Widget/BottomDrawer/README.md) 抽屉内容颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [BottomDrawer](/API/UI/Compose/Widget/BottomDrawer/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BottomDrawer.drawerContentColor()](/API/UI/Compose/Widget/BottomDrawer/README.md?id=drawerContentColor)
  方法设置 [BottomDrawer](/API/UI/Compose/Widget/BottomDrawer/README.md) 抽屉内容颜色

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
        // BottomDrawer.drawerContentColor() 用于设置 BottomDrawer 抽屉内容颜色
        drawerContentColor {
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
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