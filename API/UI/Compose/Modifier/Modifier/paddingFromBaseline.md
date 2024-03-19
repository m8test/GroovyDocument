功能:

+ 设置内容填充

定义1:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) paddingFromBaseline(Number top, Number bottom)

参数1:

+ Number top - 从布局顶部到内容中第一行文本基线的距离
+ Number bottom - 从内容中最后一行文本的基线到布局底部的距离

返回值:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [Modifier.paddingFromBaseline()](/API/UI/Compose/Modifier/Modifier/README.md?id=paddingFromBaseline)
  方法设置内容填充.

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
                    // Modifier.paddingFromBaseline() 用于设置内容填充
                    paddingFromBaseline(20, 20)
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