功能:

+ 设置图片内容缩放方式

定义:

+ [AsyncImage](/API/UI/Compose/Widget/AsyncImage/README.md)  contentScale(String contentScale)

参数:

+ String contentScale - 内容缩放方式,可选值有 Crop - 统一缩放源（保持源的宽高比），以便源的两个维度（宽度和高度）将等于或大于目标的相应维度。 None -
  不要对源应用任何缩放 FillBounds - 不均匀地水平和垂直缩放以填充目标边界。 FillHeight - 缩放保持纵横比的源，使边界与目标高度匹配。
  如果高度大于宽度，这可以覆盖比目的地更大的区域。 FillWidth - 缩放保持纵横比的源，使边界与目标宽度匹配。 如果宽度大于高度，这可以覆盖比目的地更大的区域。 Fit -
  统一缩放源（保持源的纵横比），使源的两个维度（宽度和高度）等于或小于目标的相应维度. Inside - 如果源大于目标，则缩放源以将纵横比保持在目标范围内。
  如果源在两个维度上都小于或等于目标，则其行为类似于 None。 这将始终包含在目标范围内。

返回值:

+ [AsyncImage](/API/UI/Compose/Widget/AsyncImage/README.md)  - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [AsyncImage.contentScale()](/API/UI/Compose/Widget/AsyncImage/README.md?id=contentScale)
  方法设置图片内容缩放方式.

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
            // ImageRequest.url() 用于设置从指定url获取图片
            url("https://upload.wikimedia.org/wikipedia/en/4/41/Flag_of_India.svg")
            // ImageRequest.format() 用于设置图片格式
            format("svg")
        }
        // AsyncImage.contentScale() 用于设置图片内容缩放方式
        contentScale("None")
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