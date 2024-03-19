功能:

+ 设置图标矢量图

定义:

+ [Icon](/API/UI/Compose/Widget/Icon/README.md) vector(String type, String name)

参数:

+ String type - 图标类型,可选值有 Filled,Outlined,Rounded,TwoTone,Sharp
+ String name - 图标名称,例如 Search,Home,Menu,Close等,更多请查阅 https://fonts.google.com/icons

返回值:

+ [Icon](/API/UI/Compose/Widget/Icon/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Icon.vector()](/API/UI/Compose/Widget/Icon/README.md?id=vector) 方法设置图标矢量图

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