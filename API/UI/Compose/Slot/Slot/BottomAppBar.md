功能:

+ 创建 [BottomAppBar](/API/UI/Compose/Widget/BottomAppBar/README.md) 可组合项

定义:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) BottomAppBar(Closure closure)

参数:

+ Closure closure - 设置 [BottomAppBar](/API/UI/Compose/Widget/BottomAppBar/README.md) 的闭包
    + 参数 - 无
    + delegate - [BottomAppBar](/API/UI/Compose/Widget/BottomAppBar/README.md)

返回值:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Slot.BottomAppBar()](/API/UI/Compose/Slot/Slot/README.md?id=BottomAppBar)
  方法创建 [BottomAppBar](/API/UI/Compose/Widget/BottomAppBar/README.md) 可组合项.

```groovy
def MyBottomAppBar = {
    // delegate -> Slot
    // Slot.BottomAppBar() 用于创建 BottomAppBar 可组合项
    BottomAppBar {
        // delegate -> BottomAppBar
        // BottomAppBar.backgroundColor() 用于设置应用程序栏背景颜色
        backgroundColor {
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }
        // BottomAppBar.cutoutShape() 用于设置应用程序栏的剪切形状
        cutoutShape {
            // delegate -> Shape
            // Shape.all() 用于设置四个角尺寸
            all(50, "percent")
        }
        // BottomAppBar.modifier() 用于配置可组合项的 Modifier
        modifier {
            // delegate -> Modifier
            // Modifier.fillMaxWidth() 用于设置填充最大宽度
            fillMaxWidth(1.0f)
        }
        // BottomAppBar.content() 用于设置应用程序栏内容
        content {
            // delegate -> Slot
            // Modifier -> RowScopeModifier
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Item1")
                // Text.modifier() 用于配置可组合项的 Modifier
                modifier {
                    // delegate -> RowScopeModifier
                    // RowScopeModifier.weight() 用于配置权重
                    weight(1.0f)
                }
            }
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Item2")
                // Text.modifier() 用于配置可组合项的 Modifier
                modifier {
                    // delegate -> RowScopeModifier
                    // RowScopeModifier.weight() 用于配置权重
                    weight(1.0f)
                }
            }
        }
    }
}

def MyFloatingActionButton = {
    // delegate -> Slot
    // Slot.FloatingActionButton() 用于创建 FloatingActionButton 可组合项
    FloatingActionButton {
        // delegate -> FloatingActionButton
        // FloatingActionButton.content() 用于设置悬浮动作按钮内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("按钮")
            }
        }
        // FloatingActionButton.shape() 用于设置悬浮动作按钮形状
        shape {
            // delegate -> Shape
            // Shape.all() 用于设置四个角尺寸
            all(50, "percent")
        }
    }
}

def MyScaffold = {
    // delegate -> Slot
    // Slot.Scaffold() 用于创建 Scaffold 可组合项
    Scaffold {
        // delegate -> Scaffold
        // Scaffold.bottomBar() 用于设置底部应用程序栏
        bottomBar {
            // delegate -> Slot
            MyBottomAppBar.delegate = delegate
            MyBottomAppBar()
        }
        // Scaffold.floatingActionButton() 用于设置悬浮动作按钮
        floatingActionButton {
            // delegate -> Slot
            MyFloatingActionButton.delegate = delegate
            MyFloatingActionButton()
        }
    }
}

// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    MyScaffold.delegate = delegate
    MyScaffold()
}
// Activity.onDestroy() 方法用于监听Activity销毁
$composeActivity.onDestroy {
    // Script.stop() 方法用于停止脚本
    $script.stop()
}
// Activity.start() 用于启动Android系统的Activity
$composeActivity.start()
```