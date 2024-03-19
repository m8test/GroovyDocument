功能:

+ 检查是否设置 systemGestureExclusionRects 的标志

定义:

+ [PopupProperties](/API/UI/Compose/Widget/Popup/PopupProperties/README.md) excludeFromSystemGesture(
  boolean value)

参数:

+ boolean value - true 表示检查 systemGestureExclusionRects ,false 表示不检查 systemGestureExclusionRects

返回值:

+ [PopupProperties](/API/UI/Compose/Widget/Popup/PopupProperties/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity显示对话框,
  并通过 [PopupProperties.excludeFromSystemGesture()](/API/UI/Compose/Widget/Popup/PopupProperties/README.md?id=excludeFromSystemGesture)
  方法检查是否设置 systemGestureExclusionRects 的标志

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
                text("下拉菜单")
            }
        }
        // TextButton.onClick() 用于处理点击事件
        onClick {
            // 设置状态
            state.value(true)
        }
    }
    // Slot.DropdownMenu() 用于创建 DropdownMenu 可组合项
    DropdownMenu {
        // delegate -> DropdownMenu
        // DropdownMenu.withSingleStates() 用于设置可组合项使用到的所有 SingleState
        withSingleStates(state)
        // DropdownMenu.popupProperties() 用于设置下拉菜单属性
        popupProperties {
            // delegate -> PopupProperties
            // PopupProperties.excludeFromSystemGesture() 用于检查是否设置 systemGestureExclusionRects 的标志
            excludeFromSystemGesture(false)
            // PopupProperties.dismissOnClickOutside() 用于设置下拉菜单是否允许点击菜单外面触发 onDismissRequest
            dismissOnClickOutside(false)
            // PopupProperties.focusable() 用于设置下拉菜单是否获取焦点
            focusable(true)
        }
        // DropdownMenu.onDismissRequest() 用于设置下拉菜单取消时监听事件
        onDismissRequest {
            // 隐藏下拉菜单
            state.value(false)
        }
        // DropdownMenu.expanded() 用于设置下拉菜单是否展开
        expanded(state.value())
        // DropdownMenu.content() 用于设置下拉菜单内容
        content {
            // delegate -> Slot
            // Slot.DropdownMenuItem() 用于创建 DropdownMenuItem 可组合项
            DropdownMenuItem {
                // delegate -> DropdownMenuItem
                // DropdownMenuItem.content() 用于设置下拉菜单项内容
                content {
                    // delegate -> Slot
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        // Text.text() 用于设置文本可组合项内容
                        text("菜单项1")
                    }
                }
            }
            // Slot.DropdownMenuItem() 用于创建 DropdownMenuItem 可组合项
            DropdownMenuItem {
                // delegate -> DropdownMenuItem
                // DropdownMenuItem.content() 用于设置下拉菜单项内容
                content {
                    // delegate -> Slot
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        // Text.text() 用于设置文本可组合项内容
                        text("菜单项2")
                    }
                }
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