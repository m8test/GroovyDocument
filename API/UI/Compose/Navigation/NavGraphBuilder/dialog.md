功能:

+ 将可组合项添加到导航图,以对话框形式显示,仅当此对话框代表您应用中的单独屏幕时才适用,该屏幕需要自己的生命周期和保存的状态.独立于导航图中的任何其他目的地。

定义:

+ [NavGraphBuilder](/API/UI/Compose/Navigation/NavGraphBuilder/README.md) dialog(Closure closure)

参数:

+ Closure closure - 构建导航路线的闭包
    + 参数 - 无
    + delegate - [DialogGraph](/API/UI/Compose/Navigation/DialogGraph/README.md)

返回值:

+ [NavGraphBuilder](/API/UI/Compose/Navigation/NavGraphBuilder/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [NavGraphBuilder.dialog()](/API/UI/Compose/Navigation/NavGraphBuilder/README.md?id=dialog)
  方法将可组合项添加到导航图

```groovy
def MyDialogGraph = { routeName, btnText, onBtnClick ->
    // delegate -> NavGraphBuilder
    // NavGraphBuilder.dialog() 用于将可组合项添加到导航图
    dialog {
        // delegate -> DialogGraph
        // DialogGraph.route() 用于设置导航路由
        route(routeName)
        // DialogGraph.content() 用于设置可组合项内容
        content {
            // delegate -> Slot
            // Slot.Column() 用于创建 Column 可组合项
            Column {
                // delegate -> Column
                // Column.content() 用于设置 Column 可组合项中的内容
                content {
                    // delegate -> Slot
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        // Text.text() 用于设置文本可组合项内容
                        text(routeName)
                    }
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
                                text(btnText)
                            }
                        }
                        // Button.onClick() 用于处理点击事件
                        onClick {
                            onBtnClick()
                        }
                    }
                }
            }
        }
    }
}

// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newNavController() 用于创建 NavController 对象
    def navHostController = newNavController()
    // Slot.NavHost() 用于创建 NavHost 可组合项
    NavHost {
        // delegate -> NavHost
        // NavHost.startDestination() 用于设置起始目的地的路线
        startDestination("home")
        // NavHost.navController() 用于设置 NavController
        navController(navHostController)
        // NavHost.builder() 用于构建导航图
        builder {
            // delegate -> NavGraphBuilder
            MyDialogGraph.delegate = delegate
            MyDialogGraph("home", "跳转到detail") {
                // NavController.navigate() 用于导航到指定的路线
                navHostController.navigate("detail") {
                    // delegate -> NavOptions
                }
            }
            MyDialogGraph("detail", "返回到home") {
                // NavController.popBackStack() 用于尝试弹出控制器的返回堆栈
                navHostController.popBackStack()
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