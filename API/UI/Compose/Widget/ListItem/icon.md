功能:

+ 设置列表项图标

定义:

+ [ListItem](/API/UI/Compose/Widget/ListItem/README.md) icon(Closure closure)

参数:

+ Closure closure - 设置图标的闭包
    + 参数 - 无
    + delegate -
      [Slot](/API/UI/Compose/Slot/Slot/README.md)([Modifier](/API/UI/Compose/Modifier/Modifier/README.md))

返回值:

+ [ListItem](/API/UI/Compose/Widget/ListItem/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [ListItem.icon()](/API/UI/Compose/Widget/ListItem/README.md?id=icon) 方法设置列表项图标

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.ListItem() 用于创建 ListItem 可组合项
    ListItem {
        // delegate -> ListItem
        // ListItem.icon() 用于设置列表项图标
        icon {
            // delegate -> Slot
            // Slot.Icon() 用于创建 Icon 可组合项
            Icon {
                // delegate -> Icon
                // Icon.vector() 用于设置图标矢量图
                vector("Filled", "Key")
            }
        }
        // ListItem.secondaryText() 用于设置列表项的辅助文本
        secondaryText {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("secondary text")
            }
        }
        // ListItem.overLineText() 用于设置列表项显示在主要文本上方的文本
        overLineText {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("over line text")
            }
        }
        // ListItem.trailing() 用于设置列表项尾随的元文本、图标、开关或复选框
        trailing {
            // delegate -> Slot
            // Slot.Icon() 用于创建 Icon 可组合项
            Icon {
                // delegate -> Icon
                // Icon.vector() 用于设置图标矢量图
                vector("Filled", "Delete")
            }
        }
        // ListItem.text() 用于设置列表项的主要文本
        text {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("text")
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