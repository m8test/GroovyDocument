功能:

+ 创建 [MaterialTheme](/API/UI/Compose/Widget/MaterialTheme/README.md) 可组合项

定义:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) MaterialTheme(Closure closure)

参数:

+ Closure closure - 设置 [MaterialTheme](/API/UI/Compose/Widget/MaterialTheme/README.md) 的闭包
    + 参数 - 无
    + delegate - [MaterialTheme](/API/UI/Compose/Widget/MaterialTheme/README.md)

返回值:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Slot.MaterialTheme()](/API/UI/Compose/Slot/Slot/README.md?id=MaterialTheme)
  方法创建 [MaterialTheme](/API/UI/Compose/Widget/MaterialTheme/README.md) 可组合项

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.MaterialTheme() 用于创建 MaterialTheme 可组合项
    MaterialTheme {
        // delegate -> MaterialTheme
        // MaterialTheme.colors() 用于设置主题颜色
        colors {
            // delegate -> Colors
            // Colors.primary() 用于设置主要颜色
            primary {
                // delegate -> Color
                // Color.red() 用于配置红色通道
                red(255)
            }
        }
        // MaterialTheme.content() 用于设置主题内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.LocalColors() 用于获取 Colors 对应的 CompositionLocal 对象
                def LocalThemeColors = LocalColors()
                // Text.compositionLocal() 用于获取 ProvidableCompositionLocal 的值
                def currentColors = compositionLocal(LocalThemeColors)
                // Colors.primary() 用于获取主要颜色
                def primaryColor = currentColors.primary()
                // Text.style() 用于配置文本样式
                style {
                    // delegate -> TextStyle
                    // TextStyle.color() 用于设置文字颜色
                    color {
                        // delegate -> Color
                        // Color.from() 用于从指定 Color 对象复制属性(ARGB)
                        from(primaryColor)
                    }
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