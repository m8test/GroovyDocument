功能:

+ 设置列表项辅助文本是否为单行

定义:

+ [ListItem](/API/UI/Compose/Widget/ListItem/README.md) singleLineSecondaryText(boolean value)

参数:

+ boolean value - true表示辅助文本显示为单行,false表示不显示为单行

返回值:

+ [ListItem](/API/UI/Compose/Widget/ListItem/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [ListItem.singleLineSecondaryText()](/API/UI/Compose/Widget/ListItem/README.md?id=singleLineSecondaryText)
  方法设置列表项辅助文本是否为单行

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.ListItem() 用于创建 ListItem 可组合项
    ListItem {
        // delegate -> ListItem
        // ListItem.singleLineSecondaryText() 用于设置列表项辅助文本是否为单行
        singleLineSecondaryText(true)
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