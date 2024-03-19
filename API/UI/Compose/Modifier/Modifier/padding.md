功能:

+ 设置内容填充

定义:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) padding(Closure closure)

参数:

+ Closure closure - 配置填充的闭包
    + 参数 - 无
    + delegate - [PaddingValues](/API/UI/Compose/Graphics/PaddingValues/README.md)

返回值:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Modifier.padding()](/API/UI/Compose/Modifier/Modifier/README.md?id=padding) 方法设置内容填充.

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
                    // Modifier.padding() 用于设置内容填充
                    padding {
                        // delegate -> PaddingValues
                        // PaddingValues.start() 用于设置左边距,单位dp
                        start(20)
                        // PaddingValues.end() 用于设置右边距,单位dp
                        end(20)
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