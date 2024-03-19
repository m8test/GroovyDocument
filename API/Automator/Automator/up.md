功能:

+ 将手指在指定坐标抬起,需要ADB自动化权限

定义:

+ boolean up(int pointerId, int x, int y)

参数:

+ int pointerId - 多指触控时的手指id
+ int x - 横坐标
+ int y - 纵坐标

返回值:

+ boolean - true表示操作成功,false表示操作失败

示例代码:

+ 启动一个Activity, 并通过 [Automator.up()](/API/Automator/Automator/README.md?id=up) 方法将手指在指定坐标抬起

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
                        text("down")
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
                                // CoroutineScope.delay() 用于协程延时
                                delay(1000)
                                // 开始x坐标
                                def startX = 500
                                // 结束x坐标
                                def endX = 500
                                // 开始y坐标
                                def startY = 20
                                // 结束y坐标
                                def endY = 600
                                // Automator.down() 用于将手指在指定坐标按下
                                $automator.down(0, startX, startY)
                                // 移动时间1秒钟
                                def moveTime = 1000
                                // 移动的步数
                                def moveStep = 10
                                for (i in 0..<moveStep) {
                                    int x = (int) (startX + (i + 1) * (endX - startX) / moveStep)
                                    int y = (int) (startY + (i + 1) * (endY - startY) / moveStep)
                                    // Automator.move() 用于将手指移动到指定坐标
                                    $automator.move(0, x, y)
                                    int delayTime = (int) (moveTime / moveStep)
                                    // CoroutineScope.delay() 用于协程延时
                                    delay(delayTime)
                                    $console.log("x:$x,y:$y,delay:$delayTime")
                                }
                                // Automator.up() 用于将手指在指定坐标抬起
                                $automator.up(0, endX, endY)
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
                text("Text")
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