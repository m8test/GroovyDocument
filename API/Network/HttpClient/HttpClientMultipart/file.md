功能:

+ 添加文件类型的part.

定义:

+ [HttpClientMultipart](/API/Network/HttpClient/HttpClientMultipart/README.md) file(String name,
  ScriptFile scriptFile, String filename = null, String contentType = null, Map<String, String>
  headers = null)

参数:

+ String name - part名
+ ScriptFile scriptFile - 待添加的文件
+ String filename - (选填)文件名,默认使用 ScriptFile.name() 作为文件名.
+ String contentType - (选填)文件类型,默认根据文件获取类型.
+ Map<String, String> headers - (选填)part的header信息,默认为null.

返回值:

+ [HttpClientMultipart](/API/Network/HttpClient/HttpClientMultipart/README.md) - 返回对象本身方便链式调用

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpClientMultipart.file()](/API/Network/HttpClient/HttpClientMultipart/README.md?id=file)
  添加文本类型的 part
  后再通过 [HttpClient.postMultipart()](/API/Network/HttpClient/HttpClient/README.md?id=postMultipart)
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
        post("/file") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/file"
            def path = request.path()
            $assert.assertTrue(path == "/file")
            $console.log("Path->$path")
            // HttpServerRequest.multipartBody() 可以接收multipart类型的数据, 返回值类型为 List<HttpMultipartItem>
            def multipart = request.multipartBody()
            def part = multipart[0]
            $console.log("文件类型:${part.name()}")
            // HttpMultipartItem.name() 可以获取数据名,也就是 Content-Disposition 请求头的 name 属性
            $assert.assertTrue(part.name() == "filePartName", "文件数据name的值")
            // HttpMultipartItem.value() 可以获取 name 对应的值, 此处为二进制数据, 可以保存到文件中
            def value = part.value()
            // Files.buildFile() 用于构建一个 ScriptFile 对象
            def scriptFile = $files.buildFile {
                // delegate -> FileBuilder
                // FileBuilder.path() 用于设置文件路径
                delegate.path("/sdcard/${part.filename()}")
            }
            // ScriptFile.writeBytes() 可以向文件中写入字节数据
            scriptFile.writeBytes(value)
            // HttpMultipartItem.contentType() 可以获得 HttpContentType 对象
            def contentType = part.contentType()
            // HttpContentType.contentType() 获得主类型,例如 text/plain 中的 text, application/json 中的 application
            $assert.assertTrue(contentType.contentType() == "text", "content type")
            // HttpContentType.contentSubtype() 获得子类型,例如 text/plain 中的 plain, application/json 中的 json
            $assert.assertTrue(contentType.contentSubtype() == "plain", "content subtype")
            // HttpMultipartItem.headers() 可以获得 part 的 header 信息
            def headers = part.headers()
            // 断言 headers
            $assert.assertTrue(headers.get("header1") == "value1", "header1")
            $assert.assertTrue(headers.get("header2") == "value2", "header2")
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
def response = client.postMultipart("http://localhost:8080/file", {
    // delegate -> HttpClientMultipart
    // Files.buildFile() 用于构建一个 ScriptFile 对象
    def scriptFile = $files.buildFile {
        // delegate -> FileBuilder
        // FileBuilder.path() 用于设置文件路径
        delegate.path("/sdcard/test_multipart_file.txt")
    }
    // ScriptFile.writeText() 可以向文件中写入内容
    scriptFile.writeText("Hello file")
    // HttpClientMultipart.file() 用于添加文件类型的part
    file("filePartName", scriptFile, "custom_filename_test_multipart_file.txt", "text/plain", [header1: "value1", header2: "value2"])
})
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/file"
$assert.assertTrue(textResult == "/file", "返回结果为 /file")
// HttpServer.stop() 用于停止服务器.
server.stop()
```