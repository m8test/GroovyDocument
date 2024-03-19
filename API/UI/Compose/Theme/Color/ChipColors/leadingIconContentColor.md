功能:

+ 设置 [Chip](/API/UI/Compose/Widget/Chip/README.md) 左边图标内容颜色.

定义:

+ [ChipColors](/API/UI/Compose/Theme/Color/ChipColors/README.md) leadingIconContentColor(Closure closure)

参数:

+ Closure closure - 设置颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [ChipColors](/API/UI/Compose/Theme/Color/ChipColors/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [ChipColors.leadingIconContentColor()](/API/UI/Compose/Theme/Color/ChipColors/README.md?id=leadingIconContentColor)
  方法设置 [Chip](/API/UI/Compose/Widget/Chip/README.md) 左边图标内容颜色.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Chip() 用于创建 Chip 可组合项
    Chip {
        // delegate -> Chip
        // Chip.leadingIcon() 用于设置 Chip 左边图标
        leadingIcon {
            // delegate -> Slot
            // Slot.Icon() 用于创建 Icon 可组合项
            Icon {
                // delegate -> Icon
                // Icon.contentDescription() 用于设置图标内容描述
                contentDescription("添加")
                // Icon.vector() 用于设置图标矢量图
                vector("Filled", "Add")
            }
        }
        // Chip.colors() 用于设置 Chip 颜色
        colors {
            // delegate -> ChipColors
            // ChipColors.leadingIconContentColor() 用于设置 Chip 左边图标内容颜色
            leadingIconContentColor {
                // delegate -> Color
                // Color.red() 用于配置红色通道
                red(255)
            }
        }
        // Chip.content() 用于设置 Chip 内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Chip")
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