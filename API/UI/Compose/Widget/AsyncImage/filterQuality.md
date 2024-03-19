功能:

+ 设置位图缩放并绘制到目标位置时应用于位图的采样算法。

定义:

+ [AsyncImage](/API/UI/Compose/Widget/AsyncImage/README.md)  filterQuality(String filterQuality)

参数:

+ String filterQuality - 采样算法,可选值有:
    + None - 尽可能快的过滤，尽管也是最低的质量通常这意味着最近邻过滤。
    + Low - 质量比None好,比Medium快。 通常这意味着双线性插值。
    + Medium - 质量比 Low 好，比 High 快。 通常这意味着双线性插值和金字塔参数预过滤 (mipmap) 的组合。
    + High - 最好的质量过滤，尽管也是最慢的。 通常这意味着双三次插值或更好。

返回值:

+ [AsyncImage](/API/UI/Compose/Widget/AsyncImage/README.md)  - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity,
  并通过 [AsyncImage.filterQuality()](/API/UI/Compose/Widget/AsyncImage/README.md?id=filterQuality)
  方法设置图片内容缩放方式位图缩放并绘制到目标位置时应用于位图的采样算法。

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
        contentScale("Crop")
        // AsyncImage.filterQuality() 用于设置位图缩放并绘制到目标位置时应用于位图的采样算法。
        filterQuality("High")
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