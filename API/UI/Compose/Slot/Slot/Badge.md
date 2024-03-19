功能:

+ 创建 [Badge](/API/UI/Compose/Widget/Badge/README.md) 可组合项

定义:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) Badge(Closure closure)

参数:

+ Closure closure - 设置 [Badge](/API/UI/Compose/Widget/Badge/README.md) 的闭包
    + 参数 - 无
    + delegate - [Badge](/API/UI/Compose/Widget/Badge/README.md)

返回值:

+ [Slot](/API/UI/Compose/Slot/Slot/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Slot.Badge()](/API/UI/Compose/Slot/Slot/README.md?id=Badge)
  方法创建 [Badge](/API/UI/Compose/Widget/Badge/README.md) 可组合项.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Column() 用于创建 Column 可组合项
    Column {
        // delegate -> Column
        // Column.modifier() 用于修饰 Composable
        modifier {
            // delegate -> Modifier
            // Modifier.fillMaxSize() 用于设置填充父可组合项宽度和高度, 参数为填充父可组合项的比例, 取值区间为 0.0f-1.0f
            fillMaxSize(1.0f)
        }
        // Column.verticalArrangement() 用于设置垂直方向排列方式
        verticalArrangement("Center")
        // Column.horizontalAlignment() 用于设置水平方向对齐方式
        horizontalAlignment("CenterHorizontally")
        // Column.content() 用于设置 Column 可组合项中的内容
        content {
            // delegate -> Slot
            // Slot.BadgedBox() 用于创建 BadgedBox 可组合项
            BadgedBox {
                // delegate -> BadgedBox
                // BadgedBox.badge() 用于设置 Badge
                badge {
                    // delegate -> Slot
                    // Slot.Badge() 用于创建 Badge 可组合项
                    Badge {
                        // delegate -> Badge
                        // Badge.content() 用于设置 Badge 内容
                        content {
                            // Slot.Text() 用于创建文本可组合项
                            Text {
                                // delegate -> Text
                                // Text.text() 用于设置文本可组合项内容
                                text("99+")
                            }
                        }
                    }
                }
                // BadgedBox.content() 用于设置 BadgedBox 内容
                content {
                    // delegate -> Slot
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        // Text.text() 用于设置文本可组合项内容
                        text("消息")
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