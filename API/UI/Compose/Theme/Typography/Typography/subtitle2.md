功能1:

+ 设置主题 subtitle2 文字样式

定义1:

+ [Typography](/API/UI/Compose/Theme/Typography/Typography/README.md) subtitle2(Closure closure)

参数1:

+ Closure closure - 设置文字样式的闭包
    + 参数 - 无
    + delegate - [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md)

返回值1:

+ [Typography](/API/UI/Compose/Theme/Typography/Typography/README.md) - 返回对象本身方便链式调用

功能2:

+ 获取主题 subtitle2 文字样式

定义2:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) subtitle2()

参数2:

+ 无

返回值2:

+ [TextStyle](/API/UI/Compose/Theme/Typography/TextStyle/README.md) - subtitle2 文字样式对象

示例代码:

+ 启动一个Activity,
  并通过 [Typography.subtitle2()](/API/UI/Compose/Theme/Typography/Typography/README.md?id=subtitle2)
  方法设置/获取主题 subtitle2 文字样式

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.MaterialTheme() 用于创建 MaterialTheme 可组合项
    MaterialTheme {
        // delegate -> MaterialTheme
        // MaterialTheme.typography() 用于设置主题文字样式
        typography {
            // delegate -> Typography
            // Typography.subtitle2() 用于设置主题 subtitle2 文字样式
            subtitle2 {
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
                        // Typography.subtitle2() 用于获取主题 subtitle2 文字样式
                        def subtitle2TextStyle = currentTypography.subtitle2()
                        // Text.style() 用于设置文字样式
                        style {
                            // delegate -> TextStyle
                            // TextStyle.from() 用于从指定 TextStyle 对象复制属性
                            from(subtitle2TextStyle)
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