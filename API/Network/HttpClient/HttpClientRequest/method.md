功能:

+ 设置Http请求方法

定义:

+ [HttpClientRequest](/API/Network/HttpClient/HttpClientRequest/README.md) method(
  String methodName)

参数:

+ String methodName - 请求方法,get,post,head等

返回值:

+ [HttpClientRequest](/API/Network/HttpClient/HttpClientRequest/README.md) - 返回对象本身方便链式调用

示例代码:

+

在8080端口开启一个服务器,通过 [HttpClientRequest.method()](/API/Network/HttpClient/HttpClientRequest/README.md?id=method)
设置 get,post 请求访问该服务器.

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
        get("/getMethod") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/getMethod"
            def path = request.path()
            $assert.assertTrue(path == "/getMethod")
            $console.log("Path->$path")
            // HttpServerCall.response() 可以获取响应对应HttpServerResponse
            def response = response()
            // HttpServerResponse.textBody() 可以发送文本到客户端
            response.textBody(path)
        }
        // HttpServerRouting.post() 用于配置post路由
        post("/postMethod") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/postMethod"
            def path = request.path()
            $assert.assertTrue(path == "/postMethod")
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
def client = $httpClientManager.newClient()
// HttpClient.request() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.request("http://localhost:8080/getMethod") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "get"
}
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("get请求服务器返回结果:$textResult")
// 断言返回结果为"/getMethod"
$assert.assertTrue(textResult == "/getMethod", "返回结果为 /getMethod")

// HttpClient.request() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
response = client.request("http://localhost:8080/postMethod") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为post请求.除此之外,还有get,put,patch,delete,head,options等方法
    method "post"
}
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
textResult = response.textBody()
$console.log("post请求服务器返回结果:$textResult")
// 断言返回结果为"/postMethod"
$assert.assertTrue(textResult == "/postMethod", "返回结果为 /postMethod")
// HttpServer.stop() 用于停止服务器.
server.stop()
```