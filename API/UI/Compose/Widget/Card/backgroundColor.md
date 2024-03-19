功能:

+ 设置卡片背景颜色.

定义:

+ [Card](/API/UI/Compose/Widget/Card/README.md) backgroundColor(Closure closure)

参数:

+ Closure closure - 设置颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [Card](/API/UI/Compose/Widget/Card/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Card.backgroundColor()](/API/UI/Compose/Widget/Card/README.md?id=backgroundColor)
  方法设置卡片背景颜色.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Card() 用于创建 Card 可组合项
    Card {
        // delegate -> Card
        // Card.backgroundColor() 用于设置卡片背景颜色
        backgroundColor {
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }
        // Card.content() 用于设置卡片内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.text() 用于设置文本可组合项内容
                text("Card")
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