功能:

+ 设置起始目的地的路线

定义:

+ [NavHost](/API/UI/Compose/Navigation/NavHost/README.md) startDestination(String destination)

参数:

+ String destination - 起始目的地的路线

返回值:

+ [NavHost](/API/UI/Compose/Navigation/NavHost/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [NavHost.startDestination()](/API/UI/Compose/Navigation/NavHost/README.md?id=startDestination)
  方法设置起始目的地的路线

```groovy
def MyComposableGraph = { routeName, btnText, onBtnClick ->
    // delegate -> NavGraphBuilder
    // NavGraphBuilder.composable() 用于将可组合项添加到导航图
    composable {
        // delegate -> ComposableGraph
        // ComposableGraph.route() 用于设置导航路线
        route(routeName)
        // ComposableGraph.content() 用于设置可组合项内容
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
            MyComposableGraph.delegate = delegate
            MyComposableGraph("home", "跳转到detail") {
                // NavController.navigate() 用于导航到指定的路线
                navHostController.navigate("detail") {
                    // delegate -> NavOptions
                }
            }
            MyComposableGraph("detail", "返回到home") {
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