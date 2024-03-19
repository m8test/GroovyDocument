功能:

+ 将请求体读取为字节数组.

定义:

+ byte[] bytesBody()

参数:

+ 无

返回值:

+ byte[] - 请求体转为字节数组的结果.

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpServerRequest.bytesBody()](/API/Network/HttpServer/HttpServerRequest/README.md?id=bytesBody)
  将请求体中的内容转为字节数组并写入文件中.

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
        post("/bytesBody") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/bytesBody"
            def path = request.path()
            $assert.assertTrue(path == "/bytesBody")
            $console.log("Path->$path")
            // HttpServerRequest.bytesBody() 可以将请求体内容转成字节数组
            def bytesBody = request.bytesBody()
            // Files.buildFile() 用于构建一个 ScriptFile 对象
            def scriptFile = $files.buildFile {
                // delegate -> FileBuilder
                // FileBuilder.path() 用于设置文件路径
                delegate.path("/sdcard/test_httpServerRequest_bytesBody_backup.txt")
            }
            // ScriptFile.writeBytes() 可以向文件中写入字节数组
            scriptFile.writeBytes(bytesBody)
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
def response = client.request("http://localhost:8080/bytesBody") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "post"
    // Files.buildFile() 用于构建一个 ScriptFile 对象
    def scriptFile = $files.buildFile {
        // delegate -> FileBuilder
        // FileBuilder.path() 用于设置文件路径
        delegate.path("/sdcard/test_httpServerRequest_bytesBody.txt")
    }
    // ScriptFile.writeText() 可以向文件中写入内容
    scriptFile.writeText("Hello httpServerRequest_bytesBody")
    // HttpClientRequest.body() 用于设置请求体内容,ScriptFile.readBytes() 用于读取文件内容为字节数组
    body(scriptFile.readBytes())
}
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/bytesBody"
$assert.assertTrue(textResult == "/bytesBody", "返回结果为 /bytesBody")
// HttpServer.stop() 用于停止服务器.
server.stop()
```