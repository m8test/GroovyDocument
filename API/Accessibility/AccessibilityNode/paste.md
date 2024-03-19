功能:

+ 粘贴内容到节点

定义:

+ boolean paste()

参数:

+ 无

返回值:

+ boolean - true表示操作成功,false表示操作失败

示例代码:

+ 启动一个Activity,
  并通过 [AccessibilityNode.paste()](/API/Accessibility/AccessibilityNode/README.md?id=paste)
  方法粘贴内容到节点

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
                        text("paste")
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
                                    it == "TextField"
                                }
                                // AccessibilitySelector.findOne() 用于查找一个满足无障碍节点选择器的节点
                                def node = accessibilitySelector.findOne(1000)
                                // AccessibilityNode.setSelection() 用于选择指定索引范围的内容
                                $console.log(node.setSelection(0, 5))
                                // CoroutineScope.delay() 用于协程延时
                                delay(1000)
                                // AccessibilityNode.cut() 用于剪切节点已选择的内容
                                $console.log(node.cut())
                                // CoroutineScope.delay() 用于协程延时
                                delay(1000)
                                // AccessibilityNode.paste() 用于粘贴内容到节点
                                $console.log(node.paste())
                            }
                        }
                    }
                }
            }
        }
        // Scaffold.content() 用于设置 Scaffold 内容
        content {
            // delegate -> Slot
            // Slot.mutableStateOf() 用于创建一个 MutableState 对象
            def textFieldState = mutableStateOf("TextField")
            // Slot.TextField() 用于创建 TextField 可组合项
            TextField {
                // delegate -> TextField
                // Composable.withSingleStates() 用于设置可组合项使用到的所有 SingleState , 因为 TextField 可组合项继承自 Composable ,所以可以调用 withSingleStates 方法
                withSingleStates(textFieldState)
                // TextField.value() 用于设置输入框中的内容
                value(textFieldState.value())
                // TextField.onValueChange() 用于监听输入框中内容变化
                onValueChange { textFieldValue ->
                    // MutableState.value() 用于设置 MutableState 对象的值.
                    textFieldState.value(textFieldValue)
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