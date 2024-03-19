功能:

+ 设置主题排版.

定义:

+ [MaterialTheme](/API/UI/Compose/Widget/MaterialTheme/README.md) typography(Closure closure)

参数:

+ Closure closure - 设置排版的闭包
    + 参数 - 无
    + delegate - [Typography](/API/UI/Compose/Theme/Typography/Typography/README.md)

返回值:

+ [MaterialTheme](/API/UI/Compose/Widget/MaterialTheme/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [MaterialTheme.typography()](/API/UI/Compose/Widget/MaterialTheme/README.md?id=typography) 方法设置主题排版.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.MaterialTheme() 用于创建 MaterialTheme 可组合项
    MaterialTheme {
        // delegate -> MaterialTheme
        // MaterialTheme.typography() 用于设置主题排版
        typography {
            // delegate -> Typography
            // Typography.body1() 用于设置 body1 排版
            body1 {
                // delegate -> TextStyle
                // TextStyle.fontSize() 用于设置字体大小
                fontSize(20, "sp")
            }
        }
        // MaterialTheme.content() 用于设置主题内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.LocalTypography() 用于获取 Typography 对应的 CompositionLocal 对象
                def LocalThemeTypography = LocalTypography()
                // Text.compositionLocal() 用于获取 ProvidableCompositionLocal 的值
                def currentTypography = compositionLocal(LocalThemeTypography)
                // Typography.body1() 用于获取主题 body1 排版
                def body1TextStyle = currentTypography.body1()
                // Text.style() 用于配置文本样式
                style {
                    // delegate -> TextStyle
                    // TextStyle.from() 用于从指定 TextStyle 对象复制属性
                    from(body1TextStyle)
                }
                // Text.text() 用于设置文本可组合项内容
                text("MaterialTheme")
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