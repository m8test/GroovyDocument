功能:

+ 设置前层是否应与后层的高度一致

定义:

+ [BackdropScaffold](/API/UI/Compose/Widget/BackdropScaffold/README.md) stickyFrontLayer(boolean value)

参数:

+ boolean value - true表示前层应与后层的高度一致,false表示前层不应与后层的高度一致

返回值:

+ [BackdropScaffold](/API/UI/Compose/Widget/BackdropScaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BackdropScaffold.stickyFrontLayer()](/API/UI/Compose/Widget/BackdropScaffold/README.md?id=stickyFrontLayer)
  方法设置前层是否应与后层的高度一致.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.BackdropScaffold() 用于创建 BackdropScaffold 可组合项
    BackdropScaffold {
        // delegate -> BackdropScaffold
        // BackdropScaffold.stickyFrontLayer() 用于设置前层是否应与后层的高度一致
        stickyFrontLayer(false)
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