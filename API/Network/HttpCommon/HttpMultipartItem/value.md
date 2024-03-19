功能:

+ 获取当前part的值.

定义:

+ String|byte[] value()

参数:

+ 无

返回值:

+ String|byte[] - 如果当前part为文本则返回 String ;如果当前par为文件类型则返回 byte[] .

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpMultipartItem.value()](/API/Network/HttpCommon/HttpMultipartItem/README.md?id=value)
  获取当前part的值.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 在8080端口新建一个服务器
def server = $httpServerManager.newServer(8080) {
    // delegate -> HttpServerConfig
    // HttpServerConfig.routing() 用于配置服务器路由信息
    routing {
        // delegate -> HttpServerRouting
        // HttpServerRouting.post() 用于配置Post路由
        post("/value") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/value"
            def path = request.path()
            $assert.assertTrue(path == "/value")
            $console.log("Path->$path")
            // HttpServerRequest.multipartBody() 可以接收multipart类型的数据, 返回值类型为 List<HttpMultipartItem>
            def multipart = request.multipartBody()
            // 遍历所有数据
            multipart.each {
                // it -> HttpMultipartItem
                if (it.isFile()) {
                    // HttpMultipartItem.name() 可以获取数据名,也就是 Content-Disposition 请求头的 name 属性
                    $assert.assertTrue(it.name() == "filePartName", "文件数据name的值")
                    // HttpMultipartItem.value() 可以获取 name 对应的值, 此处为二进制数据(byte[]), 可以保存到文件中
                    def value = it.value()
                    def partItem = it
                    // Files.buildFile() 用于构建一个 ScriptFile 对象
                    def scriptFile = $files.buildFile {
                        // delegate -> FileBuilder
                        // FileBuilder.path() 用于设置文件路径
                        delegate.path("/sdcard/${partItem.filename()}")
                    }
                    // ScriptFile.writeBytes() 可以向文件中写入字节数据
                    scriptFile.writeBytes(value)
                } else {
                    // HttpMultipartItem.name() 可以获取数据名,也就是 Content-Disposition 请求头的 name 属性
                    $assert.assertTrue(it.name() == "textPartName", "文本数据name的值")
                    // HttpMultipartItem.value() 可以获取 name 对应的值,此处为 String 类型
                    $assert.assertTrue(it.value() == "textPartValue", "文本数据name对应的值")
                }
            }
            // HttpServerCall.response() 可以获取响应对应HttpServerResponse
            def response = response()
            // HttpServerResponse.textBody() 可以发送文本到客户端
            response.textBody(path)
        }
    }
}
// HttpServer.start() 用于启动服务器,如果端口已经被占用了则会启动失败,报错 "Address already in use"
server.start()
// 新建一个Http客户端, HttpClientManager.newClient() 用于创建一个Http客户端
def client = $httpClientManager.newClient()
// HttpClient.postMultipart() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.postMultipart("http://localhost:8080/value", {
    // delegate -> HttpClientMultipart
    // HttpClientMultipart.text() 用于添加文本类型的part
    text("textPartName", "textPartValue")
    // Files.buildFile() 用于构建一个 ScriptFile 对象
    def scriptFile = $files.buildFile {
        // delegate -> FileBuilder
        // FileBuilder.path() 用于设置文件路径
        delegate.path("/sdcard/test_http_multipart_item_value.txt")
    }
    // ScriptFile.writeText() 可以向文件中写入内容
    scriptFile.writeText("Hello http_multipart_item_value")
    // HttpClientMultipart.file() 用于添加文件类型的part
    file("filePartName", scriptFile, "custom_filename_test_http_multipart_item_value.txt")
})
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/value"
$assert.assertTrue(textResult == "/value", "返回结果为 /value")
// HttpServer.stop() 用于停止服务器.
server.stop()
```