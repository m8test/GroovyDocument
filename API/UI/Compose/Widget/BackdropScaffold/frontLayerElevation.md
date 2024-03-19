功能:

+ 设置前层海拔.

定义:

+ [BackdropScaffold](/API/UI/Compose/Widget/BackdropScaffold/README.md) frontLayerElevation(Number
  elevation)

参数:

+ Number elevation - 需要设置的海拔,单位dp

返回值:

+ [BackdropScaffold](/API/UI/Compose/Widget/BackdropScaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BackdropScaffold.frontLayerElevation()](/API/UI/Compose/Widget/BackdropScaffold/README.md?id=frontLayerElevation)
  方法设置前层海拔.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.BackdropScaffold() 用于创建 BackdropScaffold 可组合项
    BackdropScaffold {
        // delegate -> BackdropScaffold
        // BackdropScaffold.frontLayerElevation() 用于设置前层海拔
        frontLayerElevation(20)
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