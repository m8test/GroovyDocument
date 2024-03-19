功能:

+ 添加按键事件监听器

定义:

+ boolean addOnKeyEventListener(Closure closure)

参数:

+ Closure closure - 设置按键事件监听器的闭包,闭包将会在脚本主线程执行
    + 参数
        + [KeyEvent](https://developer.android.google.cn/reference/android/view/KeyEvent) event -
          按键事件对象
    + delegate - 无

返回值:

+ int - 成功时为监听器id,失败则为-1

示例代码:

+ 启动一个Activity,
  并通过 [Accessibility.addOnKeyEventListener()](/API/Accessibility/Accessibility/README.md?id=addOnKeyEventListener)
  方法添加按键事件监听器

```groovy
// Accessibility.addOnKeyEventListener() 用于添加按键事件监听器
def result = $accessibility.addOnKeyEventListener {
    // it -> KeyEvent
    // 音量下键
    if (it.getKeyCode() == it.KEYCODE_VOLUME_DOWN) {
        if (it.getAction() == it.ACTION_DOWN) {
            def message = "音量下按下"
            $console.log(message)
            // Toast.showShort() 用于显示短吐司
            $toast.showShort(message)
        } else if (it.getAction() == it.ACTION_UP) {
            def message = "音量下抬起"
            $console.log(message)
            // Toast.showShort() 用于显示短吐司
            $toast.showShort(message)
        }
    }
}
$console.log(result)
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newScaffoldState() 用于创建 ScaffoldState
    def state = newScaffoldState {
        // delegate -> ScaffoldState
    }
    // Slot.Scaffold() 用于创建 Scaffold 可组合项
    Scaffold {
        // delegate -> Scaffold
        // Scaffold.scaffoldState() 用于设置 ScaffoldState
        scaffoldState(state)
        // Scaffold.topBar() 用于设置顶部应用程序栏
        topBar {
            // delegate -> Slot
            // Slot.TopAppBar() 用于创建 TopAppBar 可组合项
            TopAppBar {
                // delegate -> TopAppBar
                // TopAppBar.modifier() 用于配置可组合项的 Modifier
                modifier {
                    // delegate -> Modifier
                    // Modifier.fillMaxWidth() 用于设置填充最大宽度
                    fillMaxWidth(1.0f)
                }
                // TopAppBar.title() 用于设置应用程序栏标题
                title {
                    // delegate -> Slot
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        // Text.text() 用于设置文本可组合项内容
                        text("addOnKeyEventListener")
                    }
                }
                // ScaffoldState.snackBarHost() 用于设置 SnackBarHost 可组合项
                snackBarHost { snackBarHostState ->
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
            }
        }
        // Scaffold.content() 用于设置 Scaffold 内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("开启无障碍权限后按下音量下键")
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