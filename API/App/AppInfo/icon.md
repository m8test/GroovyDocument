功能:

+ 获取 App 图标

定义:

+ [Drawable](https://developer.android.google.cn/reference/android/graphics/drawable/Drawable)
  icon()

参数:

+ 无

返回值:

+ [Drawable](https://developer.android.google.cn/reference/android/graphics/drawable/Drawable) - App
  图标

示例代码:

+ 通过 [AppInfo.icon()](/API/App/AppInfo/README.md?id=icon) 获取 App 图标

```groovy
// App.info() 用于获取 App 信息
def appInfo = $app.info("com.m8test.main")
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.AsyncImage() 用于创建 AsyncImage 可组合项
    AsyncImage {
        // delegate -> AsyncImage
        // AsyncImage.request() 用于设置图片请求
        request {
            // AppInfo.icon() 用于获取 App 图标
            def icon = appInfo.icon()
            // delegate -> ImageRequest
            drawable(icon)
            // ImageRequest.format() 用于设置图片格式
            format("Png")
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