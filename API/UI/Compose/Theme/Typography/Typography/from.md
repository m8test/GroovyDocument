功能:

+ 从指定 [Typography](/API/UI/Compose/Theme/Typography/Typography/README.md) 对象复制属性

定义:

+ [Typography](/API/UI/Compose/Theme/Typography/Typography/README.md)
  from([Typography](/API/UI/Compose/Theme/Typography/Typography/README.md) typography)

参数:

+ [Typography](/API/UI/Compose/Theme/Typography/Typography/README.md) typography - 需要从哪个对象复制属性(模板对象)

返回值:

+ [Typography](/API/UI/Compose/Theme/Typography/Typography/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Typography.from()](/API/UI/Compose/Theme/Typography/Typography/README.md?id=from)
  方法从指定 [Typography](/API/UI/Compose/Theme/Typography/Typography/README.md) 对象复制属性

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def state = mutableStateOf(false)
    // Slot.MaterialTheme() 用于创建 MaterialTheme 可组合项
    MaterialTheme {
        // delegate -> MaterialTheme
        // MaterialTheme.withSingleStates() 用于设置可组合项使用到的所有 SingleState
        withSingleStates(state)
        // MaterialTheme.typography() 用于设置主题排版
        typography {
            // delegate -> Typography
            // MaterialTheme.LocalTypography() 用于获取 Typography 对应的 CompositionLocal 对象
            def LocalThemeTypography = LocalTypography()
            // MaterialTheme.compositionLocal() 用于获取 ProvidableCompositionLocal 的值
            def currentTypography = compositionLocal(LocalThemeTypography)
            // Typography.copy() 用于复制排版
            def copiedTypography = currentTypography.copy()
            // Typography.button() 用于获取主题 button 文字样式
            copiedTypography.button {
                // delegate -> TextStyle
                if (state.value()) {
                    // TextStyle.color() 用于设置文字颜色
                    color {
                        // delegate - Color
                        // Color.parse() 用于从字符串或者整数中解析颜色
                        parse("#ffff0000")
                    }
                } else {
                    // TextStyle.color() 用于设置文字颜色
                    color {
                        // delegate - Color
                        // Color.parse() 用于从字符串或者整数中解析颜色
                        parse("#ff00ff00")
                    }
                }
            }
            // Typography.from() 用于从指定 Typography 对象复制属性
            from(copiedTypography)
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
                        // Text.text() 用于设置文本可组合项内容
                        text("改变排版")
                    }
                }
                // Button.onClick() 用于处理点击事件
                onClick {
                    state.value(!state.value())
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