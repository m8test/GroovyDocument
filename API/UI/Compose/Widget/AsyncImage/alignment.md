功能:

+ 设置图片对齐方式

定义:

+ [AsyncImage](/API/UI/Compose/Widget/AsyncImage/README.md)  alignment(String alignment)

参数:

+ String alignment - 内容对其方式,可选值有
    + Center - 居中对齐
    + CenterStart - 左居中对齐
    + CenterEnd - 右居中对齐
    + TopCenter - 上居中对齐
    + TopStart - 左上对齐
    + TopEnd - 右上对齐
    + BottomCenter - 下居中对齐
    + BottomEnd - 右下对齐
    + BottomStart - 右下对齐

返回值:

+ [AsyncImage](/API/UI/Compose/Widget/AsyncImage/README.md)  - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [AsyncImage.alignment()](/API/UI/Compose/Widget/AsyncImage/README.md?id=alignment)
  方法设置图片对齐方式.

```groovy
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.AsyncImage() 用于创建 AsyncImage 可组合项
    AsyncImage {
        // delegate -> AsyncImage
        // AsyncImage.modifier() 用于修饰 Composable,Surface 继承自 Composable
        modifier {
            // delegate -> Modifier
            // Modifier.fillMaxSize() 用于设置填充父可组合项宽度和高度, 参数为填充父可组合项的比例, 取值区间为 0.0f-1.0f
            fillMaxSize(1.0f)
        }
        // AsyncImage.request() 用于设置图片请求
        request {
            // delegate -> ImageRequest
            // ImageRequest.url() 用于设置从指定url获取图片
            url("https://upload.wikimedia.org/wikipedia/en/4/41/Flag_of_India.svg")
            // ImageRequest.format() 用于设置图片格式
            format("svg")
        }
        // AsyncImage.alignment() 用于设置图片对齐方式
        alignment("Center")
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