功能:

+ 从指定 [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) 对象复制属性

定义:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md)
  from([TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) style)

参数:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) style - 需要从哪个对象复制属性(模板对象)

返回值:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [TextStyle.from()](/API/UI/Compose/Theme/Typography/TextStyle/README.md?id=from)
  方法从指定 [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) 对象复制属性

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.MaterialTheme() 用于创建 MaterialTheme 可组合项
    MaterialTheme {
        // delegate -> MaterialTheme
        // MaterialTheme.typography() 用于设置主题字体样式
        typography {
            // delegate -> Typography
            // Typography.body1() 用于设置主题 body1 字体样式
            body1 {
                // delegate -> TextStyle
                // TextStyle.color() 用于设置文字颜色
                color {
                    // delegate - Color
                    // Color.parse() 用于从字符串或者整数中解析颜色
                    parse("#ffff0000")
                }
            }
        }
        // MaterialTheme.content() 用于设置主题内容
        content {
            // delegate -> Slot
            // Slot.Button() 用于创建 Button 可组合项
            Button {
                // delegate -> Button
                // Button.content() 用于设置按钮内容
                content {
                    // delegate -> Slot
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        // Text.LocalTypography() 用于获取 Typography 对应的 CompositionLocal 对象
                        def LocalThemeTypography = LocalTypography()
                        // Text.compositionLocal() 用于获取 ProvidableCompositionLocal 的值
                        def currentTypography = compositionLocal(LocalThemeTypography)
                        // Typography.body1() 用于获取主题 body1 字体样式
                        def body1TextStyle = currentTypography.body1()
                        // TextStyle.copy() 用于复制字体样式
                        def copiedBody1TextStyle = body1TextStyle.copy()
                        // TextStyle.color() 用于设置文字颜色
                        copiedBody1TextStyle.color {
                            // delegate - Color
                            // Color.parse() 用于从字符串或者整数中解析颜色
                            parse("#ff00ff00")
                        }
                        // Text.style() 用于设置字体样式
                        style {
                            // delegate -> TextStyle
                            // TextStyle.from() 用于从指定 TextStyle 对象复制属性
                            from(copiedBody1TextStyle)
                        }
                        // Text.text() 用于设置文本可组合项内容
                        text("MaterialTheme")
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