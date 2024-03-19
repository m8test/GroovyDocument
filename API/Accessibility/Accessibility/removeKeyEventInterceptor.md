功能:

+ 移除按键事件拦截器

定义:

+ boolean removeKeyEventInterceptor(int interceptorId)

参数:

+ int interceptorId - 拦截器id

返回值:

+ boolean - true表示移除拦截器成功,false表示移除拦截器失败

示例代码:

+ 启动一个Activity,
  并通过 [Accessibility.removeKeyEventInterceptor()](/API/Accessibility/Accessibility/README.md?id=removeKeyEventInterceptor)
  方法移除按键事件拦截器

```groovy
// Accessibility.addKeyEventInterceptor() 用于添加按键事件拦截器
def result = $accessibility.addKeyEventInterceptor {
    // it -> KeyEvent
    // 音量下键
    if (it.getKeyCode() == it.KEYCODE_VOLUME_DOWN) {
        def message = "拦截音量下键"
        $console.log(message)
        // Toast.showShort() 用于显示短吐司
        $toast.showShort(message)
        // 返回true表示事件已经被处理(被拦截)
        true
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
                        text("removeKeyEventInterceptor")
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
            // Slot.Button() 用于创建 Button 可组合项
            Button {
                // delegate -> Button
                // Button.content() 用于设置按钮内容
                content {
                    // delegate -> Slot
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        // Text.text() 用于设置文本可组合项内容
                        text("移除按键事件拦截器")
                    }
                }
                // Button.onClick() 用于处理 Button 可组合项的点击事件
                onClick {
                    // Accessibility.removeKeyEventInterceptor() 用于移除按键事件拦截器
                    $console.log($accessibility.removeKeyEventInterceptor(result))
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