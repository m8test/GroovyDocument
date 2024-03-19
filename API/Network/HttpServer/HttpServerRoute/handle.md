功能:

+ 处理Http请求.

定义:

+ [HttpServerRoute](/API/Network/HttpServer/HttpServerRoute/README.md) handle(Closure closure)

参数:

+ Closure closure - 处理Http请求的闭包.
    + 参数 - 无
    + delegate - [HttpServerCall](/API/Network/HttpServer/HttpServerCall/README.md)

返回值:

+ [HttpServerRoute](/API/Network/HttpServer/HttpServerRoute/README.md) - 返回对象本身方便链式调用

示例代码:

+ 在8080端口开启一个服务器,通过
  [HttpServerRoute.handle()](/API/Network/HttpServer/HttpServerRoute/README.md?id=handle)
  处理Http请求.

```groovy
// Floaty.showConsoleWindow() 用于显示控制台悬浮窗口
$floaty.showConsoleWindow()
// 启动服务器
def server = $httpServerManager.newServer(8080) {
    // delegate -> HttpServerConfig
    routing {
        // delegate -> HttpServerRouting
        // HttpServerRouting.route(path, closure)用于配置路由信息,在closure闭包可继续通过HttpServerRoute.route(path, closure)配置路由,或者通过HttpServerRoute.get(path, closure),HttpServerRoute.post(path, closure)等配置路由
        route("/handle") {
            // delegate -> HttpServerRoute
            // HttpServerRoute.method() 用于配置请求方法
            method("get") {
                // delegate -> HttpServerRoute
                // HttpServerRoute.handle() 用于处理Http请求
                handle {
                    // delegate -> HttpServerCall
                    // HttpServerCall.request() 可以获得请求对象 HttpServerRequest
                    def request = request()
                    // HttpServerRequest.path()可获得访问路径,此处为 "/handle"
                    def path = request.path()
                    $console.log("Path->$path")
                    // HttpServerCall.response() 可以获取响应对应 HttpServerResponse
                    def response = response()
                    // HttpServerResponse.textBody() 可以发送文本到客户端
                    response.textBody(path)
                }
            }
        }
    }
}
// HttpServer.start() 用于启动服务器,如果端口已经被占用了则会启动失败,报错 "Address already in use"
server.start()
// 新建一个Http客户端, HttpClientManager.newClient() 用于创建一个Http客户端
def client = $httpClientManager.newClient()
// HttpClient.get() 会返回一个 HttpClientResponse 对象,封装了Http响应信息
def response = client.get("http://localhost:8080/handle")
// HttpClientResponse.textBody() 可以将服务器返回结果转成文本
def textResult = response.textBody()
$console.log("服务器返回结果:$textResult")
// 断言返回结果为"/handle"
$assert.assertTrue(textResult == "/handle", "返回结果为 /handle")
// HttpServer.stop() 用于停止服务器.
server.stop()
```