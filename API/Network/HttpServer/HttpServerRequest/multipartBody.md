功能:

+ 将请求体内容读取为 List <[HttpMultipartItem](/API/Network/HttpCommon/HttpMultipartItem/README.md)> .

定义:

+ List\<[HttpMultipartItem](/API/Network/HttpCommon/HttpMultipartItem/README.md)> multipartBody()

参数:

+ 无

返回值:

+ List\<[HttpMultipartItem](/API/Network/HttpCommon/HttpMultipartItem/README.md)> - 返回对象本身方便链式调用

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpServerRequest.multipartBody()](/API/Network/HttpServer/HttpServerRequest/README.md?id=multipartBody)
  读取请求体为 List\<[HttpMultipartItem](/API/Network/HttpCommon/HttpMultipartItem/README.md)> .

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 在8080端口新建一个服务器
def server = $httpServerManager.newServer(8080) {
    // delegate -> HttpServerConfig
    // HttpServerConfig.routing() 用于配置服务器路由信息
    routing {
        // delegate -> HttpServerRouting
        // HttpServerRouting.post() 用于配置post路由
        post("/multipartBody") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/multipartBody"
            def path = request.path()
            $assert.assertTrue(path == "/multipartBody")
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
                    $assert.assertTrue(it.name() == "filePartName", "文本数据name的值")
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
// HttpClient.request() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.request("http://localhost:8080/multipartBody") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "post"
    // HttpClientRequest.multipartBody() 用于设置请求体内容
    multipartBody {
        // delegate -> HttpClientMultipart
        // HttpClientMultipart.text() 用于添加文本类型的part
        text("textPartName", "textPartValue")
        // Files.buildFile() 用于构建一个 ScriptFile 对象
        def scriptFile = $files.buildFile {
            // delegate -> FileBuilder
            // FileBuilder.path() 用于设置文件路径
            delegate.path("/sdcard/test_multipartBody.txt")
        }
        // ScriptFile.writeText() 可以向文件中写入内容
        scriptFile.writeText("Hello multipartBody")
        // HttpClientMultipart.file() 用于添加文件类型的part
        file("filePartName", scriptFile, "custom_filename_test_multipartBody.txt")
    }
}
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/multipartBody"
$assert.assertTrue(textResult == "/multipartBody", "返回结果为 /multipartBody")
// HttpServer.stop() 用于停止服务器.
server.stop()
```