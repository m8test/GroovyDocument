功能:

+ 设置输入法动作,由键盘执行,并可能在键盘上显示特定图标.

定义:

+ [KeyboardOptions](/API/UI/Compose/Widget/TextField/KeyboardOptions/README.md) imeAction(String action)

参数:

+ String action - 输入法动作,可选值如下
    + Default - 使用平台和键盘默认值，让键盘决定操作。
    + None - 表示不需要从键盘执行任何操作
    + Go - 表示用户希望转到输入框中文本的目标,即访问URL
    + Search - 表示用户要执行搜索,即web搜索查询。
    + Done - 表示用户已完成向一组输入提供输入。现在应该发生某种最终确定行为，即字段是组中的最后一个元素，数据输入已最终确定。
    + Previous - 表示用户希望返回到上一个输入,即返回到表单中的上一个字段。
    + Next - 表示用户已完成当前输入,并希望移动到下一个输入,即移动到表单中的下一个字段。
    + Send - 表示用户希望发送输入框中的文本,即SMS。

返回值:

+ [KeyboardOptions](/API/UI/Compose/Widget/TextField/KeyboardOptions/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [KeyboardOptions.imeAction()](/API/UI/Compose/Widget/TextField/KeyboardOptions/README.md?id=imeAction)
  方法设置输入法动作.

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
            // Slot.TextField() 用于创建 TextField 可组合项
            TextField {
                // delegate -> TextField
                // TextField.value() 用于设置输入框内容
                value("content")
                // TextField.keyboardActions() 用于设置输入法动作(IME Action)响应事件
                keyboardActions {
                    // delegate -> KeyboardActions
                    // KeyboardActions.onDone() 用于设置输入法完成动作响应事件
                    onDone {
                        $console.log("onDone")
                    }
                }
                // TextField.keyboardOptions() 用于设置输入框键盘配置选项
                keyboardOptions {
                    // delegate -> KeyboardOptions
                    // KeyboardOptions.imeAction() 用于设置输入法动作
                    imeAction("Done")
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