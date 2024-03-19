功能:

+ 设置底部应用程序栏

定义:

+ [Scaffold](/API/UI/Compose/Widget/Scaffold/README.md) bottomBar(Closure closure)

参数:

+ Closure closure - 设置底部应用程序栏的闭包
    + 参数 - 无
    + delegate -
      [Slot](/API/UI/Compose/Slot/Slot/README.md)([Modifier](/API/UI/Compose/Modifier/Modifier/README.md))

返回值:

+ [Scaffold](/API/UI/Compose/Widget/Scaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Scaffold.bottomBar()](/API/UI/Compose/Widget/Scaffold/README.md?id=bottomBar)
  方法设置底部应用程序栏

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