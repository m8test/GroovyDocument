功能:

+ 创建一个用给定颜色均匀分布在中心周围扫描渐变的刷子。扫描相对于 3 点钟方向开始，然后顺时针方向继续，直到再次到达起始位置。.

定义:

+ [Brush](/API/UI/Compose/Graphics/Brush/README.md) sweepGradient(List\<Closure\> colors, Closure center)

参数:

+ List\<Closure\> colors - 作为渐变的一部分呈现的颜色
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)
+ Closure center - 扫描渐变圆的中心位置
    + 参数 - 无
    + delegate - [Offset](/API/UI/Compose/Graphics/Offset/README.md)

返回值:

+ [Brush](/API/UI/Compose/Graphics/Brush/README.md) - 新创建的刷子对象

示例代码:

+ 启动一个Activity, 并通过 [Brushes.sweepGradient()](/API/UI/Compose/Graphics/Brushes/README.md?id=sweepGradient)
  方法创建一个用给定颜色均匀分布在中心周围扫描渐变的刷子.

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
            // Brushes.sweepGradient() 用于创建一个用给定颜色均匀分布在中心周围扫描渐变的刷子
            def myBrush = $brushes.sweepGradient([
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
                x(50)
                // DpOffset.y() 用于设置纵坐标偏移量
                y(50)
            })
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