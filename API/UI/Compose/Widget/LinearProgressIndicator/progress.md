功能:

+ 设置进度条进度

定义:

+ [LinearProgressIndicator](/API/UI/Compose/Widget/LinearProgressIndicator/README.md) progress(Number
  progress)

参数:

+ Number progress - 进度,取值范围[0,1.0]

返回值:

+ [LinearProgressIndicator](/API/UI/Compose/Widget/LinearProgressIndicator/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [LinearProgressIndicator.progress()](/API/UI/Compose/Widget/LinearProgressIndicator/README.md?id=progress)
  方法设置进度条进度

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.LinearProgressIndicator() 用于创建 LinearProgressIndicator 可组合项
    LinearProgressIndicator {
        // delegate -> LinearProgressIndicator
        // LinearProgressIndicator.color() 用于设置进度条颜色
        color {
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }
        // LinearProgressIndicator.progress() 用于设置进度条进度
        progress(0.5)
        // LinearProgressIndicator.backgroundColor() 用于设置进度条背景颜色
        backgroundColor {
            // delegate -> Color
            // Color.blue() 用于配置蓝色通道
            blue(255)
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