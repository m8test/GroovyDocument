功能:

+ 设置文本显示方式为文本

定义:

+ [VisualTransformation](/API/UI/Compose/Widget/TextField/VisualTransformation/README.md) text()

参数:

+ 无

返回值:

+ [VisualTransformation](/API/UI/Compose/Widget/TextField/VisualTransformation/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [VisualTransformation.text()](/API/UI/Compose/Widget/TextField/VisualTransformation/README.md?id=text)
  方法设置文本显示方式为文本

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Column() 用于创建纵向布局
    Column {
        // delegate -> Column
        // Column.content() 用于设置布局内容
        content {
            // delegate -> Slot
            // Slot.mutableStateOf() 用于创建一个 MutableState 对象
            def state = mutableStateOf(false)
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
                        text("显示/隐藏文本")
                    }
                }
                // Button.onClick() 用于处理点击事件
                onClick {
                    state.value(!state.value())
                }
            }
            // Slot.TextField() 用于创建 TextField 可组合项
            TextField {
                // delegate -> TextField
                // TextField.value() 用于设置输入框内容
                value("输入框内容全显示为#")
                // TextField.withSingleStates() 用于设置可组合项使用到的所有 SingleState
                withSingleStates(state)
                // TextField.visualTransformation() 用于设置输入框内容显示方式.
                visualTransformation {
                    // delegate -> VisualTransformation
                    if (state.value()) {
                        // VisualTransformation.password() 用于设置文本显示方式为指定的字符
                        password("#")
                    } else {
                        // VisualTransformation.text() 用于设置文本显示方式为文本
                        text()
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