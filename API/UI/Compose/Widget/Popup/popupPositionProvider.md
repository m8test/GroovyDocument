功能:

+ 设置弹出窗口位置提供者,如果设置了 [Popup.offset()](/API/UI/Compose/Widget/Popup/README.md?id=offset) ,此配置无效

定义:

+ [Popup](/API/UI/Compose/Widget/Popup/README.md) popupPositionProvider(Closure closure)

参数:

+ Closure closure - 设置位置提供者的闭包
    + 参数 - 无
    + delegate - [PopupPositionProvider](/API/UI/Compose/Widget/Popup/PopupPositionProvider/README.md)

返回值:

+ [Popup](/API/UI/Compose/Widget/Popup/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [Popup.popupPositionProvider()](/API/UI/Compose/Widget/Popup/README.md?id=popupPositionProvider)
  方法设置弹出窗口位置提供者.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.mutableStateOf() 用于创建一个 MutableState 对象
    def state = mutableStateOf(false)
    // Slot.TextButton() 用于设置文本按钮
    TextButton {
        // delegate -> TextButton
        // TextButton.content() 用于设置按钮内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("显示弹出窗口")
            }
        }
        // TextButton.onClick() 用于处理点击事件
        onClick {
            // 设置状态
            state.value(true)
        }
    }
    // Slot.Popup() 用于创建 Popup 可组合项
    Popup {
        // delegate -> Popup
        // Popup.withSingleStates() 用于设置可组合项使用到的所有 SingleState
        withSingleStates(state)
        // Popup.onDismissRequest() 用于设置弹出窗口取消时监听事件
        onDismissRequest {
            // 隐藏弹出窗口
            state.value(false)
        }
        // Popup.show() 用于设置可组合项是否显示
        show(state.value())
        // Popup.popupPositionProvider() 用于设置弹出窗口位置提供者
        popupPositionProvider {
            // delegate -> PopupPositionProvider
            // PopupPositionProvider.x() 用于设置弹出窗口横坐标的获取方法
            x { anchorBounds, windowSize, layoutDirection, popupContentSize ->
                // 返回一个数字作为弹出窗口的横坐标
                // anchorBounds -> Rect 此弹出窗口锚定到的布局的窗口相对边界
                // windowSize -> Size 包含定位布局的窗口的大小
                // layoutDirection -> String 锚定布局的布局方向
                // popupContentSize -> Size 弹出窗口内容的大小
                $console.log(anchorBounds)
                $console.log(windowSize)
                $console.log(layoutDirection)
                $console.log(popupContentSize)
                0
            }
            // PopupPositionProvider.y() 用于设置弹出窗口纵坐标的获取方法
            y { anchorBounds, windowSize, layoutDirection, popupContentSize ->
                // 返回一个数字作为弹出窗口的纵坐标
                // anchorBounds -> Rect 此弹出窗口锚定到的布局的窗口相对边界
                // windowSize -> Size 包含定位布局的窗口的大小
                // layoutDirection -> String 锚定布局的布局方向
                // popupContentSize -> Size 弹出窗口内容的大小
                0
            }
        }
        // Popup.content() 用于设置弹出窗口内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("弹出窗口内容")
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