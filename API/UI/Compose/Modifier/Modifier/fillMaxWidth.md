功能:

+ 设置宽度填充比例

定义:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) fillMaxWidth(float fraction)

参数:

+ float fraction - 要使用的最大宽度的分数，取值范围[0.0-1.0]

返回值:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Modifier.fillMaxWidth()](/API/UI/Compose/Modifier/Modifier/README.md?id=fillMaxWidth)
  方法设置宽度填充比例

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
                    // Modifier.fillMaxWidth() 用于设置宽度填充比例
                    fillMaxWidth(0.5f)
                    // Modifier.background() 用于设置背景颜色
                    background({
                        // delegate -> Color
                        // Color.red() 用于配置红色通道
                        red(255)
                    }) {
                        // delegate -> Shape
                        // Shape.all() 用于设置四个角尺寸
                        all(5, "dp")
                        // Shape.roundedCorner() 用于设置角的类型为圆角
                        roundedCorner()
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