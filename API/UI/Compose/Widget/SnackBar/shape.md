功能:

+ 设置 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md) 形状

定义:

+ [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md) shape(Closure closure)

参数:

+ Closure closure - 设置形状的闭包
    + 参数 - 无
    + delegate - [Shape](/API/UI/Compose/Theme/Shape/Shape/README.md)

返回值:

+ [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [SnackBar.shape()](/API/UI/Compose/Widget/SnackBar/README.md?id=shape)
  方法设置 [SnackBar](/API/UI/Compose/Widget/SnackBar/README.md) 形状

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
            snackBarHostState.showSnackBar("圆角SnackBar", "取消", "Short")
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
                // SnackBar.shape() 用于设置 SnackBar 形状
                shape {
                    // delegate -> Shape
                    // Shape.all() 用于设置四个角尺寸
                    all(50, "dp")
                    // Shape.roundedCorner() 用于设置角的类型为圆角
                    roundedCorner()
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