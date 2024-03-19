功能:

+ 将内容偏移。偏移量可以是正的也可以是非正的。 应用偏移量只会改变内容的位置，而不会影响其尺寸测量。此修饰符在计算内容位置时不会考虑布局方向：正 x 偏移量将始终向右移动内容。
  有关在应用偏移时考虑布局方向的修饰符，请参见 [Modifier.offset()](/API/UI/Compose/Modifier/Modifier/README.md?id=offset) 。

定义:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) absoluteOffset(Closure closure)

参数:

+ Closure closure - 配置偏移量的闭包
    + 参数 - 无
    + delegate - [Offset](/API/UI/Compose/Graphics/Offset/README.md)

返回值:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [Modifier.absoluteOffset()](/API/UI/Compose/Modifier/Modifier/README.md?id=absoluteOffset) 方法将内容偏移.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Column() 用于创建纵向布局
    Column {
        // delegate -> Column
        // Column.content() 用于设置布局内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Composable.modifier() 用于配置可组合项的 Modifier ,因为 Text 可组合项继承自 Composable ,所以可以调用 modifier 方法
                modifier {
                    // delegate -> Modifier
                    // Modifier.background() 用于设置背景颜色
                    background({
                        // delegate -> Color
                        // Color.red() 用于配置红色通道
                        red(255)
                    }) {
                        // delegate -> Shape
                        // 不配置Shape默认为矩形
                    }
                    // Modifier.absoluteOffset() 用于将内容偏移
                    absoluteOffset {
                        // delegate -> Offset
                        // Offset.x() 用于设置横坐标偏移量
                        x(-3)
                        // Offset.y() 用于设置纵坐标偏移量
                        y(-3)
                    }
                }
                // Text.text() 用于设置文本可组合项内容
                text("Text")
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