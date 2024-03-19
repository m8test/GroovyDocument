功能:

+ 为Http服务器添加get请求的路由.

定义:

+ [HttpServerRoute](/API/Network/HttpServer/HttpServerRoute/README.md) get(String path = "/",
  Closure closure)

参数:

+ String path - (可选)添加路由的路径,默认为 "/"
+ Closure closure - 处理get请求的闭包,可处理来自客户端的get请求.
    + 参数 - 无
    + delegate - [HttpServerCall](/API/Network/HttpServer/HttpServerCall/README.md)

返回值:

+ [HttpServerRoute](/API/Network/HttpServer/HttpServerRoute/README.md) - 返回对象本身方便链式调用

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpServerRoute.get()](/API/Network/HttpServer/HttpServerRoute/README.md?id=get) 添加路由.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 在8080端口新建一个服务器
def server = $httpServerManager.newServer(8080) {
    // delegate -> HttpServerConfig
    // HttpServerConfig.routing() 用于配置服务器路由信息
    routing {
        // delegate -> HttpServerRouting
        // HttpServerRouting.get() 用于配置get路由
        get("/get") {
            // delegate -> HttpServerCall
            // HttpServerCall.request() 可以获得请求对象HttpServerRequest
            def request = request()
            // HttpServerRequest.path() 可获得访问路径,此处为 "/get"
            def path = request.path()
            $assert.assertTrue(path == "/get")
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
// HttpClient.get() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.get("http://localhost:8080/get")
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/get"
$assert.assertTrue(textResult == "/get", "返回结果为 /get")
// HttpServer.stop() 用于停止服务器.
server.stop()
```