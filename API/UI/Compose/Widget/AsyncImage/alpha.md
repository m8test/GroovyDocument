功能:

+ 设置图片透明度

定义:

+ [AsyncImage](/API/UI/Compose/Widget/AsyncImage/README.md) alpha(float alpha)

参数:

+ float alpha - 透明度,区间为0.0-1.0

返回值:

+ [AsyncImage](/API/UI/Compose/Widget/AsyncImage/README.md)  - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [AsyncImage.alpha()](/API/UI/Compose/Widget/AsyncImage/README.md?id=alpha) 方法设置图片透明度.

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
        // AsyncImage.alpha() 用于设置图片透明度
        alpha(0.5f)
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