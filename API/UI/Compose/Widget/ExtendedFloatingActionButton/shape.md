功能:

+ 设置扩展悬浮按钮形状.

定义:

+ [ExtendedFloatingActionButton](/API/UI/Compose/Widget/ExtendedFloatingActionButton/README.md) shape(
  Closure closure)

参数:

+ Closure closure - 设置形状的闭包
    + 参数 - 无
    + delegate - [Shape](/API/UI/Compose/Theme/Shape/Shape/README.md)

返回值:

+ [ExtendedFloatingActionButton](/API/UI/Compose/Widget/ExtendedFloatingActionButton/README.md) -
  返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [ExtendedFloatingActionButton.shape()](/API/UI/Compose/Widget/ExtendedFloatingActionButton/README.md?id=shape)
  方法设置扩展悬浮按钮形状.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.ExtendedFloatingActionButton() 用于创建 ExtendedFloatingActionButton 可组合项
    ExtendedFloatingActionButton {
        // delegate -> ExtendedFloatingActionButton
        // ExtendedFloatingActionButton.shape() 用于设置扩展悬浮按钮形状
        shape {
            // delegate -> Shape
            // Shape.all() 用于设置四个角尺寸
            all(20, "dp")
            // Shape.roundedCorner() 用于设置角的类型为圆角
            roundedCorner()
        }
        // ExtendedFloatingActionButton.icon() 用于设置扩展悬浮按钮图标
        icon {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("+")
            }
        }
        // ExtendedFloatingActionButton.text() 用于设置扩展悬浮按钮文本
        text {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("添加")
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