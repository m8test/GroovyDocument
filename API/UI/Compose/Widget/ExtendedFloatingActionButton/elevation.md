功能:

+ 设置扩展悬浮按钮海拔.

定义:

+ [ExtendedFloatingActionButton](/API/UI/Compose/Widget/ExtendedFloatingActionButton/README.md) elevation(
  Closure closure)

参数:

+ Closure closure - 设置海拔的闭包
    + 参数 - 无
    + delegate - [FloatingActionButtonElevation](/API/UI/Compose/Widget/FloatingActionButton/FloatingActionButtonElevation/README.md)

返回值:

+ [ExtendedFloatingActionButton](/API/UI/Compose/Widget/ExtendedFloatingActionButton/README.md) -
  返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [ExtendedFloatingActionButton.elevation()](/API/UI/Compose/Widget/ExtendedFloatingActionButton/README.md?id=elevation)
  方法设置扩展悬浮按钮海拔.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.ExtendedFloatingActionButton() 用于创建 ExtendedFloatingActionButton 可组合项
    ExtendedFloatingActionButton {
        // delegate -> ExtendedFloatingActionButton
        // ExtendedFloatingActionButton.elevation() 用于设置扩展悬浮按钮海拔
        elevation {
            // delegate -> FloatingActionButtonElevation
            // FloatingActionButtonElevation.defaultElevation() 用于设置默认海拔
            defaultElevation(20)
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