功能:

+ 设置前层形状.

定义:

+ [BackdropScaffold](/API/UI/Compose/Widget/BackdropScaffold/README.md) frontLayerShape(Closure closure)

参数:

+ Closure closure - 设置前层形状的闭包
    + 参数 - 无
    + delegate - [Shape](/API/UI/Compose/Theme/Shape/Shape/README.md)

返回值:

+ [BackdropScaffold](/API/UI/Compose/Widget/BackdropScaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BackdropScaffold.frontLayerShape()](/API/UI/Compose/Widget/BackdropScaffold/README.md?id=frontLayerShape)
  方法设置前层形状.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.BackdropScaffold() 用于创建 BackdropScaffold 可组合项
    BackdropScaffold {
        // delegate -> BackdropScaffold
        // BackdropScaffold.frontLayerShape() 用于设置前层形状
        frontLayerShape {
            // delegate -> Shape
            // Shape.all() 用于设置四个角尺寸
            all(20, "dp")
            // Shape.cutCorner() 用于设置角的类型为切角
            cutCorner()
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