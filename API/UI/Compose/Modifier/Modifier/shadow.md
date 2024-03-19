功能:

+ 设置阴影

定义:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) shadow(Number elevation, Closure shape, boolean
  clip, Closure ambientColor, Closure
  spotColor)

参数:

+ Number elevation - 阴影的高度,单位dp
+ Closure shape - 定义物理对象的形状
    + 参数 - 无
    + delegate - [Shape](/API/UI/Compose/Theme/Shape/Shape/README.md)
+ boolean clip - 激活时,内容绘图会剪裁到形状
+ Closure ambientColor - 设置环境色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)
+ Closure spotColor - 设置专色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Modifier.shadow()](/API/UI/Compose/Modifier/Modifier/README.md?id=shadow) 方法设置阴影

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
                    // Modifier.shadow() 用于设置阴影
                    shadow(20, {
                        // delegate -> Shape
                        // Shape.all() 用于设置四个角尺寸
                        all(10, "dp")
                        // Shape.roundedCorner() 用于设置角的类型为圆角
                        roundedCorner()
                    }, true, {
                        // delegate -> Color
                        // Color.red() 用于配置红色通道
                        red(255)
                    }, {
                        // delegate -> Color
                        // Color.blue() 用于配置蓝色通道
                        blue(255)
                    })
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