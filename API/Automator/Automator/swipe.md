功能:

+ 在指定时间内从起点滑动到终点,需要无障碍权限(安卓7.0以上)或者ADB自动化

定义:

+ boolean swipe(Closure fromPoint, Closure toPoint, long duration)

参数:

+ Closure fromPoint - 起点
    + 参数 - 无
    + delegate - [Point](/API/UI/Graphics/Point/README.md)
+ Closure toPoint - 终点
    + 参数 - 无
    + delegate - [Point](/API/UI/Graphics/Point/README.md)
+ long duration - 按压时长,单位毫秒

返回值:

+ boolean - true表示操作成功,false表示操作失败

示例代码:

+ 启动一个Activity, 并通过 [Automator.swipe()](/API/Automator/Automator/README.md?id=swipe)
  方法在指定时间内从起点滑动到终点

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
                        text("swipe")
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
                                // Accessibility.selector() 用于创建无障碍节点选择器
                                def accessibilitySelector = $accessibility.selector()
                                // AccessibilitySelector.text() 用于设置节点文本过滤器
                                accessibilitySelector.text {
                                    it == "Text"
                                }
                                // AccessibilitySelector.findOne() 用于查找一个满足无障碍节点选择器的节点
                                def node = accessibilitySelector.findOne(1000)
                                // AccessibilityNode.bounds() 用于获取节点的 bounds 值
                                def bounds = node.bounds()
                                // Automator.swipe() 用于在指定时间内从起点滑动到终点
                                $automator.swipe({
                                    // delegate -> Point
                                    // Point.x() 用于设置横坐标
                                    x(bounds.left())
                                    // Point.y() 用于设置纵坐标
                                    y(bounds.top())
                                }, {
                                    // delegate -> Point
                                    // Point.x() 用于设置横坐标
                                    x(bounds.left() + bounds.width())
                                    // Point.y() 用于设置纵坐标
                                    y(bounds.top() + bounds.height())
                                }, 2000)
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