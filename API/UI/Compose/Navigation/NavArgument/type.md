功能:

+ 设置参数类型

定义:

+ [NavArgument](/API/UI/Compose/Navigation/NavArgument/README.md) type(String type)

参数:

+ String type - 参数类型,可选值有
    + BoolArrayType - 布尔数组类型
    + BoolType - 布尔类型
    + FloatArrayType - 浮点数数组类型
    + FloatType - 浮点数类型
    + IntArrayType - 整数数组类型
    + IntType - 整数类型
    + LongArrayType - 长整数数组类型
    + LongType - 长整数类型
    + ReferenceType - 引用类型
    + StringArrayType - 字符串数组类型
    + StringType - 字符串类型

返回值:

+ [NavArgument](/API/UI/Compose/Navigation/NavArgument/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [NavArgument.type()](/API/UI/Compose/Navigation/NavArgument/README.md?id=type) 方法设置参数类型

```groovy
def MyDetailComposable = { navHostController ->
    // delegate -> NavGraphBuilder
    // NavGraphBuilder.composable() 用于将可组合项添加到导航图
    composable {
        // delegate -> ComposableGraph
        // ComposableGraph.arguments() 用于设置导航参数信息
        arguments({
            // delegate -> NavArgument
            // NavArgument.name() 用于设置参数名
            name("detailId")
            // NavArgument.type() 用于设置参数类型
            type("StringType")
            // NavArgument.nullable() 用于设置参数是否可空
            nullable(false)
            // NavArgument.defaultValue() 用于设置参数默认值
            defaultValue("defaultId")
        })
        // ComposableGraph.route() 用于设置导航路线
        route("detail?detailId={detailId}")
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
                                text("跳转到detail(指定参数)")
                            }
                        }
                        // Button.onClick() 用于处理点击事件
                        onClick {
                            // NavController.navigate() 用于导航到指定的路线
                            navHostController.navigate("detail?detailId=detail1234") {
                                // delegate -> NavOptions
                            }
                        }
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
                                text("跳转到detail(默认参数)")
                            }
                        }
                        // Button.onClick() 用于处理点击事件
                        onClick {
                            // NavController.navigate() 用于导航到指定的路线
                            navHostController.navigate("detail") {
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