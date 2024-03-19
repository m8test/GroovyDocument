功能:

+ 设置文本显示方式为指定的字符

定义:

+ [VisualTransformation](/API/UI/Compose/Widget/TextField/VisualTransformation/README.md) password(String
  char)

参数:

+ String char - 需要显示的字符,如果长度超过1,只截取第一个字符

返回值:

+ [VisualTransformation](/API/UI/Compose/Widget/TextField/VisualTransformation/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [VisualTransformation.password()](/API/UI/Compose/Widget/TextField/VisualTransformation/README.md?id=password)
  方法设置文本显示方式为指定的字符

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
                value("输入框内容全显示为#")
                // TextField.visualTransformation() 用于设置输入框内容显示方式.
                visualTransformation {
                    // delegate -> VisualTransformation
                    // VisualTransformation.password() 用于设置文本显示方式为指定的字符
                    password("#")
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