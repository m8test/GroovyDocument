功能:

+ 设置右上角尺寸.

定义:

+ [Shape](/API/UI/Compose/Theme/Shape/Shape/README.md) topRight(Number size, String unit)

参数:

+ Number size - 需要设置的尺寸大小
+ String unit - 尺寸单位,可选值有 dp 和 percent

返回值:

+ [Shape](/API/UI/Compose/Theme/Shape/Shape/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Shape.topRight()](/API/UI/Compose/Theme/Shape/Shape/README.md?id=topRight) 方法设置右上角尺寸.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Button() 用于创建 Button 可组合项
    Button {
        // delegate -> Button
        // Button.shape() 用于设置按钮形状
        shape {
            // delegate -> Shape
            // Shape.topRight() 用于设置右上角尺寸
            topRight(20, "dp")
            // Shape.roundedCorner() 用于设置角的类型为圆角
            roundedCorner()
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