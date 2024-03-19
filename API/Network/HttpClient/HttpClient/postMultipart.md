功能:

+ 发送Http Post请求,Content-Type 默认为 multipart/form-data

定义:

+ [HttpClientResponse](/API/Network/HttpClient/HttpClientResponse/README.md) postMultipart(String
  url, Closure multipartBuilder = null, Closure requestBuilder = null)

参数:

+ String url - 请求的url路径
+ Closure multipartBuilder - Multipart类型请求体构建闭包
    + 参数 - 无
    + delegate -
      [HttpClientMultipart](/API/Network/HttpClient/HttpClientMultipart/README.md)
+ Closure requestBuilder - 对Http请求配置的闭包
    + 参数 - 无
    + delegate -
      [HttpClientRequest](/API/Network/HttpClient/HttpClientRequest/README.md)

返回值:

+ [HttpClientResponse](/API/Network/HttpClient/HttpClientResponse/README.md) - Http响应信息封装的对象

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpClient.postMultipart()](/API/Network/HttpClient/HttpClient/README.md?id=postMultipart)
  方法访问该服务器.

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
        post("/postMultipart") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/postMultipart"
            def path = request.path()
            $assert.assertTrue(path == "/postMultipart")
            $console.log("Path->$path")
            // HttpServerRequest.multipartBody() 可以接收multipart类型的数据, 返回值类型为 List<HttpMultipartItem>
            def multipart = request.multipartBody()
            // 遍历所有数据
            multipart.each {
                // it -> HttpMultipartItem
                if (it.isFile()) {
                    $console.log("文件类型:${it.name()}")
                    // 文件类型的数据
                    // HttpMultipartItem.name() 可以获取数据名,也就是 Content-Disposition 请求头的 name 属性
                    $assert.assertTrue(it.name() == "filePartName", "文件数据name的值")
                    // HttpMultipartItem.value() 可以获取 name 对应的值, 此处为二进制数据, 可以保存到文件中
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
                    $console.log("文本类型:${it.name()}")
                    // 文本类型的数据
                    // HttpMultipartItem.name() 可以获取数据名,也就是 Content-Disposition 请求头的 name 属性
                    $assert.assertTrue(it.name() == "textPartName", "文本数据name的值")
                    // HttpMultipartItem.value() 可以获取 name 对应的值
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
def response = client.postMultipart("http://localhost:8080/postMultipart", {
    // delegate -> HttpClientMultipart
    // HttpClientMultipart.text() 用于添加文本类型的part
    text("textPartName", "textPartValue")
    // Files.buildFile() 用于构建一个 ScriptFile 对象
    def scriptFile = $files.buildFile {
        // delegate -> FileBuilder
        // FileBuilder.path() 用于设置文件路径
        delegate.path("/sdcard/test_postMultipart.txt")
    }
    // ScriptFile.writeText() 可以向文件中写入内容
    scriptFile.writeText("Hello postMultipart")
    // HttpClientMultipart.file() 用于添加文件类型的part
    file("filePartName", scriptFile, "custom_filename_test_postMultipart.txt")
})
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/postMultipart"
$assert.assertTrue(textResult == "/postMultipart", "返回结果为 /postMultipart")
// HttpServer.stop() 用于停止服务器.
server.stop()
```