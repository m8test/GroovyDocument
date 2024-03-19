功能:

+ 设置应用程序栏的海拔.

定义:

+ [AppBar](/API/UI/Compose/Widget/AppBar/README.md) elevation(Number elevation)

参数:

+ Number elevation - 需要设置的海拔,单位dp

返回值:

+ [AppBar](/API/UI/Compose/Widget/AppBar/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [AppBar.elevation()](/API/UI/Compose/Widget/AppBar/README.md?id=elevation) 方法设置应用程序栏海拔.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.BottomAppBar() 用于创建 BottomAppBar 可组合项
    BottomAppBar {
        // delegate -> BottomAppBar
        // BottomAppBar.elevation() 用于设置应用程序栏海拔
        elevation(24)
        // BottomAppBar.modifier() 用于配置可组合项的 Modifier
        modifier {
            // delegate -> Modifier
            // Modifier.fillMaxWidth() 用于设置填充最大宽度
            fillMaxWidth(1.0f)
        }
        // BottomAppBar.content() 用于设置应用程序栏内容
        content {
            // delegate -> Slot
            // Modifier -> RowScopeModifier
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Item1")
                // Text.modifier() 用于配置可组合项的 Modifier
                modifier {
                    // delegate -> RowScopeModifier
                    // RowScopeModifier.weight() 用于配置权重
                    weight(1.0f)
                }
            }
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Item2")
                // Text.modifier() 用于配置可组合项的 Modifier
                modifier {
                    // delegate -> RowScopeModifier
                    // RowScopeModifier.weight() 用于配置权重
                    weight(1.0f)
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