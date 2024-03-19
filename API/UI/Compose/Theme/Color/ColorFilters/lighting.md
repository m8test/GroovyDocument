功能:

+ 创建一个可用于模拟简单光照效果的 [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md)
  对象。照明 [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) 由两个参数定义，一个用于与源颜色相乘，一个用于添加到源颜色

定义:

+ [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) lighting(Closure multiply, Closure add)

参数:

+ Closure multiply - 用于设置与源颜色相乘颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)
+ Closure add - 用于设置与源颜色相加颜色的闭包
    + 参数 - 无
    + delegate - [Color](/API/UI/Compose/Theme/Color/Color/README.md)

返回值:

+ [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) -
  新创建的 [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) 对象

示例代码:

+ 启动一个Activity,
  并通过 [ColorFilters.lighting()](/API/UI/Compose/Theme/Color/ColorFilters/README.md?id=lighting)
  方法创建一个可用于模拟简单光照效果的 [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) 对象

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.AsyncImage() 用于创建 AsyncImage 可组合项
    AsyncImage {
        // delegate -> AsyncImage
        // ColorFilters.lighting() 用于创建一个可用于模拟简单光照效果的 ColorFilter 对象
        def cf = $colorFilters.lighting({
            // delegate -> Color
            // Color.red() 用于配置红色通道
            red(255)
        }) {
            // delegate -> Color
            // Color.blue() 用于配置蓝色通道
            blue(255)
        }
        // AsyncImage.colorFilter() 用于设置 ColorFilter
        colorFilter(cf)
        // AsyncImage.request() 用于设置图片请求
        request {
            // delegate -> ImageRequest
            // ImageRequest.url() 用于设置从指定url获取图片
            url("https://bkimg.cdn.bcebos.com/pic/cb8065380cd791230de06aa4a8345982b3b780da?x-bce-process=image/watermark,image_d2F0ZXIvYmFpa2UxMTY=,g_7,xp_5,yp_5")
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