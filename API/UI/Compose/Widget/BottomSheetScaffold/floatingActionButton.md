功能:

+ 设置悬浮动作按钮

定义:

+ [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) floatingActionButton(Closure
  closure)

参数:

+ Closure closure - 设置悬浮动作按钮的闭包
    + 参数 - 无
    + delegate -
      [Slot](/API/UI/Compose/Slot/Slot/README.md)([Modifier](/API/UI/Compose/Modifier/Modifier/README.md))

返回值:

+ [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BottomSheetScaffold.floatingActionButton()](/API/UI/Compose/Widget/BottomSheetScaffold/README.md?id=floatingActionButton)
  方法设置悬浮动作按钮

```groovy
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

def MyBottomSheetScaffold = {
    // delegate -> Slot
    // Slot.BottomSheetScaffold() 用于创建 BottomSheetScaffold 可组合项
    BottomSheetScaffold {
        // delegate -> BottomSheetScaffold
        // BottomSheetScaffold.floatingActionButton() 用于设置悬浮动作按钮
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
    MyBottomSheetScaffold.delegate = delegate
    MyBottomSheetScaffold()
}
// Activity.onDestroy() 方法用于监听Activity销毁
$composeActivity.onDestroy {
    // Script.stop() 方法用于停止脚本
    $script.stop()
}
// Activity.start() 用于启动Android系统的Activity
$composeActivity.start()
```