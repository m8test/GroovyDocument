功能:

+ 关闭悬浮窗口.

定义:

+ [FloatyWindow](/API/Floaty/FloatyWindow/README.md) close()

参数:

+ 无

返回值:

+ [FloatyWindow](/API/Floaty/FloatyWindow/README.md) - 返回对象本身方便链式调用

示例代码:

+ 显示一个悬浮窗口,通过 [FloatyWindow.close()](/API/Floaty/FloatyWindow/README.md?id=close) 方法关闭该悬浮窗口.

```groovy
// Floaty.window() 用于显示一个悬浮窗口
$floaty.window({
    // delegate -> FloatyWindowConfig
    // FloatyWindowConfig.title() 用于配置悬浮窗口的标题
    title("这是标题")
}) { floatyWindow ->
    // delegate -> Slot
    // Slot.Surface() 用于创建Surface可组合项
    Surface {
        // delegate -> Surface
        // Composable.modifier() 用于修饰 Composable,Surface 继承自 Composable
        modifier {
            // delegate -> Modifier
            // Modifier.fillMaxSize() 用于设置填充父可组合项宽度和高度, 参数为填充父可组合项的比例, 取值区间为 0.0f-1.0f
            fillMaxSize(1.0f)
        }
        // Surface.content() 用于设置 Surface 可组合项的内容
        content {
            // delegate -> Slot
            // Slot.Column() 用于创建 Column 可组合项
            Column {
                // delegate -> Column
                // Column.content() 用于设置 Column 可组合项中的内容
                content {
                    // delegate -> Slot
                    // Slot.Button() 用于创建 Button 可组合项
                    Button {
                        // delegate-> Button
                        // Button.content() 用于设置 Button 可组合项中的内容
                        content {
                            // delegate -> Slot
                            // Slot.Text() 用于创建 Text 可组合项
                            Text {
                                // delegate -> Text
                                // Text.text() 用于设置 Text 可组合项的文本内容
                                text('关闭悬浮窗')
                            }
                        }
                        // Button.onClick() 用于处理 Button 可组合项的点击事件
                        onClick {
                            // FloatyWindow.close() 用于关闭悬浮窗口
                            floatyWindow.close()
                        }
                    }
                }
            }
        }
    }
}
```