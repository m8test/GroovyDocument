功能:

+ 设置 [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md)

定义:

+ [AsyncImage](/API/UI/Compose/Widget/AsyncImage/README.md)
  colorFilter([ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) colorFilter)

参数:

+ [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) colorFilter -
  需要设置的 [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) 对象

返回值:

+ [AsyncImage](/API/UI/Compose/Widget/AsyncImage/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [AsyncImage.colorFilter()](/API/UI/Compose/Widget/AsyncImage/README.md?id=colorFilter)
  方法设置 [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md)

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.AsyncImage() 用于创建 AsyncImage 可组合项
    AsyncImage {
        // delegate -> AsyncImage
        // ColorFilters.tint() 用于创建 ColorFilter 对象
        def cf = $colorFilters.tint({
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }, "SrcIn")
        // AsyncImage.colorFilter() 用于设置 ColorFilter
        colorFilter(cf)
        // AsyncImage.request() 用于设置图片请求
        request {
            // delegate -> ImageRequest
            def resources = $applicationContext.getResources()
            // ImageRequest.drawable() 用于设置从 Drawable 中读取图片
            drawable(resources.getDrawable(resources.getIdentifier("ic_baseline_android_24", "drawable", $applicationContext.getPackageName())))
            // ImageRequest.format() 用于设置图片格式
            format("svg")
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