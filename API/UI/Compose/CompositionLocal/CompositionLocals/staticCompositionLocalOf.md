功能:

+ 创建 [StaticProvidableCompositionLocal](
  /API/UI/Compose/CompositionLocal/StaticProvidableCompositionLocal/README.md) 对象

定义:

+ [StaticProvidableCompositionLocal](/API/UI/Compose/CompositionLocal/StaticProvidableCompositionLocal/README.md)
  staticCompositionLocalOf(Closure closure)

参数:

+ Closure closure - 获取默认值的闭包
    + 参数 - 无
    + delegate - 无
    + 返回值 - Object

返回值:

+ [StaticProvidableCompositionLocal](
  /API/UI/Compose/CompositionLocal/StaticProvidableCompositionLocal/README.md) -
  新创建的 [StaticProvidableCompositionLocal](
  /API/UI/Compose/CompositionLocal/StaticProvidableCompositionLocal/README.md) 对象

示例代码:

+ 启动一个Activity,
  并通过 [CompositionLocals.staticCompositionLocalOf()](/API/UI/Compose/CompositionLocal/CompositionLocals/README.md?id=staticCompositionLocalOf)
  方法将 [CompositionLocal](/API/UI/Compose/CompositionLocal/CompositionLocal/README.md) 键与值相关联

```groovy
// CompositionLocals.compositionLocalOf() 用于创建 DynamicProvidableCompositionLocal 对象
def LocalDynamicText = $compositionLocals.compositionLocalOf { "Dynamic" }
// CompositionLocals.staticCompositionLocalOf() 用于创建 StaticProvidableCompositionLocal 对象
def LocalStaticText = $compositionLocals.staticCompositionLocalOf { "Static" }
def testText = "initialize"
def MyDynamicColumn = {
    // delegate -> Slot
    // Slot.Column() 用于创建 Column 可组合项
    Column {
        // delegate -> Column
        // Column.content() 用于设置 Column 内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text(testText)
            }
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.compositionLocal() 用于获取 ProvidableCompositionLocal 的值
                def currentText = compositionLocal(LocalDynamicText)
                // Text.text() 用于设置文本可组合项内容
                text(currentText.value())
            }
        }
    }
}
def MyStaticColumn = {
    // delegate -> Slot
    // Slot.Column() 用于创建 Column 可组合项
    Column {
        // delegate -> Column
        // Column.content() 用于设置 Column 内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text(testText)
            }
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.compositionLocal() 用于获取 ProvidableCompositionLocal 的值
                def currentText = compositionLocal(LocalStaticText)
                // Text.text() 用于设置文本可组合项内容
                text(currentText.value())
            }
        }
    }
}
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def state = mutableStateOf("默认值")
    // Slot.Column() 用于创建 Column 可组合项
    Column {
        // delegate -> Column
        // Column.content() 用于设置 Column 内容
        content {
            // delegate -> Slot
            // Slot.CompositionLocalProvider() 用于创建 CompositionLocalProvider 可组合项
            CompositionLocalProvider {
                // delegate -> CompositionLocalProvider
                // ProvidableCompositionLocal.provides() 用于将 CompositionLocal 键与值相关联
                def providedValue = LocalDynamicText.provides(state)
                // CompositionLocalProvider.values() 用于设置 ProvidedValue
                values([providedValue])
                // CompositionLocalProvider.content() 用于设置 CompositionLocalProvider 内容
                content {
                    // delegate -> Slot
                    MyDynamicColumn.delegate = delegate
                    MyDynamicColumn()
                }
            }
            // Slot.CompositionLocalProvider() 用于创建 CompositionLocalProvider 可组合项
            CompositionLocalProvider {
                // delegate -> CompositionLocalProvider
                // ProvidableCompositionLocal.provides() 用于将 CompositionLocal 键与值相关联
                def providedValue = LocalStaticText.provides(state)
                // CompositionLocalProvider.values() 用于设置 ProvidedValue
                values([providedValue])
                // CompositionLocalProvider.content() 用于设置 CompositionLocalProvider 内容
                content {
                    // delegate -> Slot
                    MyStaticColumn.delegate = delegate
                    MyStaticColumn()
                }
            }
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
                        text("更新")
                    }
                }
                // Button.onClick() 用于处理点击事件
                onClick {
                    testText = "update"
                    state.value("更新值")
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