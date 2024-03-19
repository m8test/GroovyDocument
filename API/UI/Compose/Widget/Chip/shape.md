功能:

+ 设置 [Chip](/API/UI/Compose/Widget/Chip/README.md) 形状.

定义:

+ [Chip](/API/UI/Compose/Widget/Chip/README.md) shape(Closure closure)

参数:

+ Closure closure - 设置形状的闭包
    + 参数 - 无
    + delegate - [Shape](/API/UI/Compose/Theme/Shape/Shape/README.md)

返回值:

+ [Chip](/API/UI/Compose/Widget/Chip/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Chip.shape()](/API/UI/Compose/Widget/Chip/README.md?id=shape)
  方法设置 [Chip](/API/UI/Compose/Widget/Chip/README.md) 形状.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Chip() 用于创建 Chip 可组合项
    Chip {
        // delegate -> Chip
        // Chip.shape() 用于设置 Chip 形状
        shape {
            // delegate -> Shape
            // Shape.all() 用于设置四个角尺寸
            all(20, "dp")
            // Shape.cutCorner() 用于设置角的类型为切角
            cutCorner()
        }
        // Chip.colors() 用于设置 Chip 颜色
        colors {
            // delegate -> ChipColors
            // ChipColors.backgroundColor() 用于设置 Chip 背景颜色
            backgroundColor {
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