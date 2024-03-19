功能:

+ 设置深层链接请求的 [Uri](https://developer.android.google.cn/reference/android/net/Uri)

定义:

+ [NavDeepLinkRequest](/API/UI/Compose/Navigation/NavDeepLinkRequest/README.md)
  uri([Uri](https://developer.android.google.cn/reference/android/net/Uri) uri)

参数:

+ [Uri](https://developer.android.google.cn/reference/android/net/Uri) uri -
  需要设置的 [Uri](https://developer.android.google.cn/reference/android/net/Uri) 对象

返回值:

+ [NavDeepLinkRequest](/API/UI/Compose/Navigation/NavDeepLinkRequest/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [NavDeepLinkRequest.uri()](/API/UI/Compose/Navigation/NavDeepLinkRequest/README.md?id=uri)
  方法设置深层链接请求的 [Uri](https://developer.android.google.cn/reference/android/net/Uri)

```groovy
def detailUri = "https://www.m8test.com"
def MyDetailComposable = { navHostController ->
    // delegate -> NavGraphBuilder
    // NavGraphBuilder.composable() 用于将可组合项添加到导航图
    composable {
        // delegate -> ComposableGraph
        // ComposableGraph.route() 用于设置导航路线
        route("detail/{detailId}")
        // ComposableGraph.deepLinks() 用于设置深层链接
        deepLinks({
            // delegate -> NavDeepLink
            // NavDeepLink.uriPattern() 用于设置深层链接的uri模式
            uriPattern("${detailUri}/{detailId}")
        })
        // ComposableGraph.content() 用于设置可组合项内容
        content { navBackStackEntry ->
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
                        // NavBackStackEntry.arguments() 用于获取导航参数
                        def arguments = navBackStackEntry.arguments()
                        // Text.text() 用于设置文本可组合项内容
                        text("detail-${arguments.getString("detailId")}")
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
                                text("返回到home")
                            }
                        }
                        // Button.onClick() 用于处理点击事件
                        onClick {
                            // NavController.popBackStack() 用于尝试弹出控制器的返回堆栈
                            navHostController.popBackStack()
                        }
                    }
                }
            }
        }
    }
}

def MyHomeComposable = { navHostController ->
    // delegate -> NavGraphBuilder
    // NavGraphBuilder.composable() 用于将可组合项添加到导航图
    composable {
        // delegate -> ComposableGraph
        // ComposableGraph.route() 用于设置导航路线
        route("home")
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
                        text("home")
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
                                text("跳转到detail(deep link)")
                            }
                        }
                        // Button.onClick() 用于处理点击事件
                        onClick {
                            // NavController.navigate() 用于导航到指定的路线
                            navHostController.navigate({
                                // delegate -> NavDeepLinkRequest
                                // NavDeepLinkRequest.uri() 用于设置深层链接请求的 Uri
                                uri(android.net.Uri.parse("$detailUri/detailIdFromDeepLink"))
                            }) {
                                // delegate -> NavOptions
                            }
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
            MyHomeComposable.delegate = delegate
            MyHomeComposable(navHostController)
            MyDetailComposable.delegate = delegate
            MyDetailComposable(navHostController)
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