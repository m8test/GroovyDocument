功能:

+ 设置是否自动重定向http请求(状态码为301,302),默认情况下开启自动重定向功能.

定义:

+ [HttpClientConfig](/API/Network/HttpClient/HttpCLientConfig/README.md) followRedirects(boolean
  followRedirects)

参数:

+ boolean followRedirects - 是否自动重定向.

返回值:

+ [HttpClientConfig](/API/Network/HttpClient/HttpCLientConfig/README.md) - 返回对象本身方便链式调用

示例代码:

+ 在8080端口开启一个服务器,创建两个 [HttpClient](/API/Network/HttpClient/HttpClient/README.md)
  ,一个开启自动重定向,另外一个关闭自动重定向,再分别通过 [HttpClient.request()](/API/Network/HttpClient/HttpClient/README.md?id=request)
  访问该服务器.

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
        get("/followRedirects") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/followRedirects"
            def path = request.path()
            $assert.assertTrue(path == "/followRedirects")
            $console.log("Path->$path")
            // HttpServerCall.response1() 可以获取响应对应HttpServerResponse
            def response = response()
            // HttpServerResponse.textBody() 可以发送文本到客户端
            response.redirect("http://localhost:8080/afterRedirect", true)
        }
        // HttpServerRouting.get() 用于配置Get路由
        get("/afterRedirect") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/afterRedirect"
            def path = request.path()
            $assert.assertTrue(path == "/afterRedirect")
            $console.log("Path->$path")
            // HttpServerCall.response1() 可以获取响应对应HttpServerResponse
            def response = response()
            // HttpServerResponse.textBody() 可以发送文本到客户端
            response.textBody(path)
        }
    }
}
// HttpServer.start() 用于启动服务器,如果端口已经被占用了则会启动失败,报错 "Address already in use"
server.start()
// 新建一个Http客户端, HttpClientManager.newClient() 用于创建一个Http客户端
def client1 = $httpClientManager.newClient {
    // HttpClientConfig.followRedirects() 用于配置是否自动重定向
    followRedirects true
}
// HttpClient.request() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response1 = client1.request("http://localhost:8080/followRedirects") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "get"
}
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response1.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/afterRedirect"
$assert.assertTrue(textResult == "/afterRedirect", "返回结果为 /afterRedirect")
// 新建一个Http客户端, HttpClientManager.newClient() 用于创建一个Http客户端
def client2 = $httpClientManager.newClient {
    // HttpClientConfig.followRedirects() 用于配置是否自动重定向
    followRedirects false
}
// HttpClient.request() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response2 = client2.request("http://localhost:8080/followRedirects") {
    // delegate -> HttpClientRequest
    // HttpClientRequest.method() 用于配置请求方法,此处为配置为Get请求.除此之外,还有post,put,patch,delete,head,options等方法
    method "get"
}
// HttpClientResponse.statusCode() 可以获得响应状态码对象 HttpStatusCode
def statusCode = response2.statusCode()
// HttpStatusCode.value() 可以获得状态码的值
$assert.assertTrue(statusCode.value() == 301, "重定向状态码")
// HttpServer.stop() 用于停止服务器.
server.stop()
```