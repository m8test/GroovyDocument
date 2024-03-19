功能:

+ 新建一个 [HttpClient](/API/Network/HttpClient/HttpClient/README.md) .

定义:

+ [HttpClient](/API/Network/HttpClient/HttpClient/README.md) newClient(Closure config = null)

参数:

+ Closure config - 客户端配置闭包
    + 参数 - 无
    + delegate - [HttpClientConfig](/API/Network/HttpClient/HttpClientConfig/README.md)

返回值:

+ [HttpClient](/API/Network/HttpClient/HttpClient/README.md) -
  新建的 [HttpClient](/API/Network/HttpClient/HttpClient/README.md)

示例代码:

+ 新建一个 [HttpClient](/API/Network/HttpClient/HttpClient/README.md) 并访问本地服务器.

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
        get("/newClient") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/newClient"
            def path = request.path()
            $assert.assertTrue(path == "/newClient")
            $console.log("Path->$path")
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
def client = $httpClientManager.newClient {
    // delegate -> HttpClientConfig
    // HttpClientConfig.followRedirects() 用于设置是否自动重定向Http请求
    followRedirects(true)
}
// HttpClient.get() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.get("http://localhost:8080/newClient")
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/newClient"
$assert.assertTrue(textResult == "/newClient", "返回结果为 /newClient")
// HttpServer.stop() 用于停止服务器.
server.stop()
```