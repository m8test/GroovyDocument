功能:

+ 设置抽屉海拔

定义:

+ [Scaffold](/API/UI/Compose/Widget/Scaffold/README.md) drawerElevation(Number elevation)

参数:

+ Number elevation - 需要设置的海拔,单位dp

返回值:

+ [Scaffold](/API/UI/Compose/Widget/Scaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [Scaffold.drawerElevation()](/API/UI/Compose/Widget/Scaffold/README.md?id=drawerElevation) 方法设置抽屉海拔

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.Scaffold() 用于创建 Scaffold 可组合项
    Scaffold {
        // delegate -> Scaffold
        // Scaffold.drawerElevation() 用于设置抽屉海拔
        drawerElevation(20)
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