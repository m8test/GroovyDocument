功能:

+ 创建[View](https://developer.android.google.cn/reference/android/view/View).

定义:

+ [AndroidView](/API/UI/Compose/Widget/AndroidView/README.md) factory(Closure closure)

参数:

+ Closure closure - 创建 [View](https://developer.android.google.cn/reference/android/view/View) 的闭包
    + 参数 - [Context](https://developer.android.google.cn/reference/android/content/Context)
    + delegate - 无
    + 返回值 - [View](https://developer.android.google.cn/reference/android/view/View).

返回值:

+ [AndroidView](/API/UI/Compose/Widget/AndroidView/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [AndroidView.factory()](/API/UI/Compose/Widget/AndroidView/README.md?id=factory)
  方法创建[View](https://developer.android.google.cn/reference/android/view/View).

```groovy
import android.widget.TextView

// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.AndroidView() 用于显示自定义View或者安卓系统提供的View
    AndroidView {
        // delegate - AndroidView
        // AndroidView.factory() 用于创建View
        factory { context ->
            def textView = new TextView(context)
            textView.setText("通过AndroidView显示的文本")
            textView
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