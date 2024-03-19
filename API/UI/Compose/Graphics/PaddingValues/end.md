功能:

+ 设置右边距.

定义:

+ [PaddingValues](/API/UI/Compose/Graphics/PaddingValues/README.md) end(Number end)

参数:

+ Number end - 边距,单位dp

返回值:

+ [PaddingValues](/API/UI/Compose/Graphics/PaddingValues/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [PaddingValues.end()](/API/UI/Compose/Graphics/PaddingValues/README.md?id=end) 方法设置右边距.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Button() 用于创建 Button 可组合项
    Button {
        // delegate -> Button
        // Button.contentPadding() 用于设置按钮内容边距
        contentPadding {
            // delegate -> PaddingValues
            // PaddingValues.end() 用于设置右边距
            end(20)
        }
        // Button.content() 用于设置按钮内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Button")
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