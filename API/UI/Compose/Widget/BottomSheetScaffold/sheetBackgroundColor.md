功能:

+ 设置 [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) 底页背景颜色

定义:

+ [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) sheetBackgroundColor(Closure
  closure)

参数:

+ Closure closure - 设置 [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) 底页背景颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [BottomSheetScaffold.sheetBackgroundColor()](/API/UI/Compose/Widget/BottomSheetScaffold/README.md?id=sheetBackgroundColor)
  方法设置 [BottomSheetScaffold](/API/UI/Compose/Widget/BottomSheetScaffold/README.md) 底页背景颜色

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.BottomSheetScaffold() 用于创建 BottomSheetScaffold 可组合项
    BottomSheetScaffold {
        // delegate -> BottomSheetScaffold
        // BottomSheetScaffold.sheetBackgroundColor() 用于设置BottomSheetScaffold 底页背景颜色
        sheetBackgroundColor {
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
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