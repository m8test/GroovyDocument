功能:

+ 设置从指定文件获取图片

定义:

+ [ImageRequest](/API/UI/Compose/Widget/AsyncImage/ImageRequest/README.md)
  file([ScriptFile](/API/File/ScriptFile/README.md) file)

参数:

+ [ScriptFile](/API/File/ScriptFile/README.md) file - 图片文件

返回值:

+ [ImageRequest](/API/UI/Compose/Widget/AsyncImage/ImageRequest/README.md) - 返回对象本身方便链式调用

示例代码:

+ 启动一个Activity, 并通过 [ImageRequest.file()](/API/UI/Compose/Widget/AsyncImage/ImageRequest/README.md?id=file)
  方法设置从指定文件获取图片

```groovy
// 新建一个Http客户端, HttpClientManager.newClient() 用于创建一个Http客户端
def client = $httpClientManager.newClient()
// HttpClient.request() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.request("https://upload.wikimedia.org/wikipedia/en/4/41/Flag_of_India.svg") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "get"
}
// HttpClientResponse.bytesBody() 可以将服务器返回结果转成字节数组
def bytesBody = response.bytesBody()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    path("/sdcard/image_request.svg")
}
// ScriptFile.writeBytes() 可以向文件中写入字节数组
scriptFile.writeBytes(bytesBody)
// ComposeActivity.createView() 用于创建用户界面
$composeActivity.createView {
    // delegate -> Slot
    // Slot.AsyncImage() 用于创建 AsyncImage 可组合项
    AsyncImage {
        // delegate -> AsyncImage
        // AsyncImage.request() 用于设置图片请求
        request {
            // delegate -> ImageRequest
            // ImageRequest.file() 用于设置从指定文件获取图片
            file(scriptFile)
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