功能:

+ 将内容剪裁成指定形状

定义:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) clip(Closure closure)

参数:

+ Closure closure - 配置形状的闭包
    + 参数 - 无
    + delegate - [Shape](/API/UI/Compose/Theme/Shape/Shape/README.md)

返回值:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Modifier.clip()](/API/UI/Compose/Modifier/Modifier/README.md?id=clip) 方法将内容剪裁成指定形状.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Column() 用于创建纵向布局
    Column {
        // delegate -> Column
        // Column.content() 用于设置布局内容
        content {
            // delegate -> Slot
            // Slot.Button() 用于创建 Button 可组合项
            Button {
                // delegate -> Button
                // Composable.modifier() 用于配置可组合项的 Modifier ,因为 Text 可组合项继承自 Composable ,所以可以调用 modifier 方法
                modifier {
                    // delegate -> Modifier
                    // Modifier.clip() 用于将内容剪裁成指定形状
                    clip {
                        // delegate -> Shape
                        // Shape.all() 用于设置四个角尺寸
                        all(25, "dp")
                        // Shape.roundedCorner() 用于设置角的类型为圆角
                        roundedCorner()
                    }
                }
                // Button.content() 用于设置按钮内容
                content {
                    // delegate -> Slot
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        // Text.text() 用于设置文本可组合项内容
                        text("Text")
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