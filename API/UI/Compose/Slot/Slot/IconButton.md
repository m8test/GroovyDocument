功能:

+ 创建 [IconButton](/API/UI/Compose/Widget/IconButton/README.md) 可组合项

定义:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) IconButton(Closure closure)

参数:

+ Closure closure - 设置 [IconButton](/API/UI/Compose/Widget/IconButton/README.md) 的闭包
    + 参数 - 无
    + delegate - [IconButton](/API/UI/Compose/Widget/IconButton/README.md)

返回值:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Slot.IconButton()](/API/UI/Compose/Slot/Slot/README.md?id=IconButton)
  方法创建 [IconButton](/API/UI/Compose/Widget/IconButton/README.md) 可组合项

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.IconButton() 用于创建 IconButton 可组合项
    IconButton {
        // delegate -> IconButton
        // IconButton.content() 用于设置图标按钮内容
        content {
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