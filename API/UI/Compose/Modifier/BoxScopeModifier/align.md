功能:

+ 将内容元素拉到 [Box](/API/UI/Compose/Widget/Box/README.md) 中的特定对齐方式。此对齐方式将优先于 [Box](/API/UI/Compose/Widget/Box/README.md)
  的对齐方式参数。

定义:

+ [BoxScopeModifier](/API/UI/Compose/Modifier/BoxScopeModifier/README.md) align(String alignment)

参数:

+ String alignment - 内容对其方式,可选值有
    + Center - 居中对齐
    + CenterStart - 左居中对齐
    + CenterEnd - 右居中对齐
    + TopCenter - 上居中对齐
    + TopStart - 左上对齐
    + TopEnd - 右上对齐
    + BottomCenter - 下居中对齐
    + BottomEnd - 右下对齐
    + BottomStart - 右下对齐

返回值:

+ [BoxScopeModifier](/API/UI/Compose/Modifier/BoxScopeModifier/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [BoxScopeModifier.align()](/API/UI/Compose/Modifier/BoxScopeModifier/README.md?id=align)
  方法将内容元素拉到 [Box](/API/UI/Compose/Widget/Box/README.md) 中的特定对齐方式.

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
                    // BoxScopeModifier.align() 用于将内容元素拉到 Box 中的特定对齐方式
                    align("Center")
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