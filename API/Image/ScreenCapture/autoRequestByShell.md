功能:

+ 设置是否自动通过 Shell 授予截屏权限

定义:

+ [ScreenCapture](/API/Image/ScreenCapture/README.md) autoRequestByShell(boolean autoRequestByShell)

参数:

+ boolean autoRequestByShell - true表示自动通过 Shell 授予截图权限,false表示不通过 Shell 授予截图权限

返回值:

+ [ScreenCapture](/API/Image/ScreenCapture/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [ScreenCapture.autoRequestByShell()](/API/Image/ScreenCapture/README.md?id=autoRequestByShell)
  方法设置是否自动通过 Shell 授予截屏权限

```groovy
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
                        text("autoRequestByShell")
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
                // TopAppBar.actions() 用于设置应用程序栏的右边动作按钮
                actions {
                    // delegate -> Slot
                    // Slot.IconButton() 用于创建 IconButton 可组合项
                    IconButton {
                        // delegate -> IconButton
                        // IconButton.content() 用于设置图标按钮内容
                        content {
                            // delegate -> Slot
                            // Slot.Icon() 用于创建 Icon 可组合项
                            Icon {
                                // delegate -> Icon
                                // Icon.contentDescription() 用于设置图标内容描述
                                contentDescription("运行")
                                // Icon.vector() 用于设置图标矢量图
                                vector("Filled", "PlayArrow")
                            }
                        }
                        // IconButton.onClick() 用于设置图标按钮点击事件
                        onClick {
                            // 开启一个子线程不指定线程名
                            $threads.startThread {
                                // 获取当前线程
                                def currentThread = $threads.currentThread()
                                // ScriptThread.screenCapture() 用于获取线程对应的屏幕截图器
                                def screenCapture = currentThread.screenCapture()
                                // ScreenCapture.autoRequestByShell() 用于设置是否自动通过 Shell 授予截屏权限
                                screenCapture.autoRequestByShell(true)
                                // ScreenCapture.requestPermission() 用于获取截屏权限
                                def requestPermission = screenCapture.requestPermission()
                                if (requestPermission) {
                                    // ScreenCapture.captureScreen() 用于截取屏幕
                                    def screenImage = screenCapture.captureScreen()
                                    // Images.clip() 用于裁剪图片
                                    def clipImage = $images.clip(screenImage, {
                                        // delegate -> Rect
                                        // Rect.left() 用于设置矩形的左边缘相对于 x 轴的偏移量。
                                        left(100)
                                        // Rect.right() 用于设置矩形的右边缘相对于 x 轴的偏移量。
                                        right(200)
                                        // Rect.top() 用于设置矩形的底边距 y 轴的偏移量。
                                        top(100)
                                        // Rect.bottom() 用于设置矩形的上边缘相对于 y 轴的偏移量。
                                        bottom(200)
                                    })
                                    // Images.matchTemplate() 用于匹配模板
                                    def matchingResults = $images.matchTemplate {
                                        // delegate -> TemplateMatcher
                                        // TemplateMatcher.image() 用于设置原图(大图)
                                        image(screenImage)
                                        // TemplateMatcher.template() 用于设置模板图(小图)
                                        template(clipImage)
                                    }
                                    // ScaffoldState.snackBarHostState() 用于获取 SnackBarHostState
                                    def snackBarHostState = state.snackBarHostState()
                                    // SnackBarHostState.showSnackBar() 用于显示 SnackBar
                                    snackBarHostState.showSnackBar(matchingResults.toString(), null, "Short")
                                } else {
                                    // ScaffoldState.snackBarHostState() 用于获取 SnackBarHostState
                                    def snackBarHostState = state.snackBarHostState()
                                    // SnackBarHostState.showSnackBar() 用于显示 SnackBar
                                    snackBarHostState.showSnackBar("没有截图权限", null, "Short")
                                }
                            }
                        }
                    }
                }
            }
        }
        // Scaffold.content() 用于设置 Scaffold 内容
        content {
            // delegate -> Slot
            // Slot.AsyncImage() 用于创建 AsyncImage 可组合项
            AsyncImage {
                // delegate -> AsyncImage
                // AsyncImage.request() 用于设置图片请求
                request {
                    // delegate -> ImageRequest
                    // ImageRequest.url() 用于设置从指定url获取图片
                    url("https://s1.ax1x.com/2023/02/17/pSbOeMj.jpg")
                    // ImageRequest.format() 用于设置图片格式
                    format("png")
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