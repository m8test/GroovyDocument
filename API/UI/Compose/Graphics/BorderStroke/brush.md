功能:

+ 设置边框刷子.

定义:

+ [BorderStroke](/API/UI/Compose/Graphics/BorderStroke/README.md)
  brush([Brush](/API/UI/Compose/Graphics/Brush/README.md) brush)

参数:

+ [Brush](/API/UI/Compose/Graphics/Brush/README.md) brush - 需要设置的刷子

返回值:

+ [BorderStroke](/API/UI/Compose/Graphics/BorderStroke/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [BorderStroke.brush()](/API/UI/Compose/Graphics/BorderStroke/README.md?id=brush)
  方法设置边框刷子.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Button() 用于创建 Button 可组合项
    Button {
        // delegate -> Button
        // Button.border() 用于设置按钮边框
        border {
            // delegate -> BorderStroke
            // BorderStroke.width() 用于设置边框宽度
            width(5)
            // Brushes.linearGradient() 用于创建沿给定的开始和结束坐标使用提供的颜色创建线性渐变的刷子
            def myBrush = $brushes.linearGradient([
                    {
                        // delegate -> Color
                        // Color.red() 用于配置红色通道
                        red(255)
                    },
                    {
                        // delegate -> Color
                        // Color.green() 用于配置绿色通道
                        green(255)
                    },
                    {
                        // delegate -> Color
                        // Color.blue() 用于配置蓝色通道
                        blue(255)
                    },
            ], {
                // delegate -> Offset
                // DpOffset.x() 用于设置横坐标偏移量
                x(0)
                // DpOffset.y() 用于设置纵坐标偏移量
                y(50)
            }, {
                // delegate -> Offset
                // DpOffset.x() 用于设置横坐标偏移量
                x(0)
                // DpOffset.y() 用于设置纵坐标偏移量
                y(100)
            }, "Repeated")
            // BorderStroke.brush() 用于设置边框刷子
            brush(myBrush)
        }
        // Button.content() 用于设置按钮内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Button")
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