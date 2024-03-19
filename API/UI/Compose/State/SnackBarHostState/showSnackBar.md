功能:

+ 显示 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md)

定义:

+ [Deferred](/API/Coroutines/Deferred/README.md) showSnackBar(String message, String actionLabel,
  String duration)

参数:

+ String message - 要在 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md) 中显示的文本
+ String actionLabel - 要显示在 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md) 上的动作按钮,如果不需要动作按钮可为null
+ String duration - [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md) 显示的时长,可选值有:
    + Short - 在短时间内展示 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md)
    + Long - 长时间展示 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md)
    + Indefinite - 无限期显示 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md) ,直到明确取消或单击操作

返回值:

+ [Deferred](/API/Coroutines/Deferred/README.md) - 可获取协程执行结果的对象,结果为 String 类型,可选值有
    + Dismissed - 显示的 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md) 已被用户通过超时或关闭
    + ActionPerformed - 在超时之前，已单击 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md) 上的操作

示例代码:

+ 启动一个Activity,
  并通过 [SnackBarHostState.showSnackBar()](/API/UI/Compose/State/SnackBarHostState/README.md?id=showSnackBar)
  方法显示 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md)

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newSnackBarHostState() 用于创建 SnackBarHostState
    def snackBarHostState = newSnackBarHostState {
        // delegate -> SnackBarHostState
    }
    // Slot.TextButton() 用于设置文本按钮
    TextButton {
        // delegate -> TextButton
        // TextButton.content() 用于设置按钮内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("显示SnackBar")
            }
        }
        // TextButton.onClick() 用于处理点击事件
        onClick {
            // SnackBarHostState.showSnackBar() 用于显示 SnackBar
            snackBarHostState.showSnackBar("测试SnackBar", "取消", "Indefinite")
        }
    }
    // delegate -> Slot
    // Slot.SnackBarHost() 用于创建 SnackBarHost 可组合项
    SnackBarHost {
        // delegate -> SnackBarHost
        // SnackBarHost.hostState() 用于设置 SnackBarHostState
        hostState(snackBarHostState)
        // SnackBarHost.snackBar() 用于设置 SnackBar 可组合项
        snackBar { data ->
            // delegate -> Slot
            // Slot.SnackBar() 用于创建 SnackBar 可组合项
            SnackBar {
                // delegate -> SnackBar
                // SnackBar.snackBarData() 用于设置 SnackBarData
                snackBarData(data)
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