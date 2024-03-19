功能:

+ 设置从 [Drawable](https://developer.android.google.cn/reference/android/graphics/drawable/Drawable)
  中读取图片

定义:

+ [ImageRequest](/API/UI/Compose/Widget/AsyncImage/ImageRequest/README.md)
  drawable([Drawable](https://developer.android.google.cn/reference/android/graphics/drawable/Drawable)
  drawable)

参数:

+ [Drawable](https://developer.android.google.cn/reference/android/graphics/drawable/Drawable)
  drawable -
  安卓 [Drawable](https://developer.android.google.cn/reference/android/graphics/drawable/Drawable) 对象

返回值:

+ [ImageRequest](/API/UI/Compose/Widget/AsyncImage/ImageRequest/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [ImageRequest.drawable()](/API/UI/Compose/Widget/AsyncImage/ImageRequest/README.md?id=drawable) 方法设置从
  [Drawable](https://developer.android.google.cn/reference/android/graphics/drawable/Drawable) 中读取图片

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.AsyncImage() 用于创建 AsyncImage 可组合项
    AsyncImage {
        // delegate -> AsyncImage
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