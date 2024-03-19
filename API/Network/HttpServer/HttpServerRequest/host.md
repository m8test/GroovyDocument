功能:

+ 获取Http请求所访问的主机,可以是主机名(例如 localhost)或者主机ip(例如 127.0.0.1),不包括端口号.

定义:

+ String host()

参数:

+ 无

返回值:

+ String - Http 请求所访问的主机.

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpServerRequest.host()](/API/Network/HttpServer/HttpServerRequest/README.md?id=host)
  获取Http请求所访问的主机.

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
        get("/hostName") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/hostName"
            def path = request.path()
            $assert.assertTrue(path == "/hostName")
            $console.log("Path->$path")
            // HttpServerRequest.host() 用于获取访问的主机名,不包括端口号
            $assert.assertTrue(request.host() == "localhost", "主机名")
            // HttpServerCall.response() 可以获取响应对应HttpServerResponse
            def response = response()
            // HttpServerResponse.textBody() 可以发送文本到客户端
            response.textBody(path)
        }
        // HttpServerRouting.get() 用于配置Get路由
        get("/hostIp") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/hostIp"
            def path = request.path()
            $assert.assertTrue(path == "/hostIp")
            $console.log("Path->$path")
            // HttpServerRequest.host() 用于获取访问的主机名,不包括端口号
            $assert.assertTrue(request.host() == "127.0.0.1", "主机IP")
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
def response = client.request("http://localhost:8080/hostName") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "get"
}
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/hostName"
$assert.assertTrue(textResult == "/hostName", "返回结果为 /hostName")
// HttpClient.request() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
response = client.request("http://127.0.0.1:8080/hostIp") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "get"
}
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/hostIp"
$assert.assertTrue(textResult == "/hostIp", "返回结果为 /hostIp")
// HttpServer.stop() 用于停止服务器.
server.stop()
```