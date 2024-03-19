功能:

+ 在行内垂直对齐元素。此对齐方式将优先于 [Row.verticalAlignment()](/API/UI/Compose/Widget/Row/README.md?id=verticalAlignment)

定义:

+ [RowScopeModifier](/API/UI/Compose/Modifier/RowScopeModifier/README.md) align(String alignment)

参数:

+ String alignment - 垂直对齐方式,可选值有
    + Bottom -> 底部对齐
    + Top -> 顶部对齐
    + CenterVertically -> 垂直居中对齐

返回值:

+ [RowScopeModifier](/API/UI/Compose/Modifier/RowScopeModifier/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [RowScopeModifier.align()](/API/UI/Compose/Modifier/RowScopeModifier/README.md?id=align)
  方法在行内垂直对齐元素.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Row() 用于创建 Row 可组合项
    Row {
        // delegate -> Row
        // Row.modifier() 用于修饰 Composable
        modifier {
            // delegate -> Modifier
            // Modifier.fillMaxSize() 用于设置填充父可组合项宽度和高度, 参数为填充父可组合项的比例, 取值区间为 0.0f-1.0f
            fillMaxSize(1.0f)
        }
        // Row.content() 用于设置 Row 内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.modifier() 用于修饰 Composable
                modifier {
                    // delegate -> RowScopeModifier
                    // RowScopeModifier.align() 用于在行内垂直对齐元素
                    align("CenterVertically")
                }
                // Text.text() 用于设置文本可组合项内容
                text("Row")
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