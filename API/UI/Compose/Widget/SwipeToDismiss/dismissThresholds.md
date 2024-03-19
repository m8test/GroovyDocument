功能:

+ 设置 [SwipeToDismiss](/API/UI/Compose/Widget/SwipeToDismiss/README.md) 需要被刷过才能被关闭的阈值

定义:

+ [SwipeToDismiss](/API/UI/Compose/Widget/SwipeToDismiss/README.md) dismissThresholds(String direction,
  Closure closure)

参数:

+ String direction - 滑动方向,可选值有
    + StartToEnd - 从左到右
    + EndToStart - 从右到左
+ Closure closure - 设置阈值的闭包
    + 参数 - 无
    + delegate - [ThresholdConfig](/API/UI/Compose/Widget/SwipeToDismiss/ThresholdConfig/README.md)

返回值:

+ [SwipeToDismiss](/API/UI/Compose/Widget/SwipeToDismiss/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [SwipeToDismiss.dismissThresholds()](/API/UI/Compose/Widget/SwipeToDismiss/README.md?id=dismissThresholds)
  方法设置 [SwipeToDismiss](/API/UI/Compose/Widget/SwipeToDismiss/README.md) 需要被刷过才能被关闭的阈值

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.SwipeToDismiss() 用于创建 SwipeToDismiss 可组合项
    SwipeToDismiss {
        // delegate -> SwipeToDismiss
        // SwipeToDismiss.dismissThresholds() 用于设置 SwipeToDismiss 需要被刷过才能被关闭的阈值
        dismissThresholds("StartToEnd") {
            // delegate -> ThresholdConfig
            // ThresholdConfig.fractionalThreshold() 用于设置百分比阈值
            fractionalThreshold(0.5f)
        }
        // SwipeToDismiss.background() 用于设置 SwipeToDismiss 背景
        background {
            // delegate -> Slot
            // Slot.Box() 用于创建 Box 可组合项
            Box {
                // delegate -> Box
                // Box.modifier() 用于修饰 Composable
                modifier {
                    // delegate -> Modifier
                    // Modifier.fillMaxSize() 用于设置填充最大宽度
                    fillMaxSize(1.0f)
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
            }
        }
        // SwipeToDismiss.dismissContent() 用于设置 SwipeToDismiss 可取消内容
        dismissContent {
            // delegate -> Slot
            // Slot.Row() 用于创建 Row 可组合项
            Row {
                // delegate -> Row
                // Row.content() 用于设置行内容
                content {
                    // delegate -> Slot
                    // Slot.Text() 用于创建文本可组合项
                    Text {
                        // delegate -> Text
                        // Text.text() 用于设置文本可组合项内容
                        text("SwipeToDismiss")
                    }
                }
                // Row.modifier() 用于修饰 Composable
                modifier {
                    // delegate -> Modifier
                    // Modifier.fillMaxWidth() 用于设置填充最大宽度
                    fillMaxWidth(1.0f)
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