功能:

+ 启动Android系统的[Activity](https://developer.android.google.cn/reference/android/app/Activity)

定义:

+ [Activity](/API/UI/Activity/Activity/README.md) start()

参数:

+ 无

返回值:

+ [Activity](/API/UI/Activity/Activity/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 通过 [Activity.start()](/API/UI/Activity/Activity/README.md?id=start)
  方法启动Android系统的[Activity](https://developer.android.google.cn/reference/android/app/Activity)

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
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("text")
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