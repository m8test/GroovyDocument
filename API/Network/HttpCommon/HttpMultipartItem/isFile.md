功能:

+ 判断当前part是否为文件.

定义:

+ boolean isFile()

参数:

+ 无

返回值:

+ boolean - 如果当前part为文件返回true,否则返回false

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpMultipartItem.isFile()](/API/Network/HttpCommon/HttpMultipartItem/README.md?id=isFile)
  判断当前part是否为文件.

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
        post("/isFile") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/isFile"
            def path = request.path()
            $assert.assertTrue(path == "/isFile")
            $console.log("Path->$path")
            // HttpServerRequest.multipartBody() 可以接收multipart类型的数据, 返回值类型为 List<HttpMultipartItem>
            def multipart = request.multipartBody()
            // 遍历所有数据
            multipart.each {
                // it -> HttpMultipartItem
                // HttpMultipartItem.isFile() 用于判断当前part是否为文件.
                if (it.isFile()) {
                    $console.log("文件类型:${it.name()}")
                } else {
                    $console.log("文本类型:${it.name()}")
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
def response = client.postMultipart("http://localhost:8080/isFile", {
    // delegate -> HttpClientMultipart
    // HttpClientMultipart.text() 用于添加文本类型的part
    text("textPartName", "textPartValue")
    // Files.buildFile() 用于构建一个 ScriptFile 对象
    def scriptFile = $files.buildFile {
        // delegate -> FileBuilder
        // FileBuilder.path() 用于设置文件路径
        delegate.path("/sdcard/test_http_multipart_item_isFile.txt")
    }
    // ScriptFile.writeText() 可以向文件中写入内容
    scriptFile.writeText("Hello HttpMultipartItem.filename()")
    // HttpClientMultipart.file() 用于添加文件类型的part
    file("filePartName", scriptFile, "custom_filename_test_http_multipart_item_isFile.txt")
})
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/isFile"
$assert.assertTrue(textResult == "/isFile", "返回结果为 /isFile")
// HttpServer.stop() 用于停止服务器.
server.stop()
```