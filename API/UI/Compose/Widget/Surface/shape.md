功能:

+ 设置 [Surface](/API/UI/Compose/Widget/Surface/README.md) 形状.

定义:

+ [Surface](/API/UI/Compose/Widget/Surface/README.md) shape(Closure closure)

参数:

+ Closure closure - 设置形状的闭包
    + 参数 - 无
    + delegate - [Shape](/API/UI/Compose/Theme/Shape/Shape/README.md)

返回值:

+ [Surface](/API/UI/Compose/Widget/Surface/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Surface.shape()](/API/UI/Compose/Widget/Surface/README.md?id=shape)
  方法设置 [Surface](/API/UI/Compose/Widget/Surface/README.md) 形状.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Surface() 用于创建 Surface 可组合项
    Surface {
        // delegate -> Surface
        // Surface.shape() 用于设置 Surface 形状
        shape {
            // delegate -> Shape
            // Shape.all() 用于设置四个角尺寸
            all(20, "dp")
            // Shape.roundedCorner() 用于设置角的类型为圆角
            roundedCorner()
        }
        // Surface.color() 用于设置 Surface 背景颜色
        color {
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }
        // Surface.content() 用于设置 Surface 内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Surface")
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