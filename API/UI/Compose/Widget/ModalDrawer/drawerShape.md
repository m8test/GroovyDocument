功能:

+ 设置 [ModalDrawer](/API/UI/Compose/Widget/ModalDrawer/README.md) 抽屉形状

定义:

+ [ModalDrawer](/API/UI/Compose/Widget/ModalDrawer/README.md) drawerShape(Closure closure)

参数:

+ Closure closure - 设置 [ModalDrawer](/API/UI/Compose/Widget/ModalDrawer/README.md) 抽屉形状的闭包
    + 参数 - 无
    + delegate - [Shape](/API/UI/Compose/Theme/Shape/Shape/README.md)

返回值:

+ [ModalDrawer](/API/UI/Compose/Widget/ModalDrawer/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [ModalDrawer.drawerShape()](/API/UI/Compose/Widget/ModalDrawer/README.md?id=drawerShape)
  方法设置 [ModalDrawer](/API/UI/Compose/Widget/ModalDrawer/README.md) 抽屉形状

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.ModalDrawer() 用于创建 ModalDrawer 可组合项
    ModalDrawer {
        // delegate -> ModalDrawer
        // ModalDrawer.drawerContent() 用于设置 ModalDrawer 抽屉内容
        drawerContent {
            // delegate -> Slot
            // Slot.Text() 用于创建文本可组合项
            Text {
                // delegate -> Text
                // Text.modifier() 用于修饰 Composable
                modifier {
                    // delegate -> Modifier
                    // Modifier.padding() 用于设置边距
                    padding {
                        // delegate -> PaddingValues
                        // PaddingValues.all() 用于同时设置上下左右四个方向边距
                        all(20)
                    }
                }
                // Text.text() 用于设置文本可组合项内容
                text("ModalDrawer抽屉内容")
            }
        }
        // ModalDrawer.drawerShape() 用于设置 ModalDrawer 抽屉形状
        drawerShape {
            // delegate -> Shape
            // Shape.all() 用于设置四个角尺寸
            all(20, "dp")
            // Shape.roundedCorner() 用于设置角的类型为圆角
            roundedCorner()
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