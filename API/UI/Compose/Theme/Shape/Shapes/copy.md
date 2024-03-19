功能:

+ 复制形状.

定义:

+ [Shapes](/API/UI/Compose/Theme/Shape/Shapes/README.md) copy()

参数:

+ 无

返回值:

+ [Shapes](/API/UI/Compose/Theme/Shape/Shapes/README.md) -
  新复制的 [Shapes](/API/UI/Compose/Theme/Shape/Shapes/README.md) 对象

示例代码:

+ 启动一个Activity, 并通过 [Shapes.copy()](/API/UI/Compose/Theme/Shape/Shapes/README.md?id=copy) 方法复制形状.

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
        // MaterialTheme.shapes() 用于设置主题形状
        shapes {
            // delegate -> Shapes
            // MaterialTheme.LocalShapes() 用于获取 Shapes 对应的 CompositionLocal 对象
            def LocalThemeShapes = LocalShapes()
            // MaterialTheme.compositionLocal() 用于获取 ProvidableCompositionLocal 的值
            def currentShapes = compositionLocal(LocalThemeShapes)
            // Shapes.copy() 用于复制形状
            def copiedShapes = currentShapes.copy()
            // Shapes.small() 用于设置 small 形状
            copiedShapes.small {
                // delegate -> Shape
                if (state.value()) {
                    // Shape.all() 用于设置四个角尺寸
                    all(20, "dp")
                } else {
                    // Shape.all() 用于设置四个角尺寸
                    all(5, "dp")
                }
            }
            // Shapes.from() 用于从指定 Shapes 对象复制属性
            from(copiedShapes)
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
                        text("改变形状")
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