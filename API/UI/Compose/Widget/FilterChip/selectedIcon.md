功能:

+ 设置 [FilterChip](/API/UI/Compose/Widget/FilterChip/README.md) 被选中时显示的图标.

定义:

+ [FilterChip](/API/UI/Compose/Widget/FilterChip/README.md) selectedIcon(boolean value)

参数:

+ Closure closure - 设置图标的闭包
    + 参数 - 无
    + delegate -
      [Slot](/API/UI/Compose/Slot/Slot/README.md)([Modifier](/API/UI/Compose/Modifier/Modifier/README.md))

返回值:

+ [FilterChip](/API/UI/Compose/Widget/FilterChip/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [FilterChip.selectedIcon()](/API/UI/Compose/Widget/FilterChip/README.md?id=selectedIcon)
  方法设置 [FilterChip](/API/UI/Compose/Widget/FilterChip/README.md) 被选中时显示的图标

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.FilterChip() 用于创建 FilterChip 可组合项
    FilterChip {
        // delegate -> FilterChip
        // FilterChip.selectedIcon() 用于设置 FilterChip 被选中时显示的图标
        selectedIcon {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("&")
            }
        }
        // FilterChip.selected() 用于设置是否选中 FilterChip
        selected(true)
        // FilterChip.content() 用于设置 FilterChip 内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("FilterChip")
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