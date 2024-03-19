功能:

+ 从指定 [Colors](/API/UI/Compose/Theme/Color/Colors/README.md) 对象复制属性

定义:

+ [Colors](/API/UI/Compose/Theme/Color/Colors/README.md) from([Colors](/API/UI/Compose/Theme/Color/Colors/README.md)
  colors)

参数:

+ [Colors](/API/UI/Compose/Theme/Color/Colors/README.md) colors - 需要从哪个对象复制属性(模板对象)

返回值:

+ [Colors](/API/UI/Compose/Theme/Color/Colors/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Colors.from()](/API/UI/Compose/Theme/Color/Colors/README.md?id=from)
  方法从指定 [Colors](/API/UI/Compose/Theme/Color/Colors/README.md) 对象复制属性

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
        // MaterialTheme.colors() 用于设置主题颜色
        colors {
            // delegate -> Colors
            // MaterialTheme.LocalColors() 用于获取 Colors 对应的 CompositionLocal 对象
            def LocalThemeColors = LocalColors()
            // MaterialTheme.compositionLocal() 用于获取 ProvidableCompositionLocal 的值
            def currentColors = compositionLocal(LocalThemeColors)
            // Colors.copy() 用于复制颜色
            def copiedColors = currentColors.copy()
            // Colors.isLight() 用于设置颜色是否为亮色
            isLight(state.value())
            // Colors.primary() 用于设置 primary 颜色
            copiedColors.primary {
                // delegate -> Color
                if (state.value()) {
                    // Color.parse() 用于从字符串或者整数中解析颜色
                    parse(0xff00ff00)
                } else {
                    // Color.parse() 用于从字符串或者整数中解析颜色
                    parse(0xffff0000)
                }
            }
            // Colors.from() 用于从指定 Colors 对象复制属性
            from(copiedColors)
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
                        text("暗色/亮色")
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