功能:

+ 获取图片高度

定义:

+ int height()

参数:

+ 无

返回值:

+ int - 图片高度

示例代码:

+ 启动一个Activity, 并通过 [ScriptImage.height()](/API/Image/ScriptImage/README.md?id=height) 方法获取图片高度

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newCoroutineScope() 用于创建 CoroutineScope
    def coroutineScope = newCoroutineScope {
        // delegate -> CoroutineContext
    }
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
                        text("height")
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
                            // CoroutineScope.launch() 用于启动一个子协程(如果CoroutineContext设置了Job参数,那么就是启动一个新协程,与启动它的协程没有父子关系)
                            coroutineScope.launch({
                                // delegate -> CoroutineContext
                                dispatcher("IO")
                            }, "DEFAULT") {
                                // delegate -> CoroutineScope
                                // Images.read() 用于读取图片
                                def originImage = $images.read {
                                    // delegate -> ImageReader
                                    // ImageReader.url() 用于从网络读取图片
                                    url("https://s1.ax1x.com/2023/02/17/pSbOeMj.jpg")
                                }
                                // ScriptImage.height() 用于获取图片高度
                                def imageHeight = originImage.height()
                                // ScaffoldState.snackBarHostState() 用于获取 SnackBarHostState
                                def snackBarHostState = state.snackBarHostState()
                                // SnackBarHostState.showSnackBar() 用于显示 SnackBar
                                snackBarHostState.showSnackBar("height:${imageHeight}", null, "Short")
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