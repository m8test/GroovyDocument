功能:

+ 创建一个用给定的颜色均匀分布在渐变中的水平渐变刷子.

定义:

+ [Brush](/API/UI/Compose/Graphics/Brush/README.md) horizontalGradient(List\<Closure\> colors, Number
  startX, Number endX, String tileMode)

参数:

+ List\<Closure\> colors - 作为渐变的一部分呈现的颜色
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)
+ Number startX - 水平渐变的起始 x 位置
+ Number endX - 水平渐变的结束 x 位置
+ String tileMode - 确定着色器如何填充其边界外区域的行为, 可选值有
    + Clamp - 边缘被固定到最终颜色。渐变将使用最接近该区域的点的颜色绘制内部区域之外的所有区域。
    + Repeated - 边缘从第一种颜色重复到最后一种。这就好像从 0.0 到 1.0 的停止点然后从 1.0 到 2.0、2.0 到 3.0 等等重复（对于线性渐变，类似地从 -1.0 到
      0.0、-2.0 到 -1.0 等）。
    + Mirror - 边缘从最后一种颜色镜像到第一种颜色。 这就好像停止点从 0.0 到 1.0 然后从 2.0 向后重复到 1.0，然后从 2.0 向前重复到 3.0，然后再从 4.0
      向后重复到 3.0，依此类推（对于线性梯度，类似地从负
    + Decal - 仅在其原始边界内渲染着色器的图像像素。 如果着色器在其原始边界之外绘制，则会绘制透明黑色。

返回值:

+ [Brush](/API/UI/Compose/Graphics/Brush/README.md) - 新创建的刷子对象

示例代码:

+ 启动一个Activity,
  并通过 [Brushes.horizontalGradient()](/API/UI/Compose/Graphics/Brushes/README.md?id=horizontalGradient)
  方法创建一个用给定的颜色均匀分布在渐变中的水平渐变刷子.

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
            // Brushes.horizontalGradient() 用于创建一个用给定的颜色均匀分布在渐变中的水平渐变刷子
            def myBrush = $brushes.horizontalGradient([
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
            ], 10, 20, "Repeated")
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