功能:

+ 设置可组合项的 [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) .

定义1:

+ [Composable](/API/UI/Compose/Widget/Composable/README.md) modifier(Closure modifier)

参数1:

+ Closure modifier - 配置 [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) 的闭包
    + 参数 - 无
    + delegate - [Modifier](/API/UI/Compose/Modifier/Modifier/README.md)

定义2:

+ [Composable](/API/UI/Compose/Widget/Composable/README.md)
  modifier([Modifier](/API/UI/Compose/Modifier/Modifier/README.md) modifier)

参数2:

+ [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) modifier -
  需要设置的 [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) 对象

返回值:

+ [Composable](/API/UI/Compose/Widget/Composable/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Composable.modifier()](/API/UI/Compose/Widget/Composable/README.md?id=modifier) 方法设置
  [Text](/API/UI/Compose/Widget/Text/README.md) 可组合项的 [Modifier](/API/UI/Compose/Modifier/Modifier/README.md) .

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.newModifier() 用于创建 Modifier
    def reusedModifier = newModifier {
        // delegate -> Modifier
        // Modifier.background() 用于设置背景颜色
        background({
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }) {
            // delegate -> Shape
            // 不配置Shape默认为矩形
        }
    }
    // Slot.Column() 用于创建纵向布局
    Column {
        // delegate -> Column
        // Column.content() 用于设置布局内容
        content {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Composable.modifier() 用于配置可组合项的 Modifier ,因为 Text 可组合项继承自 Composable ,所以可以调用 modifier 方法
                modifier(reusedModifier)
                // Composable.modifier() 用于配置可组合项的 Modifier ,因为 Text 可组合项继承自 Composable ,所以可以调用 modifier 方法
                modifier {
                    // delegate -> Modifier
                    // Modifier.alpha() 用于设置透明度
                    alpha(0.5f)
                }
                // Text.text() 用于设置文本可组合项内容
                text("red background")
            }
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Composable.modifier() 用于配置可组合项的 Modifier ,因为 Text 可组合项继承自 Composable ,所以可以调用 modifier 方法
                modifier(reusedModifier)
                // Composable.modifier() 用于配置可组合项的 Modifier ,因为 Text 可组合项继承自 Composable ,所以可以调用 modifier 方法
                modifier {
                    // delegate -> Modifier
                    // Modifier.alpha() 用于设置透明度
                    alpha(0.8f)
                }
                // Text.text() 用于设置文本可组合项内容
                text("red background")
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