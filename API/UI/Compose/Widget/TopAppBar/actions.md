功能:

+ 设置应用程序栏的右边动作按钮.

定义:

+ [TopAppBar](/API/UI/Compose/Widget/TopAppBar/README.md) actions(Closure closure)

参数:

+ Closure closure - 设置动作按钮的闭包
    + 参数 - 无
    + delegate -
      [RowScopeSlot](/API/UI/Compose/Slot/RowScopeSlot/README.md)([RowScopeModifier](/API/UI/Compose/Modifier/RowScopeModifier/README.md))

返回值:

+ [TopAppBar](/API/UI/Compose/Widget/TopAppBar/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [TopAppBar.actions()](/API/UI/Compose/Widget/TopAppBar/README.md?id=actions)
  方法设置应用程序栏右边动作按钮.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.TopAppBar() 用于创建 TopAppBar 可组合项
    TopAppBar {
        // delegate -> TopAppBar
        // TopAppBar.backgroundColor() 用于设置应用程序栏背景颜色
        backgroundColor {
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }
        // TopAppBar.modifier() 用于配置可组合项的 Modifier
        modifier {
            // delegate -> Modifier
            // Modifier.fillMaxWidth() 用于设置填充最大宽度
            fillMaxWidth(1.0f)
        }
        // TopAppBar.navigationIcon() 用于设置应用程序栏左边导航按钮
        navigationIcon {
            // delegate -> Slot
            // Slot.IconButton() 用于创建 IconButton 可组合项
            IconButton {
                // delegate -> IconButton
                // IconButton.content() 用于设置图标按钮内容
                content {
                    // delegate -> Slot
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        // Text.text() 用于设置文本可组合项内容
                        text("<")
                    }
                }
            }
        }
        // TopAppBar.title() 用于设置应用程序栏标题
        title {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("标题")
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
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        // Text.text() 用于设置文本可组合项内容
                        text("@")
                    }
                }
            }
            // Slot.IconButton() 用于创建 IconButton 可组合项
            IconButton {
                // delegate -> IconButton
                // IconButton.content() 用于设置图标按钮内容
                content {
                    // delegate -> Slot
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        // Text.text() 用于设置文本可组合项内容
                        text("&")
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