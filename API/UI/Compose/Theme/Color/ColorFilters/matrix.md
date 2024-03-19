功能:

+ 创建一个通过 4x5 颜色矩阵转换颜色的 [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) 对象。此滤镜可用于更改像素的饱和度，从
  YUV 转换为 RGB 等。

定义:

+ [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) matrix(List\<Float\> matrix)

参数:

+ List\<Float\> matrix - 矩阵数组

返回值:

+ [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) -
  新创建的 [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) 对象

示例代码:

+ 启动一个Activity, 并通过 [ColorFilters.matrix()](/API/UI/Compose/Theme/Color/ColorFilters/README.md?id=matrix)
  方法创建一个通过 4x5 颜色矩阵转换颜色的 [ColorFilter](/API/UI/Compose/Theme/Color/ColorFilter/README.md) 对象

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.AsyncImage() 用于创建 AsyncImage 可组合项
    AsyncImage {
        // delegate -> AsyncImage
        // ColorFilters.matrix() 用于创建一个通过 4x5 颜色矩阵转换颜色的 ColorFilter 对象
        def cf = $colorFilters.matrix([
                -1f, 0f, 0f, 0f, 255f, //R通道：-1xR+255=255-R, 取反
                0f, -1f, 0f, 0f, 255f, //G通道：-1xG+255=255-G, 取反
                0f, 0f, -1f, 0f, 255f, //B通道：-1xB+255=255-B, 取反
                0f, 0f, 0f, 1f, 0f
        ])
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