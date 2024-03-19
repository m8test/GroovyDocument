功能:

+ 设置图标颜色

定义:

+ [Icon](/API/UI/Compose/Widget/Icon/README.md) tint(Closure closure)

参数:

+ Closure closure - 设置颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [Icon](/API/UI/Compose/Widget/Icon/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Icon.tint()](/API/UI/Compose/Widget/Icon/README.md?id=tint) 方法设置图标颜色

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Icon() 用于创建 Icon 可组合项
    Icon {
        // delegate -> Icon
        // Icon.contentDescription() 用于设置图标内容描述
        contentDescription("添加")
        // Icon.tint() 用于设置图标颜色
        tint {
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }
        // Icon.vector() 用于设置图标矢量图
        vector("Filled", "Add")
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