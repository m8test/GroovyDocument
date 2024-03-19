功能:

+ 获取此字符集在默认语言环境中的可读名称.

定义:

+ String displayName()

参数:

+ 无

返回值:

+ String - 此字符集在默认语言环境中的可读名称

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpCharset.displayName()](/API/Network/HttpCommon/HttpCharset/README.md?id=displayName)
  获取此字符集在默认语言环境中的可读名称

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
        get("/displayName") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/displayName"
            def path = request.path()
            $assert.assertTrue(path == "/displayName")
            $console.log("Path->$path")
            // HttpServerCall.response() 可以获取响应对应HttpServerResponse
            def response = response()
            // HttpServerResponse.textBody() 可以发送文本到客户端
            response.textBody(path, "text/plain; charset=gbk")
        }
    }
}
// HttpServer.start() 用于启动服务器,如果端口已经被占用了则会启动失败,报错 "Address already in use"
server.start()
// 新建一个Http客户端, HttpClientManager.newClient() 用于创建一个Http客户端
def client = $httpClientManager.newClient()
// HttpClient.request() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.request("http://localhost:8080/displayName") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "get"
}
// HttpClientResponse.charset() 可以获得响应体编码方式
def charset = response.charset()
// HttpCharset.displayName() 用于获取此字符集在默认语言环境中的可读名称.
def displayName = charset.displayName()
$assert.assertTrue(displayName == "GBK", "获取此字符集在默认语言环境中的可读名称")
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/displayName"
$assert.assertTrue(textResult == "/displayName", "返回结果为 /displayName")
// HttpServer.stop() 用于停止服务器.
server.stop()
```