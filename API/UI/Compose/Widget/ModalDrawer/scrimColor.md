功能:

+ 设置 [ModalDrawer](/API/UI/Compose/Widget/ModalDrawer/README.md) 抽屉打开时非抽屉部分的颜色

定义:

+ [ModalDrawer](/API/UI/Compose/Widget/ModalDrawer/README.md) scrimColor(Closure closure)

参数:

+ Closure closure - 设置 [ModalDrawer](/API/UI/Compose/Widget/ModalDrawer/README.md) 抽屉打开时非抽屉部分的颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [ModalDrawer](/API/UI/Compose/Widget/ModalDrawer/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [ModalDrawer.scrimColor()](/API/UI/Compose/Widget/ModalDrawer/README.md?id=scrimColor)
  方法设置 [ModalDrawer](/API/UI/Compose/Widget/ModalDrawer/README.md) 抽屉打开时非抽屉部分的颜色

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.ModalDrawer() 用于创建 ModalDrawer 可组合项
    ModalDrawer {
        // delegate -> ModalDrawer
        // ModalDrawer.drawerContent() 用于设置 ModalDrawer 抽屉内容
        drawerContent {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("ModalDrawer抽屉内容")
            }
        }
        // ModalDrawer.scrimColor() 用于设置 ModalDrawer 抽屉打开时非抽屉部分的颜色
        scrimColor {
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