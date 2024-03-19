功能:

+ 在测量完所有其他内容元素后，调整元素大小以匹配 [Box](/API/UI/Compose/Widget/Box/README.md)
  的大小。使用此修饰符的元素不参与定义 [Box](/API/UI/Compose/Widget/Box/README.md) 的大小。
  相反，在测量所有其他子项（不使用 [BoxScopeModifier.matchParentSize()](/API/UI/Compose/Modifier/BoxScopeModifier/README.md?id=matchParentSize)
  修饰符）以获得
  [Box](/API/UI/Compose/Widget/Box/README.md) 的大小之后，它匹配 [Box](/API/UI/Compose/Widget/Box/README.md) 的大小。 相反，通用的
  [Modifier.fillMaxSize()](/API/UI/Compose/Modifier/Modifier/README.md?id=fillMaxSize) 修饰符使元素占据所有可用空间，将参与定义
  [Box](/API/UI/Compose/Widget/Box/README.md) 的大小。 因此，将它用于 [Box](/API/UI/Compose/Widget/Box/README.md)
  内的元素将使 [Box](/API/UI/Compose/Widget/Box/README.md) 本身始终填充可用空间。

定义:

+ [BoxScopeModifier](/API/UI/Compose/Modifier/BoxScopeModifier/README.md) matchParentSize()

参数:

+ 无

返回值:

+ [BoxScopeModifier](/API/UI/Compose/Modifier/BoxScopeModifier/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BoxScopeModifier.matchParentSize()](/API/UI/Compose/Modifier/BoxScopeModifier/README.md?id=matchParentSize)
  方法调整元素大小以匹配 [Box](/API/UI/Compose/Widget/Box/README.md) 的大小.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Box() 用于创建 Box 可组合项
    Box {
        // delegate -> Box
        // Box.modifier() 用于设置修饰符
        modifier {
            // delegate -> BoxScopeModifier
            // Modifier.size() 用于同时设置宽度和高度
            size(150)
        }
        // Box.content() 用于设置 Box 内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.modifier() 用于设置修饰符
                modifier {
                    // delegate -> BoxScopeModifier
                    // BoxScopeModifier.matchParentSize() 用于调整元素大小以匹配 Box 的大小
                    matchParentSize()
                    // Modifier.background() 用于设置背景颜色
                    background({
                        // delegate -> Color
                        // Color.red() 用于配置红色通道
                        red(255)
                    }) {
                        // delegate -> Shape
                        // 不配置Shape默认为矩形
                    }
                }
                // Text.text() 用于设置文本可组合项内容
                text("Box内容")
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