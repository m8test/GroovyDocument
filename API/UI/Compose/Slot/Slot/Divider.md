功能:

+ 创建 [Divider](/API/UI/Compose/Widget/Divider/README.md) 可组合项

定义:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) Divider(Closure closure)

参数:

+ Closure closure - 设置 [Divider](/API/UI/Compose/Widget/Divider/README.md) 的闭包
    + 参数 - 无
    + delegate - [Divider](/API/UI/Compose/Widget/Divider/README.md)

返回值:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Slot.Divider()](/API/UI/Compose/Slot/Slot/README.md?id=Divider)
  方法创建 [Divider](/API/UI/Compose/Widget/Divider/README.md) 可组合项.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Divider() 用于创建 Divider 可组合项
    Divider {
        // delegate -> Divider
        // Divider.color() 用于设置分割线颜色
        color {
            // delegate -> Color
            // Color.green() 用于配置绿色通道
            green(255)
        }
        // Divider.thickness() 用于设置分割线厚度
        thickness(5)
        // Divider.startIndent() 用于设置分割线起始偏移量
        startIndent(20)
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