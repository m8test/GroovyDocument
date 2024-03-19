功能:

+ 获取安卓[Activity](https://developer.android.google.cn/reference/android/app/Activity)对象

定义:

+ [Activity](/API/UI/Activity/Activity/README.md) androidActivity()

参数:

+ 无

返回值:

+ [Activity](/API/UI/Activity/Activity/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 通过 [Activity.androidActivity()](/API/UI/Activity/Activity/README.md?id=androidActivity)
  方法获取安卓[Activity](https://developer.android.google.cn/reference/android/app/Activity)对象

```groovy
import android.app.Activity

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
// Activity.onCreate() 方法用于监听Activity创建
$composeActivity.onCreate {
    // Activity.androidActivity() 用于获取安卓Activity对象
    def aa = $composeActivity.androidActivity()
    $assert.assertTrue(aa instanceof Activity, "Android Activity子类对象")
}
// Activity.onDestroy() 方法用于监听Activity销毁
$composeActivity.onDestroy {
    // Script.stop() 方法用于停止脚本
    $script.stop()
}
// Activity.start() 用于启动Android系统的Activity
$composeActivity.start()
```