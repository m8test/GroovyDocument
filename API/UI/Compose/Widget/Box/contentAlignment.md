功能:

+ 设置 [Box](/API/UI/Compose/Widget/Box/README.md) 内容对齐方式

定义:

+ [Box](/API/UI/Compose/Widget/Box/README.md) contentAlignment(String alignment)

参数:

+ String alignment - 内容对其方式,可选值有
    + Center - 居中对齐
    + CenterStart - 左居中对齐
    + CenterEnd - 右居中对齐
    + TopCenter - 上居中对齐
    + TopStart - 左上对齐
    + TopEnd - 右上对齐
    + BottomCenter - 下居中对齐
    + BottomEnd - 右下对齐
    + BottomStart - 右下对齐

返回值:

+ [Box](/API/UI/Compose/Widget/Box/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Box.contentAlignment()](/API/UI/Compose/Widget/Box/README.md?id=contentAlignment)
  方法设置 [Box](/API/UI/Compose/Widget/Box/README.md) 内容对齐方式.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Box() 用于创建 Box 可组合项
    Box {
        // delegate -> Box
        // Box.contentAlignment() 用于设置 Box 内容对齐方式
        contentAlignment("Center")
        // Box.modifier() 用于修饰 Composable
        modifier {
            // delegate -> Modifier
            // Modifier.height() 用于设置盒子高度
            height(250)
            // Modifier.width() 用于设置盒子宽度
            width(250)
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
        // Box.content() 用于设置 Box 内容
        content {
            // delegate -> Slot
            // Slot.Box() 用于创建 Box 可组合项
            Box {
                // delegate -> Box
                // Box.modifier() 用于修饰 Composable
                modifier {
                    // delegate -> Modifier
                    // Modifier.height() 用于设置盒子高度
                    height(150)
                    // Modifier.width() 用于设置盒子宽度
                    width(150)
                    // Modifier.background() 用于设置背景颜色
                    background({
                        // delegate -> Color
                        // Color.green() 用于配置绿色通道
                        green(255)
                    }) {
                        // delegate -> Shape
                        // 不配置Shape默认为矩形
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