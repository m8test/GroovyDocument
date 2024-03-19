功能:

+ 更新悬浮窗位置.

定义:

+ [FloatyWindow](/API/Floaty/FloatyWindow/README.md) position(int x, int y)

参数:

+ int x - x方向偏移量
+ int y - y方向偏移量

返回值:

+ [FloatyWindow](/API/Floaty/FloatyWindow/README.md) - 返回对象本身方便链式调用

示例代码:

+ 显示一个悬浮窗口并通过 [FloatyWindow.position()](/API/Floaty/FloatyWindow/README.md?id=position) 左/右移动悬浮窗口.

```groovy
def MyButton = { floatyWindow, buttonText, buttonOnClick ->
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
                text(buttonText)
            }
        }
        // Button.onClick() 用于处理 Button 可组合项的点击事件
        onClick {
            buttonOnClick()
        }
    }
}

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
                    // FloatyWindow.config() 用于获取悬浮窗对应的 FloatyWindowConfig 对象
                    def config = floatyWindow.config()
                    // FloatyWindowConfig.params() 用于获取悬浮窗布局参数(LayoutParams)
                    def layoutParams = config.params()
                    MyButton.delegate = delegate
                    MyButton(floatyWindow, "左移") {
                        // FloatWindow.position() 用于更新悬浮窗位置
                        floatyWindow.position(layoutParams.x - 50, layoutParams.y)
                    }
                    MyButton(floatyWindow, "右移") {
                        // FloatWindow.position() 用于更新悬浮窗位置
                        floatyWindow.position(layoutParams.x + 50, layoutParams.y)
                    }
                }
            }
        }
    }
}
```