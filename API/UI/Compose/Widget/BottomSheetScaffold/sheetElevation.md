功能:

+ 设置底页海拔

定义:

+ [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) sheetElevation(Number
  elevation)

参数:

+ Number elevation - 需要设置的海拔,单位dp

返回值:

+ [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BottomSheetScaffold.sheetElevation()](/API/UI/Compose/Widget/BottomSheetScaffold/README.md?id=sheetElevation)
  方法设置底页海拔

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.BottomSheetScaffold() 用于创建 BottomSheetScaffold 可组合项
    BottomSheetScaffold {
        // delegate -> BottomSheetScaffold
        // BottomSheetScaffold.sheetElevation() 用于设置底页海拔
        sheetElevation(20)
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