功能:

+ 从字符串或者整数中解析颜色.

定义:

+ [Color](/API/UI/Compose/Theme/Color/Color/README.md) parse(int|String value)

参数:

+ int|String value - 如果是int类型,四个字节分别表示ARGB,如果是String类型,格式为16进制字符串,如"#ff00ff00"

返回值:

+ [Color](/API/UI/Compose/Theme/Color/Color/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Color.parse()](/API/UI/Compose/Theme/Color/Color/README.md?id=parse) 方法从字符串或者整数中解析颜色.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Column() 用于创建 Column 可组合项
    Column {
        // delegate -> Column
        // Column.content() 用于设置 Column 可组合项中的内容
        content {
            // delegate -> Slot
            // Slot.Button() 用于创建 Button 可组合项
            Button {
                // delegate -> Button
                // Button.colors() 用于设置按钮颜色
                colors {
                    // delegate -> FilledButtonColors
                    // FilledButtonColors.contentColor() 用于设置按钮的内容颜色
                    contentColor {
                        // delegate -> Color
                        // Color.parse() 用于从字符串或者整数中解析颜色
                        parse(0xff00ff00)
                    }
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
            // Slot.Button() 用于创建 Button 可组合项
            Button {
                // delegate -> Button
                // Button.colors() 用于设置按钮颜色
                colors {
                    // delegate -> FilledButtonColors
                    // FilledButtonColors.contentColor() 用于设置按钮的内容颜色
                    contentColor {
                        // delegate -> Color
                        // Color.parse() 用于从字符串或者整数中解析颜色
                        parse("#ff00ff00")
                    }
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