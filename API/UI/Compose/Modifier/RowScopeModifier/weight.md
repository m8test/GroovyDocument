功能:

+ 调整元素的宽度大小与其相对于 [Row](/API/UI/Compose/Widget/Row/README.md) 中其他加权同级元素的权重成比例。
  父元素会划分测量未加权的子元素后剩余的水平空间，并按照这个权重进行分配。 当 fill
  为真时，元素将被强制占据分配给它的整个宽度。 否则，允许元素更小——这将导致 [Row](/API/UI/Compose/Widget/Row/README.md)
  更小，因为未使用的分配宽度不会重新分配给其他兄弟。

定义:

+ [RowScopeModifier](/API/UI/Compose/Modifier/RowScopeModifier/README.md) weight(float weight, boolean fill)

参数:

+ float weight - 赋予此元素的比例宽度，与所有加权兄弟姐妹的总数相关。
+ boolean fill - 当为真时，元素将占据分配的整个宽度。

返回值:

+ [RowScopeModifier](/API/UI/Compose/Modifier/RowScopeModifier/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [RowScopeModifier.weight()](/API/UI/Compose/Modifier/RowScopeModifier/README.md?id=weight)
  方法调整元素的宽度大小与其相对于 [Row](/API/UI/Compose/Widget/Row/README.md) 中其他加权同级元素的权重成比例.

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
                    // RowScopeModifier.weight() 用于调整元素的宽度大小与其相对于 Row 中其他加权同级元素的权重成比例
                    weight(0.7f, true)
                }
                // Text.text() 用于设置文本可组合项内容
                text("0.7")
            }
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.modifier() 用于修饰 Composable
                modifier {
                    // delegate -> RowScopeModifier
                    // RowScopeModifier.weight() 用于调整元素的宽度大小与其相对于 Row 中其他加权同级元素的权重成比例
                    weight(0.3f, true)
                }
                // Text.text() 用于设置文本可组合项内容
                text("0.3")
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