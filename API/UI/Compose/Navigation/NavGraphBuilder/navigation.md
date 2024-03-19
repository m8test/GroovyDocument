功能:

+ 构造一个嵌套的导航图

定义:

+ [NavGraphBuilder](/API/UI/Compose/Navigation/NavGraphBuilder/README.md) navigation(Closure closure)

参数:

+ Closure closure - 构建嵌套导航图的闭包
    + 参数 - 无
    + delegate - [NavigationGraph](/API/UI/Compose/Navigation/NavigationGraph/README.md)

返回值:

+ [NavGraphBuilder](/API/UI/Compose/Navigation/NavGraphBuilder/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [NavGraphBuilder.navigation()](/API/UI/Compose/Navigation/NavGraphBuilder/README.md?id=navigation)
  方法构造一个嵌套的导航图

```groovy
def MyComposableGraph = { routeName, btnText, onBtnClick, btn2Text = "", onBtn2Click = null ->
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
                    // Slot.Button() 用于创建 Button 可组合项
                    Button {
                        // delegate -> Button
                        // Button.show() 用于设置可组合项是否显示
                        show(btn2Text != "")
                        // Button.content() 用于设置按钮内容
                        content {
                            // delegate -> Slot
                            // Slot.Text() 用于创建文本可组合项
                            Text {
                                // delegate -> Text
                                // Text.text() 用于设置文本可组合项内容
                                text(btn2Text)
                            }
                        }
                        // Button.onClick() 用于处理点击事件
                        onClick {
                            onBtn2Click()
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
        startDestination("authorization")
        // NavHost.navController() 用于设置 NavController
        navController(navHostController)
        // NavHost.builder() 用于构建导航图
        builder {
            // delegate -> NavGraphBuilder
            // NavGraphBuilder.navigation() 用于构造一个嵌套的导航图
            navigation {
                // delegate -> NavigationGraph
                // NavigationGraph.route() 用于设置导航路线
                route("main")
                // NavigationGraph.startDestination() 用于设置起始目的地的路线
                startDestination("home")
                // NavigationGraph.builder() 用于构建导航图
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
            // NavGraphBuilder.navigation() 用于构造一个嵌套的导航图
            navigation {
                // delegate -> NavigationGraph
                // NavigationGraph.route() 用于设置导航路线
                route("authorization")
                // NavigationGraph.startDestination() 用于设置起始目的地的路线
                startDestination("login")
                // NavigationGraph.builder() 用于构建导航图
                builder {
                    // delegate -> NavGraphBuilder
                    MyComposableGraph.delegate = delegate
                    MyComposableGraph("login", "登录", {
                        // NavController.navigate() 用于导航到指定的路线
                        navHostController.navigate("main") {
                            // delegate -> NavOptions
                            // NavOptions.popUpTo() 用于在导航之前弹出给定的目的地
                            popUpTo("login") {
                                // delegate -> PopUpTo
                                // PopUpTo.inclusive() 用于设置目的地是否应该从返回堆栈中弹出
                                inclusive(true)
                            }
                        }
                    }, "注册") {
                        // NavController.navigate() 用于导航到指定的路线
                        navHostController.navigate("register") {
                            // delegate -> NavOptions
                        }
                    }
                    MyComposableGraph("register", "登录") {
                        // NavController.navigate() 用于导航到指定的路线
                        navHostController.navigate("login") {
                            // delegate -> NavOptions
                            // NavOptions.popUpTo() 用于在导航之前弹出给定的目的地
                            popUpTo("login") {
                                // delegate -> PopUpTo
                                // PopUpTo.inclusive() 用于设置目的地是否应该从返回堆栈中弹出
                                inclusive(true)
                            }
                        }
                    }
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