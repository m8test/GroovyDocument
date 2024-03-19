功能:

+ 设置抽屉形状

定义:

+ [Scaffold](/API/UI/Compose/Widget/Scaffold/README.md) drawerShape(Closure closure)

参数:

+ Closure closure - 设置抽屉形状的闭包
    + 参数 - 无
    + delegate - [Shape](/API/UI/Compose/Theme/Shape/Shape/README.md)

返回值:

+ [Scaffold](/API/UI/Compose/Widget/Scaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [Scaffold.drawerShape()](/API/UI/Compose/Widget/Scaffold/README.md?id=drawerShape)
  方法设置抽屉形状

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Scaffold() 用于创建 Scaffold 可组合项
    Scaffold {
        // delegate -> Scaffold
        // Scaffold.drawerShape() 用于设置抽屉形状
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