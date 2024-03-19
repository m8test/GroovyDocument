功能:

+ 设置节点内容

定义:

+ boolean setText(String content)

参数:

+ String content - 需要设置的内容

返回值:

+ boolean - true表示操作成功,false表示操作失败

示例代码:

+ 启动一个Activity,
  并通过 [AccessibilityNode.setText()](/API/Accessibility/AccessibilityNode/README.md?id=setText)
  方法设置节点内容

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
                        text("setText")
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
                            // Accessibility.selector() 用于创建无障碍节点选择器
                            def accessibilitySelector = $accessibility.selector()
                            // AccessibilitySelector.text() 用于设置节点文本过滤器
                            accessibilitySelector.text {
                                it == "TextField"
                            }
                            // AccessibilitySelector.findOne() 用于查找一个满足无障碍节点选择器的节点
                            def node = accessibilitySelector.findOne(1000)
                            // AccessibilityNode.setText() 用于设置节点内容
                            $console.log(node.setText("setText"))
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