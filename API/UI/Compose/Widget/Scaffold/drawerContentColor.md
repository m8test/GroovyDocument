功能:

+ 设置抽屉内容颜色

定义:

+ [Scaffold](/API/UI/Compose/Widget/Scaffold/README.md) drawerContentColor(Closure closure)

参数:

+ Closure closure - 设置抽屉内容颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [Scaffold](/API/UI/Compose/Widget/Scaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [Scaffold.drawerContentColor()](/API/UI/Compose/Widget/Scaffold/README.md?id=drawerContentColor)
  方法设置抽屉内容颜色

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Scaffold() 用于创建 Scaffold 可组合项
    Scaffold {
        // delegate -> Scaffold
        // Scaffold.drawerContentColor() 用于设置抽屉内容颜色
        drawerContentColor {
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }
        // Scaffold.drawerContent() 用于设置抽屉内容
        drawerContent {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("抽屉内容")
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