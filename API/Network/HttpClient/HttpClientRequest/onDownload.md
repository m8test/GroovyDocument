功能:

+ 监听数据下载进度

定义:

+ [HttpClientRequest](/API/Network/HttpClient/HttpClientRequest/README.md) onDownload(long
  downloaded, long total)

参数:

+ long downloaded - 已下载数据大小
+ long total - 数据总大小

返回值:

+ [HttpClientRequest](/API/Network/HttpClient/HttpClientRequest/README.md) - 返回对象本身方便链式调用

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpClientRequest.onDownload()](/API/Network/HttpClient/HttpClientRequest/README.md?id=onDownload)
  监听数据下载进度再通过 [HttpClient.request()](/API/Network/HttpClient/HttpClient/README.md?id=request)
  方法从该服务器下载内容保存到本地.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 在8080端口新建一个服务器
def server = $httpServerManager.newServer(8080) {
    // delegate -> HttpServerConfig
    // HttpServerConfig.routing() 用于配置服务器路由信息
    routing {
        // delegate -> HttpServerRouting
        // HttpServerRouting.get() 用于配置Get路由
        get("/request") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/request"
            def path = request.path()
            $assert.assertTrue(path == "/request")
            $console.log("Path->$path")
            // HttpServerCall.response() 可以获取响应对应HttpServerResponse
            def response = response()
            // Files.buildFile() 用于构建一个 ScriptFile 对象
            def scriptFile = $files.buildFile {
                // delegate -> FileBuilder
                // FileBuilder.path() 用于设置文件路径
                delegate.path("/sdcard/test_onDownload.txt")
            }
            // ScriptFile.writeText() 可以向文件中写入内容
            scriptFile.writeText("Hello onDownload")
            // HttpServerResponse.bytesBody() 可以发送字节数组到客户端,ScriptFile.readBytes() 用于读取文件内容为字节数组
            response.bytesBody(scriptFile.readBytes())
        }
    }
}
// HttpServer.start() 用于启动服务器,如果端口已经被占用了则会启动失败,报错 "Address already in use"
server.start()
// 新建一个Http客户端, HttpClientManager.newClient() 用于创建一个Http客户端
def client = $httpClientManager.newClient()
// HttpClient.request() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.request("http://localhost:8080/request") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "get"
    // HttpClientRequest.onDownload() 用于监听数据下载进度
    onDownload { long downloaded, long total ->
        $console.log("已下载:$downloaded,总共:$total")
    }
}
// HttpClientResponse.bytesBody() 可以将服务器返回结果转成字节数组
def bytesBody = response.bytesBody()
// Files.buildFile() 用于构建一个 ScriptFile 对象
def scriptFile = $files.buildFile {
    // delegate -> FileBuilder
    // FileBuilder.path() 用于设置文件路径
    delegate.path("/sdcard/test_onDownload_backup.txt")
}
// ScriptFile.writeBytes() 可以向文件中写入字节数组
scriptFile.writeBytes(bytesBody)
// ScriptFile.readText() 可以读取文件内容为文本
def content = scriptFile.readText()
// 断言文件中的内容
$assert.assertTrue(content == "Hello onDownload", "下载文件内容")
// HttpServer.stop() 用于停止服务器.
server.stop()
```